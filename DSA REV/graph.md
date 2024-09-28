# Graph

---

### **1. Graph Representation: Adjacency List**

The **Adjacency List** representation of a graph is one of the most efficient ways to represent a graph, especially when dealing with a sparse graph (where the number of edges is much less than the maximum number of possible edges).

In an adjacency list:
- Each vertex maintains a list of its adjacent vertices (its neighbors).
- It allows us to efficiently iterate over all neighbors of a vertex.

#### **Adjacency List Implementation**

Let's implement an adjacency list representation of an **undirected** graph in Python. We'll use a dictionary where each key is a vertex, and the value is a list of adjacent vertices.

```python
class Graph:
    def __init__(self):
        # Use a dictionary to store adjacency lists
        self.graph = {}

    def add_edge(self, u, v):
        # For undirected graph, add edge both ways
        if u not in self.graph:
            self.graph[u] = []
        if v not in self.graph:
            self.graph[v] = []
        self.graph[u].append(v)
        self.graph[v].append(u)

    def print_graph(self):
        for vertex in self.graph:
            print(f"{vertex} -> {self.graph[vertex]}")

# Create a graph
g = Graph()
g.add_edge('A', 'B')
g.add_edge('A', 'C')
g.add_edge('B', 'D')
g.add_edge('C', 'D')

g.print_graph()
```

**Output:**
```
A -> ['B', 'C']
B -> ['A', 'D']
C -> ['A', 'D']
D -> ['B', 'C']
```

### **2. Adjacency List Implementation (Directed Graph)**

For a **directed graph**, we only add edges in one direction.

```python
class DirectedGraph:
    def __init__(self):
        self.graph = {}

    def add_edge(self, u, v):
        if u not in self.graph:
            self.graph[u] = []
        self.graph[u].append(v)

    def print_graph(self):
        for vertex in self.graph:
            print(f"{vertex} -> {self.graph[vertex]}")

# Create a directed graph
g = DirectedGraph()
g.add_edge('A', 'B')
g.add_edge('A', 'C')
g.add_edge('B', 'D')
g.add_edge('C', 'D')

g.print_graph()
```

**Output:**
```
A -> ['B', 'C']
B -> ['D']
C -> ['D']
```

### **3. Adjacency List and Matrix Comparison**

The **Adjacency Matrix** is another common way to represent a graph. It uses a 2D matrix (a 2D list in Python) to indicate the presence or absence of edges.

#### **Adjacency Matrix Implementation**
For an undirected, unweighted graph:

```python
class GraphMatrix:
    def __init__(self, num_vertices):
        # Create a num_vertices x num_vertices matrix initialized to 0
        self.matrix = [[0] * num_vertices for _ in range(num_vertices)]
        self.num_vertices = num_vertices

    def add_edge(self, u, v):
        # For undirected graph
        self.matrix[u][v] = 1
        self.matrix[v][u] = 1

    def print_graph(self):
        for row in self.matrix:
            print(row)

# Create a graph
g = GraphMatrix(4)  # Graph with 4 vertices
g.add_edge(0, 1)
g.add_edge(0, 2)
g.add_edge(1, 3)
g.add_edge(2, 3)

g.print_graph()
```

**Output:**
```
[0, 1, 1, 0]
[1, 0, 0, 1]
[1, 0, 0, 1]
[0, 1, 1, 0]
```

#### **Adjacency List vs. Adjacency Matrix Comparison**

| **Feature**                | **Adjacency List**                            | **Adjacency Matrix**                      |
|----------------------------|-----------------------------------------------|-------------------------------------------|
| **Space Complexity**        | \( O(V + E) \), where \( E \) is the number of edges | \( O(V^2) \), where \( V \) is the number of vertices |
| **Edge Lookup**             | \( O(E) \)                                   | \( O(1) \)                               |
| **Iterating Over Neighbors**| Efficient (\( O(\text{degree}) \))           | Inefficient (\( O(V) \))                 |
| **Suitable for**            | Sparse Graphs                                | Dense Graphs                             |

- **Adjacency List** is more space-efficient, especially for sparse graphs.
- **Adjacency Matrix** allows constant-time edge lookups, but uses more space.

---

### **4. Breadth-First Search (BFS) and Its Applications**

**Breadth-First Search (BFS)** is an algorithm for traversing or searching graph data structures. It starts at the root node and explores all the neighbor nodes at the present depth before moving on to nodes at the next depth level.

#### **BFS Implementation**

We'll implement BFS for an undirected graph represented using an adjacency list.

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])

    while queue:
        vertex = queue.popleft()
        if vertex not in visited:
            print(vertex, end=' ')
            visited.add(vertex)
            for neighbor in graph[vertex]:
                if neighbor not in visited:
                    queue.append(neighbor)

graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}

bfs(graph, 'A')
```

**Output:**
```
A B C D E F
```

#### **BFS Applications**
- **Shortest Path in an Unweighted Graph**: BFS finds the shortest path between two nodes in an unweighted graph.
- **Web Crawlers**: Exploring all pages connected to a particular web page.
- **Social Networks**: Finding the shortest connection between people (degrees of separation).
- **Peer-to-Peer Networks**: Searching for data distributed across peers.

---

### **5. Depth-First Search (DFS) and Its Applications**

**Depth-First Search (DFS)** is another algorithm for traversing or searching graph data structures. It starts at the root (or an arbitrary node), explores as far as possible along each branch before backtracking.

#### **DFS Implementation**

We can implement DFS using recursion (stack-based).

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)
    print(start, end=' ')

    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}

dfs(graph, 'A')
```

**Output:**
```
A B D E F C
```

#### **DFS Applications**
- **Topological Sorting**: Used in scheduling problems, DFS helps to perform topological sorting in Directed Acyclic Graphs (DAGs).
- **Cycle Detection**: DFS can be used to detect cycles in graphs.
- **Maze Solving**: DFS can explore all possible paths in a maze until it finds the goal.
- **Connected Components**: In an undirected graph, DFS can be used to identify all the connected components.
- **Pathfinding**: Similar to BFS, but DFS may find a path that is not the shortest.

---

### **Summary**

1. **Adjacency List Implementation**: We saw how to implement both directed and undirected graphs using an adjacency list.
2. **Adjacency List vs. Adjacency Matrix**: Adjacency lists are space-efficient for sparse graphs, while adjacency matrices provide constant-time edge lookup for dense graphs.
3. **Breadth-First Search (BFS)**: BFS explores a graph layer by layer and is useful for finding the shortest path in unweighted graphs.
4. **Depth-First Search (DFS)**: DFS explores as far as possible along each branch and is useful for tasks like topological sorting, cycle detection, and maze solving.


Below is a detailed explanation of each of the requested graph algorithms and concepts, along with Python implementations where appropriate:

---

### **1. Detect Cycle in an Undirected Graph**

A cycle in an **undirected graph** occurs when there is a path that begins at a vertex and returns to the same vertex without repeating any edges. To detect a cycle, we can use Depth-First Search (DFS).

#### **Algorithm (DFS-based Approach)**:
- Start DFS from any vertex.
- Track visited vertices.
- For every visited vertex, check its neighbors.
- If a neighbor is already visited and is not the parent of the current vertex, then there is a cycle.

#### **Python Code for Cycle Detection in an Undirected Graph**:

```python
class Graph:
    def __init__(self, vertices):
        self.graph = {i: [] for i in range(vertices)}

    def add_edge(self, u, v):
        self.graph[u].append(v)
        self.graph[v].append(u)

    def is_cyclic_util(self, v, visited, parent):
        visited[v] = True

        for neighbor in self.graph[v]:
            if not visited[neighbor]:
                if self.is_cyclic_util(neighbor, visited, v):
                    return True
            elif neighbor != parent:
                return True
        return False

    def is_cyclic(self):
        visited = [False] * len(self.graph)
        for i in range(len(self.graph)):
            if not visited[i]:
                if self.is_cyclic_util(i, visited, -1):
                    return True
        return False


g = Graph(5)
g.add_edge(0, 1)
g.add_edge(1, 2)
g.add_edge(2, 0)
g.add_edge(1, 3)
g.add_edge(3, 4)

print("Cycle Detected" if g.is_cyclic() else "No Cycle Detected")
```

**Output**:  
`Cycle Detected`

---

### **2. Detect Cycle in a Directed Graph**

In a **directed graph**, a cycle exists if we can revisit a vertex after moving along directed edges. The simplest approach to detect cycles in a directed graph is using DFS with a "recursion stack."

#### **Algorithm (DFS-based with Recursion Stack)**:
- Track visited vertices and a recursion stack.
- If a vertex is found in the recursion stack during DFS traversal, it means there is a cycle.

#### **Python Code for Cycle Detection in a Directed Graph**:

```python
class DirectedGraph:
    def __init__(self, vertices):
        self.graph = {i: [] for i in range(vertices)}

    def add_edge(self, u, v):
        self.graph[u].append(v)

    def is_cyclic_util(self, v, visited, rec_stack):
        visited[v] = True
        rec_stack[v] = True

        for neighbor in self.graph[v]:
            if not visited[neighbor]:
                if self.is_cyclic_util(neighbor, visited, rec_stack):
                    return True
            elif rec_stack[neighbor]:
                return True

        rec_stack[v] = False
        return False

    def is_cyclic(self):
        visited = [False] * len(self.graph)
        rec_stack = [False] * len(self.graph)

        for node in range(len(self.graph)):
            if not visited[node]:
                if self.is_cyclic_util(node, visited, rec_stack):
                    return True
        return False


g = DirectedGraph(4)
g.add_edge(0, 1)
g.add_edge(1, 2)
g.add_edge(2, 0)
g.add_edge(3, 2)

print("Cycle Detected" if g.is_cyclic() else "No Cycle Detected")
```

**Output**:  
`Cycle Detected`

---

### **3. Topological Sorting**

**Topological Sort** is a linear ordering of vertices in a Directed Acyclic Graph (DAG) where for every directed edge \(u \to v\), vertex \(u\) comes before \(v\) in the ordering. Topological sort is useful in scheduling tasks.

#### **Algorithm (DFS-based)**:
- Perform DFS and push the vertex to a stack after finishing all its neighbors.
- Reverse the stack at the end to get the topological sort.

#### **Python Code for Topological Sorting**:

```python
class Graph:
    def __init__(self, vertices):
        self.graph = {i: [] for i in range(vertices)}

    def add_edge(self, u, v):
        self.graph[u].append(v)

    def topological_sort_util(self, v, visited, stack):
        visited[v] = True
        for neighbor in self.graph[v]:
            if not visited[neighbor]:
                self.topological_sort_util(neighbor, visited, stack)
        stack.append(v)

    def topological_sort(self):
        visited = [False] * len(self.graph)
        stack = []

        for i in range(len(self.graph)):
            if not visited[i]:
                self.topological_sort_util(i, visited, stack)

        print(stack[::-1])


g = Graph(6)
g.add_edge(5, 2)
g.add_edge(5, 0)
g.add_edge(4, 0)
g.add_edge(4, 1)
g.add_edge(2, 3)
g.add_edge(3, 1)

g.topological_sort()
```

**Output**:  
`[5, 4, 2, 3, 1, 0]`

---

### **4. Shortest Path Problems**

#### **4.1 Dijkstra’s Algorithm (Shortest Path in Weighted Graph)**

**Dijkstra’s Algorithm** finds the shortest path from a source to all vertices in a graph with non-negative edge weights.

#### **Algorithm**:
- Use a priority queue to explore vertices with the shortest known distance.
- Update distances to neighboring vertices as smaller distances are found.

#### **Python Code for Dijkstra’s Algorithm**:

```python
import heapq

def dijkstra(graph, start):
    pq = [(0, start)]
    distances = {vertex: float('inf') for vertex in graph}
    distances[start] = 0

    while pq:
        current_distance, current_vertex = heapq.heappop(pq)

        if current_distance > distances[current_vertex]:
            continue

        for neighbor, weight in graph[current_vertex]:
            distance = current_distance + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(pq, (distance, neighbor))

    return distances

graph = {
    'A': [('B', 1), ('C', 4)],
    'B': [('A', 1), ('C', 2), ('D', 5)],
    'C': [('A', 4), ('B', 2), ('D', 1)],
    'D': [('B', 5), ('C', 1)]
}

distances = dijkstra(graph, 'A')
print(distances)
```

**Output**:  
`{'A': 0, 'B': 1, 'C': 3, 'D': 4}`

---

#### **4.2 Bellman-Ford Algorithm**

**Bellman-Ford Algorithm** can handle negative weights and finds the shortest paths from a source vertex to all other vertices.

#### **Algorithm**:
- Relax all edges \(V-1\) times, where \(V\) is the number of vertices.
- Check for negative weight cycles by verifying whether further relaxation is possible.

#### **Python Code for Bellman-Ford Algorithm**:

```python
class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.edges = []

    def add_edge(self, u, v, weight):
        self.edges.append((u, v, weight))

    def bellman_ford(self, src):
        dist = [float('inf')] * self.V
        dist[src] = 0

        for _ in range(self.V - 1):
            for u, v, weight in self.edges:
                if dist[u] != float('inf') and dist[u] + weight < dist[v]:
                    dist[v] = dist[u] + weight

        # Check for negative weight cycles
        for u, v, weight in self.edges:
            if dist[u] != float('inf') and dist[u] + weight < dist[v]:
                print("Graph contains negative weight cycle")
                return

        print(dist)


g = Graph(5)
g.add_edge(0, 1, -1)
g.add_edge(0, 2, 4)
g.add_edge(1, 2, 3)
g.add_edge(1, 3, 2)
g.add_edge(1, 4, 2)
g.add_edge(3, 2, 5)
g.add_edge(3, 1, 1)
g.add_edge(4, 3, -3)

g.bellman_ford(0)
```

**Output**:  
`[0, -1, 2, -2, 1]`

---

### **5. Prim's Algorithm (Minimum Spanning Tree)**

**Prim's Algorithm** finds a minimum spanning tree for a connected weighted undirected graph. It grows the spanning tree by adding edges one by one that connect the tree to a new vertex.

#### **Python Code for Prim’s Algorithm**:

```python
import heapq

def prim(graph, start):
    mst = []
    visited = set()
    pq = [(0, start, None)]  # (cost, node, parent)

    while pq:
        cost, node, parent = heapq.heappop(pq)
        if node not in

 visited:
            visited.add(node)
            if parent is not None:
                mst.append((parent, node, cost))

            for neighbor, weight in graph[node]:
                if neighbor not in visited:
                    heapq.heappush(pq, (weight, neighbor, node))

    return mst

graph = {
    'A': [('B', 1), ('C', 2)],
    'B': [('A', 1), ('C', 4), ('D', 6)],
    'C': [('A', 2), ('B', 4), ('D', 3)],
    'D': [('B', 6), ('C', 3)]
}

mst = prim(graph, 'A')
print(mst)
```

**Output**:  
`[('A', 'B', 1), ('A', 'C', 2), ('C', 'D', 3)]`

---

