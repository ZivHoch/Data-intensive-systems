## Data-intensive-systems

This repository focuses on understanding and optimizing processes within a network provider's infrastructure. The company operates multiple servers, each responsible for executing service tasks. A service task involves local processing by the server, which may also delegate subtasks to other servers. These subtasks are integral to completing the service task effectively.

### Overview

In this system, a server receives a service request either from a user or another server and responds with a service response. The duration of a service task is the time elapsed between receiving the request and sending the response. Importantly, we disregard network delays for simplicity in modeling.

### Example Scenario

Consider a scenario where Server S1 receives a request to purchase a book (X) from a user at time t0. Server S1, realizing the need for a credit check, sends a request to Server S2 at time t1. Meanwhile, at time t3, Server S1 receives another request to buy another book (Y). It further requests an ID check from Server S3 at time t4. Subsequently, Server S1 receives a response from Server S2 at time t5 and responds to the initial book purchase request at time t6. Finally, Server S1 receives a response from Server S3 at time t7.

### Log File Analysis

The system logs each request and response exchange between servers in the following format:

```<FromServer, ToServer, time, action (Request or Response), processId >```


### Goals

1. **Identify Variations**: The first goal is to identify variations in processes recorded in the log file. Processes exhibiting similar characteristics should be represented by a unified representation to simplify analysis.
2. **Group Similar Processes**: The second goal involves grouping processes that share some similarities but are distinct enough to warrant separate representations.

### Approach

To achieve these goals, we'll develop a comprehensive framework consisting of:

- **Data Parsing**: Extracting information from the log file to understand the sequence of requests and responses.
- **Feature Extraction**: Identifying key features of processes such as server interactions, timing, and process identifiers.
- **Clustering Algorithms**: Employing clustering techniques to group similar processes based on extracted features.
- **Process Representation**: Designing a method to represent processes efficiently, potentially using statistical summaries or unique identifiers.
- **Evaluation**: Assessing the effectiveness and efficiency of the framework through rigorous testing and validation.

### Implementation

The framework will be implemented as a program capable of analyzing log files, performing clustering, and generating representations of processes. Detailed documentation will accompany the codebase to facilitate understanding and usage.

### Evaluation

Evaluation will involve testing the framework on various datasets to ensure its robustness and scalability. Metrics such as clustering accuracy, representation compactness, and runtime performance will be measured to gauge effectiveness.

### Conclusion

By developing this framework, we aim to enhance understanding and optimization of data-intensive processes within network provider systems. The ability to identify variations and similarities in processes will facilitate more efficient resource allocation and system management.
