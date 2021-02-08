# Reject the Optimization to Skip Veirification on the Block Submitted via RPC

We decide to reject the proposal to allow skipping verification on the block submitted via RPC (#238).

Because it violates the principle that the CKB node must validate the data it receives before relaying them to the network.

Such an optimization may bring benefits to miners, but once there's a bug in the alternative miner implementation, the impact will spread to the whole network. As the CKB chain developers, we keep neutral to the network participants and recard the network balance as our first priority.
