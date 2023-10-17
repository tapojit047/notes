# ZooKeeper:
ZooKeeper is a distributed coordination service that provides a reliable and highly available way to manage the coordination and configuration of distributed systems. It is often used in complex distributed applications to ensure that different nodes in the system can agree on and coordinate various tasks and decisions. The characteristics you've listed describe the basic building blocks and features of ZooKeeper:

In a distributed system, there are multiple nodes or machines that need to communicate with each other and coordinate their actions. ZooKeeper provides a way to ensure that these nodes are aware of each other and can coordinate their actions. It does this by maintaining a hierarchical tree of data nodes called "Znodes".

- **ZooKeeper Internal Data Structure is like a Tree:**
  - ZooKeeper's internal data structure is organized as a hierarchical tree-like structure. This structure is similar to a **file system**, where data is organized in a tree of directories and files.
  
![Screenshot from 2023-10-17 11-51-39.png](..%2F..%2Fimages%2FScreenshot%20from%202023-10-17%2011-51-39.png)

- **Each Node is Called a zNode**:
  - In ZooKeeper, each element in the tree structure is referred to as a "zNode." ZNodes are the fundamental data units and are used to store data and represent a node in the distributed system.
- **Each zNode Has a Path**:
  - Each zNode in the ZooKeeper hierarchy is identified by a unique path within the tree. Paths are similar to file paths in a file system and help locate and address specific zNodes.
  -  Druid clusters often consist of multiple nodes. ZooKeeper paths can be used to register and discover the available Druid services and nodes. For example, paths like "/druid/brokers" and "/druid/coordinators" can be used to list and discover broker and coordinator nodes, respectively.
- **Each zNode Can Store Data**:
  - ZNodes can store a small amount of associated data. 
  - For example, The leader stores information in a zNode to announce its status and other nodes watch this zNode to detect leadership changes.
- **No Renaming of zNode**:
  - ZooKeeper does not support renaming zNodes. If you need to change the name or location of a zNode, you typically need to create a new zNode with the desired name, copy the data, and then delete the old zNode.
- **Each zNode Can Be WATCHed for Changes:**
  - Clients can register watches on zNodes to receive notifications when changes occur. This feature allows clients to react to updates in the distributed system's state, such as changes in configuration, leadership, or the presence of other clients.

![Screenshot from 2023-10-17 11-52-05.png](..%2F..%2Fimages%2FScreenshot%20from%202023-10-17%2011-52-05.png)


![Screenshot from 2023-10-17 15-49-37.png](..%2F..%2Fimages%2FScreenshot%20from%202023-10-17%2015-49-37.png)
- The ZooKeeper architecture consists of a hierarchy of nodes called znodes, organized in a tree-like structure. Each znode can store data and has a set of permissions that control access to the znode. The znodes are organized in a hierarchical namespace, similar to a file system. At the root of the hierarchy is the root znode, and all other znodes are children of the root znode. The hierarchy is similar to a file system hierarchy, where each znode can have children and grandchildren, and so on.