State - an object that represents a possible configuration of the word (agent and environment)

State space of a problem is the set of all possible states for that problem

State space graph - kinda like a NFA. State A --(action)-> State B
![](images/Pasted%20image%2020240719091858.png)

Actions are available depending on environment, so in above image all the loops are pointless (stay in the same state), so are unnecessary

### Directed graph
Many AI problems can be abstracted into the problem of finding a path in a directed graph.
- A **graph** consists of a set of **nodes** (usually states) and a set of **arcs**/edges (usually actions).
- In theory, a **path** is a sequence of nodes (n0,n1,n2,...) where there is an arc from n_i to n_(i+1). Practically, a path is a sequence of arcs
- The length of a path is **k**.
- An arc can have an associated cost/weight. The cost of a path is the sum of the cost of the arcs used by the path.
- Given a set of **starting nodes** and a set of **goal nodes**/desired states, a **solution** is a path from a starting node to a goal node.

### Explicit vs Implicit graphs
Explicit graphs
- Nodes and vertices are readily available
- The entire graph is in memory
- Stored in a structure like an adjacency list/matrix
- The complexity of algorithms is measured in terms of the number of vertices or edges
Implicit graphs
- Neighbours of a node only known by visiting that node
- The graph is generated on the fly
- The complexity of algorithms is measured in terms of the **depth** of a goal node and the **average branching factor** (average number of outgoing arcs)

### Searching graphs
Generic search algorithm - given a graph, start nodes, and goal nodes, incrementally explore paths from the start nodes.
- Maintain a **frontier** of explored paths
- As search goes on, frontier is updated and graph explored until a goal node found.
- The way the paths are removed from the frontier defines the **search strategy**
- 