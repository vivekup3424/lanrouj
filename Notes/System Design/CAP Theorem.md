
![[Pasted image 20241127234550.png]]

The **CAP theorem**, proposed by Eric Brewer, is a fundamental principle in distributed systems. 
It states that in a distributed data system, it is impossible to simultaneously guarantee all three of the following properties:

1. **Consistency (C)**  
    Every read receives the most recent write or an error. In other words, all nodes in the system return the same data if queried, ensuring uniformity.
    
    - **Example**: If a user updates their profile, any subsequent read from the system will reflect the updated profile immediately.
2. **Availability (A)**  
    Every request (read or write) receives a response, regardless of the system state (but not necessarily the most recent write).
    
    - **Example**: Even if some nodes are unreachable or delayed, the system still provides responses to requests, though they might be outdated.
3. **Partition Tolerance (P)**  
    The system continues to operate despite arbitrary partitioning due to network failures. A network partition happens when communication is interrupted between some nodes, effectively dividing the system into disjoint segments.
    
    - **Example**: If a data center loses connectivity, the system still serves clients connected to it.

### The Tradeoff

The CAP theorem argues that a distributed system can satisfy **at most two** of the three properties at any given time. Here's why:

- **Consistency and Availability without Partition Tolerance (CA systems):** If a network partition occurs, CA systems cannot function properly. They rely on a fully connected network. Such systems ensure data uniformity and responsiveness but will fail when partitions arise.
    
    - **Example**: Traditional relational databases that assume no network partition.
    - Imaginary concept not conceivable in reality.
    
- **Consistency and Partition Tolerance without Availability (CP systems):** These systems prioritize data accuracy over responsiveness during a partition. If nodes can't synchronize due to a partition, the system may refuse to serve requests until the partition resolves.
    
    - **Example**: Some distributed databases like HBase or MongoDB in strict consistency modes.
- **Availability and Partition Tolerance without Consistency (AP systems):** AP systems prioritize availability and resilience to partitions, even if it means serving stale or inconsistent data.
    
    - **Example**: DNS systems or systems like DynamoDB are designed to handle partitions while remaining available.

### Real-World Implications

1. **Eventual Consistency (AP Systems):** Many distributed systems adopt eventual consistency, meaning data becomes consistent over time once the partition resolves. This is a compromise to balance the tradeoffs.
    
2. **Latency and Network Failures:** Real-world networks are imperfect, and partitions are inevitable. Most modern systems choose partition tolerance (P) as a fundamental requirement, leaving them to decide between consistency (C) and availability (A).
    
3. **Use Cases:**
    
    - **C-preferring systems (CP):** Banking systems, financial services, or applications where strong data consistency is critical.
    - **A-preferring systems (AP):** Social media feeds, messaging apps, or systems prioritizing availability for user experience.

### Example Scenarios

- **CA Example:** Centralized databases with backups but no tolerance for network failures.
- **CP Example:** A ticketing system that ensures no overselling of tickets by sacrificing availability during partitioning.
- **AP Example:** Online shopping cart services that allow users to add items even during network disruptions but might show stale prices.
