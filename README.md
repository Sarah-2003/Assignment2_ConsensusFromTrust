# Distributed Consensus Algorithm

## Overview
This repository contains the implementation of a distributed consensus algorithm designed to resist Sybil attacks while minimizing energy consumption compared to traditional proof-of-work mechanisms. The implementation focuses on a graph of trust relationships between nodes, where nodes can either be compliant or malicious.

## Assignment Details
The project involves creating a `CompliantNode` class that implements the `Node` interface. Each compliant node behaves according to the rules defined by the assignment, and aims to achieve consensus with its peers through a series of rounds, even in the presence of malicious nodes.

## Project Structure
- **`Node.java`**: The interface defining the methods that must be implemented by any node in the network.
- **`CompliantNode.java`**: The main implementation of the compliant node, which includes the consensus algorithm.
- **`Candidate.java`**: A class that represents candidate transactions received from other nodes.
- **`MaliciousNode.java`**: An example implementation of a malicious node for testing purposes.
- **`Simulation.java`**: A class that generates a random directed graph of nodes and manages the simulation of rounds for consensus testing.
- **`Transaction.java`**: A simple wrapper class for representing transactions.

## Implementation Details

### CompliantNode Class
The `CompliantNode` class is responsible for:
- Following its designated followees as defined by a boolean array.
- Receiving candidate transactions from its followees.
- Proposing a set of transactions to its followers each round.
- Achieving consensus by determining which transactions are valid based on the proposals received from its followers.

#### Key Methods
- **`setFollowees(boolean[] followees)`**: Initializes the list of followees for the node.
- **`setPendingTransaction(Set<Transaction> pendingTransactions)`**: Sets the initial list of transactions that the node can propose.
- **`sendToFollowers()`**: Returns the set of transactions the node proposes to its followers.
- **`receiveFromFollowees(Set<Candidate> candidates)`**: Processes the candidates received from its followees.

### Consensus Algorithm
The consensus algorithm iteratively collects proposals from followees over a specified number of rounds. At each round:
1. The node collects proposals from its followees.
2. It evaluates the proposals to determine which transactions have the majority support.
3. The node then broadcasts the agreed-upon transactions to its followers.

### Handling Malicious Nodes
The implementation is designed to withstand up to 45% of malicious nodes by leveraging the majority consensus approach. The algorithm ignores proposals that do not meet the trust threshold, ensuring that malicious behavior does not dominate the decision-making process.

## Graph Parameters
The network is defined by several parameters:
- **Pairwise Connectivity Probability**: {0.1, 0.2, 0.3}
- **Malicious Node Probability**: {0.15, 0.30, 0.45}
- **Transaction Communication Probability**: {0.01, 0.05, 0.10}
- **Number of Rounds**: {10, 20}

## How to Run the Project

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd distributed-consensus-algorithm
   ```

2. Compile the Java files:
   ```bash
   javac *.java
   ```

3. Run the simulation:
   ```bash
   java Simulation
   ```

## Testing
The implementation has been tested against a variety of scenarios with different graph parameters. Results indicate the success rate of reaching consensus under various configurations, along with the performance metrics such as execution time and consensus size.

## Conclusion
The CompliantNode implementation effectively demonstrates how distributed consensus can be achieved in the presence of malicious nodes while minimizing resource consumption. This project provides a practical understanding of trust-based consensus mechanisms in distributed systems.
