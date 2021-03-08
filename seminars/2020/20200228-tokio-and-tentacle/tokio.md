## tokio 内部分享

Rust 的异步模型是**协作式就绪通知模型**，Runtime 实现不归编译器实现，一种开放式的实现，编译器只做最核心的 trait 规范，其余由社区百花齐放。但实际上，真正有能力写一个高效稳定的 Runtime 的人是相对少的，有意愿去写的就更少了，除非没有办法，比如在 kernel 内需要实现一个基于 Rust async 的通知机制，这种特定场景需要完全自己实现，一般来说，社区大部分会在 tokio 和 async-std 中选择一个作为自己的核心依赖。

### 工作队列和线程池

默认与核心数相同的异步执行线程，每个队列有自己的 local queue，并共享全局 queue，同时还对没有 poll 过的 Future 使用插队的方式，让其尽快执行。

工作线程获取任务的优先级是：

1. local + lifo_slot 混合第一
2. 查看不空闲的其他 worker 的队列
3. 查看全局队列

tokio 有两个线程池，默认异步执行线程会开与核心数相同的线程用来执行异步任务，而 blocking 线程池，默认不开，当出现 blocking 任务后再尝试开启。

blocking 线程池负责执行重计算任务，同时也有将当前异步线程直接转换为 blocking 线程的 api，相当于对异步线程的切换，支持无法 send 的 blocking 任务。

### Driver 在 tokio 内部的执行

每一个工作线程就是一个 Driver，在空闲时刻，工作线程会 park 在各种 driver 的 poll 上，包括 io/timer 等等。

#### IO Driver

网络类的底层 Future，由 tokio 实现，实现的过程是通过 `PollEvented::new_with_interest` 将 fd 对应的 token 与 tokio 端的资源绑定，当 epoll wake 对应的 token 的时候，io driver wake 对应的网络资源。

#### Timing wheel

根据[论文](http://www.cs.columbia.edu/~nahum/w6998/papers/ton97-timing-wheels.pdf)描述，存在七种计时器的实现：

##### Straightforward

- 适用于只存在较少计时器的场景
- 所有计时需求都在较少的 clock 内完成
- 获取 os per tick 的消息来自于专门优化的硬件

操作是，每次获取 trick 之后所有 timer 时间相应减少

##### Ordered List

相比于第一种来说，可以同时支持稍微多一点的计时任务需求，但在需要动态大量插入计时任务的情况下，插入操作消耗会比较大。

同时因为 ordered list 的存在有最小计时的记录，os 时钟不需要每个 tick 中断一次进行查询，大幅降低计时消耗。

##### Tree-Based Algorithms

将计时任务的排序改为 Tree-base 的实现，比如最小堆，排序算法消耗将从 O(n) 降为 O(logn)

##### Basic time wheel

规定最大计时上限，将计时任务限定在当前时间指针 + 时间偏移最大上限之间，类似桶排序，排序消耗从 O(logn) 近似下降到 O(1)，只是一个求模运算，就直接插入对应的桶中了，但当时间指针指向某一个桶的时候，需要遍历其中的所有任务找到到期任务

##### Hash Table With Sorted Lists

将桶中队列进行排序处理，当 hash 足够平均的时候，timer 的 callback 操作也将从 O(n) 降到 O(1)，但插入计时任务将可能变为 O(n)

##### Hash Table with Unsorted Lists

因为不需要排序，可以降低插入计时任务的消耗

##### Exploiting Hierarchy

将时间论分级，比如分为 ms，s，min，hour，day，year，每个级别有固定长度，相当于一个插槽，可以将对应匹配的任务插入其中，时钟将从最小的地方开始每个 tick，如果最小单位没有，就直接跳入当前最小的任务，当 year 的任务经过一定的时间之后，需要自行调整到小单位的对应队列中，最小精度就是支持的最小单位中的每个插槽代表的单位。这是目前 tokio 的实现。

### Future 在 tokio 内部的运行

Future 将会被转换成 Cell，进而变成 RawTask（C ABI 的 ptr），再包装成 Task，在真正执行的时候，是 Harness

tokio 内部的 task 有对应的状态，避免无效操作：

- running
- notify: in queue
- idle: pending
- complete: finished
- terminal: clean
- shutdown: runtime shutdown

比如 notify 之前会查看状态，决定是否需要将任务插入队列

wake 操作的语义是将对应任务唤醒执行，在 tokio 的实现里，wake 操作实现为将自己插入任务队列

### 配额机制

为了缓解在协作异步模型下的无限执行问题，tokio 在执行 Future 的时候会计算 budget 值，当值为零时，如果当前任务还需要运行，则将其强制塞到队列最后面去，给予其他任务运行的机会，一种强制平衡的措施。

但这种 budget 的设定只在 tokio 提供的底层类型中才有，包括 lock、net、channel 等。


可以参考 [PPT](https://docs.google.com/presentation/d/1Yi5H3Tyos18GiS0-ZEVl3WzN6FALQ9drOIe1ggavlhg/edit?usp=sharing)，这里只列举了 tokio 的主干逻辑，分支及代码实现上会比较复杂，但这些机制的描述已经让新手能够相对熟悉 tokio 的机制和能力，如果想更细致了解，可以去细读源码。
