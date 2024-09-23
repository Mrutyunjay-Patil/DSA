---
tags: [DSA Java]
title: Course Module 6. Graph Algorithms
created: '2024-09-17T14:10:20.730Z'
modified: '2024-09-17T14:32:27.142Z'
---

# **Course Module 6. Graph Algorithms**

**Duration:** 2 Weeks

Graph Algorithms are essential tools in computer science used to solve problems related to networks, such as social networks, transportation systems, and communication networks. Understanding these algorithms will enhance your ability to navigate complex data structures, optimize routes, and analyze connections efficiently. This module is designed to break down these advanced topics into simple, understandable concepts, making them accessible even to those without a strong technical background.

---

## **Week 1: Graph Traversal and Shortest Path Algorithms**

### **1. Graph Traversal Algorithms**

Graph traversal refers to the process of visiting all the nodes (vertices) in a graph in a systematic manner. The two primary traversal algorithms are Depth-First Search (DFS) and Breadth-First Search (BFS).

#### **1.1 Depth-First Search (DFS)**

**Overview:**
Depth-First Search (DFS) is an algorithm for traversing or searching tree or graph data structures. It starts at a selected node (often called the "root" in trees) and explores as far as possible along each branch before backtracking.

**How It Works:**
- **Start** at the root node.
- **Explore** each branch before backtracking.
- **Use** a stack (either explicitly or via recursion) to keep track of the path.

**Example:**
Consider the following graph:

```
    A
   / \
  B   C
 / \   \
D   E   F
```

**Steps:**
1. Start at A.
2. Move to B.
3. Move to D (as deep as possible).
4. Backtrack to B and move to E.
5. Backtrack to A and move to C.
6. Move to F.

**Java Implementation:**

```java
import java.util.*;

public class DepthFirstSearch {
    // Function to perform DFS
    public static void dfs(Map<Character, List<Character>> graph, char start, Set<Character> visited) {
        // Mark the current node as visited
        visited.add(start);
        System.out.print(start + " ");
        
        // Recur for all the vertices adjacent to this vertex
        for (char neighbor : graph.get(start)) {
            if (!visited.contains(neighbor)) {
                dfs(graph, neighbor, visited);
            }
        }
    }

    // Example usage
    public static void main(String[] args) {
        // Creating a graph using adjacency list representation
        Map<Character, List<Character>> graph = new HashMap<>();
        graph.put('A', Arrays.asList('B', 'C'));
        graph.put('B', Arrays.asList('A', 'D', 'E'));
        graph.put('C', Arrays.asList('A', 'F'));
        graph.put('D', Arrays.asList('B'));
        graph.put('E', Arrays.asList('B'));
        graph.put('F', Arrays.asList('C'));

        Set<Character> visited = new HashSet<>();
        System.out.println("DFS Traversal starting from A:");
        dfs(graph, 'A', visited);
        // Output: A B D E C F 
    }
}
```

**Explanation:**
- **Graph Representation:** The graph is represented as an adjacency list using a `Map<Character, List<Character>>`.
- **Visited Set:** Keeps track of visited nodes to avoid cycles.
- **DFS Function:** Recursively visits each node and its neighbors.

**Time Complexity:** O(V + E) where V is the number of vertices and E is the number of edges.

**Space Complexity:** O(V) due to the recursion stack and the visited set.

**When to Use:**
- Solving puzzles like mazes.
- Topological sorting.
- Finding connected components.

---

#### **1.2 Breadth-First Search (BFS)**

**Overview:**
Breadth-First Search (BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the root node and explores all neighboring nodes at the present depth before moving on to nodes at the next depth level.

**How It Works:**
- **Start** at the root node.
- **Explore** all immediate neighbors.
- **Move** to the next level of nodes.
- **Use** a queue to keep track of the nodes to visit next.

**Example:**
Using the same graph as above:

```
    A
   / \
  B   C
 / \   \
D   E   F
```

**Steps:**
1. Start at A.
2. Visit neighbors B and C.
3. Visit neighbors of B (D and E) and neighbor of C (F).

**Java Implementation:**

```java
import java.util.*;

public class BreadthFirstSearch {
    // Function to perform BFS
    public static void bfs(Map<Character, List<Character>> graph, char start) {
        Set<Character> visited = new HashSet<>();
        Queue<Character> queue = new LinkedList<>();

        // Mark the start node as visited and enqueue it
        visited.add(start);
        queue.add(start);

        while (!queue.isEmpty()) {
            // Dequeue a vertex from the queue and print it
            char current = queue.poll();
            System.out.print(current + " ");

            // Get all adjacent vertices of the dequeued vertex
            for (char neighbor : graph.get(current)) {
                if (!visited.contains(neighbor)) {
                    visited.add(neighbor);
                    queue.add(neighbor);
                }
            }
        }
    }

    // Example usage
    public static void main(String[] args) {
        // Creating a graph using adjacency list representation
        Map<Character, List<Character>> graph = new HashMap<>();
        graph.put('A', Arrays.asList('B', 'C'));
        graph.put('B', Arrays.asList('A', 'D', 'E'));
        graph.put('C', Arrays.asList('A', 'F'));
        graph.put('D', Arrays.asList('B'));
        graph.put('E', Arrays.asList('B'));
        graph.put('F', Arrays.asList('C'));

        System.out.println("BFS Traversal starting from A:");
        bfs(graph, 'A');
        // Output: A B C D E F 
    }
}
```

**Explanation:**
- **Graph Representation:** Similar to DFS, using an adjacency list.
- **Visited Set:** To keep track of visited nodes.
- **Queue:** Ensures nodes are visited in the order they were discovered.

**Time Complexity:** O(V + E)

**Space Complexity:** O(V) due to the queue and visited set.

**When to Use:**
- Finding the shortest path in unweighted graphs.
- Broadcasting in networks.
- Crawling web pages.

---

### **2. Shortest Path Algorithms**

Shortest Path Algorithms find the shortest path between two nodes in a graph. These algorithms are vital in applications like GPS navigation, network routing, and social network analysis.

#### **2.1 Dijkstra's Algorithm**

**Overview:**
Dijkstra's Algorithm is used to find the shortest path from a single source node to all other nodes in a graph with non-negative edge weights.

**How It Works:**
1. Assign to every node a tentative distance value: set it to zero for the initial node and to infinity for all other nodes.
2. Set the initial node as current.
3. For the current node, consider all its unvisited neighbors and calculate their tentative distances.
4. After considering all neighbors, mark the current node as visited. A visited node will not be checked again.
5. Select the unvisited node with the smallest tentative distance and set it as the new current node.
6. Repeat steps 3-5 until all nodes are visited.

**Example:**
Consider the following weighted graph:

```
    A
   / \
  1   4
 /     \
B-------C
 \     /
  2   1
   \ /
    D
```

**Edge Weights:**
- A-B: 1
- A-C: 4
- B-C: 3
- B-D: 2
- C-D: 1

**Steps:**
1. Start at A: distance A=0, B=1, C=4, D=∞
2. Visit B: update distances B=1, C=1+3=4, D=1+2=3
3. Visit C: update distances D=1+1=2
4. Visit D: all nodes visited.

**Java Implementation:**

```java
import java.util.*;

public class DijkstraAlgorithm {
    // Class to represent a node and its distance
    static class Node implements Comparable<Node> {
        char vertex;
        int distance;

        Node(char vertex, int distance) {
            this.vertex = vertex;
            this.distance = distance;
        }

        // Compare nodes based on distance
        public int compareTo(Node other) {
            return this.distance - other.distance;
        }
    }

    // Function to perform Dijkstra's algorithm
    public static Map<Character, Integer> dijkstra(Map<Character, List<Node>> graph, char start) {
        // Priority queue to select the node with the smallest distance
        PriorityQueue<Node> pq = new PriorityQueue<>();
        // Map to store the shortest distance to each node
        Map<Character, Integer> distances = new HashMap<>();
        // Set to keep track of visited nodes
        Set<Character> visited = new HashSet<>();

        // Initialize distances
        for (char vertex : graph.keySet()) {
            distances.put(vertex, Integer.MAX_VALUE);
        }
        distances.put(start, 0);

        // Add the start node to the priority queue
        pq.add(new Node(start, 0));

        while (!pq.isEmpty()) {
            // Extract the node with the smallest distance
            Node current = pq.poll();
            char currentVertex = current.vertex;

            if (visited.contains(currentVertex))
                continue;

            visited.add(currentVertex);

            // Update distances for neighbors
            for (Node neighbor : graph.get(currentVertex)) {
                if (!visited.contains(neighbor.vertex)) {
                    int newDist = distances.get(currentVertex) + neighbor.distance;
                    if (newDist < distances.get(neighbor.vertex)) {
                        distances.put(neighbor.vertex, newDist);
                        pq.add(new Node(neighbor.vertex, newDist));
                    }
                }
            }
        }

        return distances;
    }

    // Example usage
    public static void main(String[] args) {
        // Creating a graph using adjacency list representation
        Map<Character, List<Node>> graph = new HashMap<>();

        graph.put('A', Arrays.asList(new Node('B', 1), new Node('C', 4)));
        graph.put('B', Arrays.asList(new Node('A', 1), new Node('C', 3), new Node('D', 2)));
        graph.put('C', Arrays.asList(new Node('A', 4), new Node('B', 3), new Node('D', 1)));
        graph.put('D', Arrays.asList(new Node('B', 2), new Node('C', 1)));

        char start = 'A';
        Map<Character, Integer> distances = dijkstra(graph, start);

        System.out.println("Shortest distances from " + start + ":");
        for (char vertex : distances.keySet()) {
            System.out.println(vertex + ": " + distances.get(vertex));
        }
        /*
        Output:
        Shortest distances from A:
        A: 0
        B: 1
        C: 2
        D: 3
        */
    }
}
```

**Explanation:**
- **Graph Representation:** Uses an adjacency list with each neighbor represented as a `Node` containing the vertex and distance.
- **Priority Queue:** Ensures the node with the smallest tentative distance is processed first.
- **Distances Map:** Keeps track of the shortest known distance to each node.
- **Visited Set:** Prevents reprocessing nodes.

**Time Complexity:** O(E + V log V) where V is the number of vertices and E is the number of edges.

**Space Complexity:** O(V + E)

**When to Use:**
- Finding the shortest path in road networks.
- Routing protocols in computer networks.
- GPS navigation systems.

---

#### **2.2 Bellman-Ford Algorithm**

**Overview:**
The Bellman-Ford Algorithm computes the shortest paths from a single source vertex to all other vertices in a weighted graph. Unlike Dijkstra's Algorithm, Bellman-Ford can handle graphs with negative edge weights and detect negative weight cycles.

**How It Works:**
1. Initialize distances from the source to all vertices as infinite and distance to the source itself as zero.
2. Relax all edges V-1 times, where V is the number of vertices.
3. Check for negative-weight cycles by verifying if any distance can be further reduced.

**Example:**
Consider the following graph with a negative edge:

```
    A
   / \
  1  -4
 /     \
B-------C
 \     /
  3   2
   \ /
    D
```

**Edge Weights:**
- A-B: 1
- A-C: -4
- B-C: 3
- B-D: 2
- C-D: 2

**Java Implementation:**

```java
import java.util.*;

public class BellmanFordAlgorithm {
    // Class to represent an edge
    static class Edge {
        char source;
        char destination;
        int weight;

        Edge(char source, char destination, int weight) {
            this.source = source;
            this.destination = destination;
            this.weight = weight;
        }
    }

    // Function to perform Bellman-Ford algorithm
    public static Map<Character, Integer> bellmanFord(List<Edge> edges, char start, Set<Character> vertices) {
        // Initialize distances
        Map<Character, Integer> distances = new HashMap<>();
        for (char vertex : vertices) {
            distances.put(vertex, Integer.MAX_VALUE);
        }
        distances.put(start, 0);

        // Relax edges repeatedly
        int V = vertices.size();
        for (int i = 1; i < V; i++) {
            for (Edge edge : edges) {
                if (distances.get(edge.source) != Integer.MAX_VALUE &&
                    distances.get(edge.source) + edge.weight < distances.get(edge.destination)) {
                    distances.put(edge.destination, distances.get(edge.source) + edge.weight);
                }
            }
        }

        // Check for negative-weight cycles
        for (Edge edge : edges) {
            if (distances.get(edge.source) != Integer.MAX_VALUE &&
                distances.get(edge.source) + edge.weight < distances.get(edge.destination)) {
                System.out.println("Graph contains a negative-weight cycle.");
                return null;
            }
        }

        return distances;
    }

    // Example usage
    public static void main(String[] args) {
        List<Edge> edges = new ArrayList<>();
        edges.add(new Edge('A', 'B', 1));
        edges.add(new Edge('A', 'C', -4));
        edges.add(new Edge('B', 'C', 3));
        edges.add(new Edge('B', 'D', 2));
        edges.add(new Edge('C', 'D', 2));

        Set<Character> vertices = new HashSet<>(Arrays.asList('A', 'B', 'C', 'D'));
        char start = 'A';

        Map<Character, Integer> distances = bellmanFord(edges, start, vertices);

        if (distances != null) {
            System.out.println("Shortest distances from " + start + ":");
            for (char vertex : distances.keySet()) {
                System.out.println(vertex + ": " + distances.get(vertex));
            }
            /*
            Output:
            Shortest distances from A:
            A: 0
            B: 1
            C: -3
            D: -1
            */
        }
    }
}
```

**Explanation:**
- **Edge Class:** Represents each edge with a source, destination, and weight.
- **Distance Initialization:** Sets all distances to infinity except the start node.
- **Relaxation:** Updates the distance to each vertex by checking if a shorter path exists through any edge.
- **Negative Cycle Detection:** After V-1 relaxations, checks if any edge can still reduce the distance, indicating a negative cycle.

**Time Complexity:** O(V * E)

**Space Complexity:** O(V)

**When to Use:**
- Finding shortest paths in graphs with negative weights.
- Detecting negative cycles in financial modeling.

---

#### **2.3 A* Search Algorithm**

**Overview:**
The A* Search Algorithm is an extension of Dijkstra's Algorithm that uses heuristics to improve efficiency by prioritizing nodes that are likely to lead to the goal. It is widely used in pathfinding and graph traversal, especially in game development and GPS navigation.

**How It Works:**
1. **Initialize** the open list with the start node.
2. **Loop** until the open list is empty:
   - Select the node with the lowest `f(n) = g(n) + h(n)` from the open list.
   - If this node is the goal, reconstruct the path and terminate.
   - Otherwise, move it to the closed list and examine its neighbors.
   - For each neighbor, calculate `g(n)` (cost from start) and `h(n)` (heuristic estimate to goal).
   - If the neighbor is in the closed list with a lower `g(n)`, skip it.
   - If not, add/update the neighbor in the open list.
3. **Heuristic Function (`h(n)`):** Estimates the cost from node `n` to the goal. It should be admissible (never overestimates the true cost).

**Example:**
Finding the shortest path from node A to node D using A*.

Assume the heuristic `h(n)` is the straight-line distance to D.

**Java Implementation:**

```java
import java.util.*;

public class AStarSearch {
    // Class to represent a node in the graph
    static class Node implements Comparable<Node> {
        char vertex;
        int g; // Cost from start to this node
        int h; // Heuristic cost to goal
        int f; // Total cost (g + h)
        Node parent;

        Node(char vertex, int g, int h, Node parent) {
            this.vertex = vertex;
            this.g = g;
            this.h = h;
            this.f = g + h;
            this.parent = parent;
        }

        // Compare nodes based on f value
        public int compareTo(Node other) {
            return this.f - other.f;
        }
    }

    // Function to perform A* Search
    public static List<Character> aStar(Map<Character, List<Node>> graph, char start, char goal, Map<Character, Integer> heuristics) {
        PriorityQueue<Node> openList = new PriorityQueue<>();
        Set<Character> closedList = new HashSet<>();

        // Initialize the start node
        openList.add(new Node(start, 0, heuristics.get(start), null));

        while (!openList.isEmpty()) {
            // Get the node with the lowest f value
            Node current = openList.poll();

            if (current.vertex == goal) {
                // Reconstruct the path
                List<Character> path = new ArrayList<>();
                while (current != null) {
                    path.add(current.vertex);
                    current = current.parent;
                }
                Collections.reverse(path);
                return path;
            }

            closedList.add(current.vertex);

            // Explore neighbors
            for (Node neighbor : graph.get(current.vertex)) {
                if (closedList.contains(neighbor.vertex))
                    continue;

                int tentativeG = current.g + neighbor.g; // neighbor.g represents the edge weight

                // Check if neighbor is already in openList with a lower g
                boolean inOpen = false;
                for (Node node : openList) {
                    if (node.vertex == neighbor.vertex && tentativeG >= node.g) {
                        inOpen = true;
                        break;
                    }
                }

                if (!inOpen) {
                    openList.add(new Node(neighbor.vertex, tentativeG, heuristics.get(neighbor.vertex), current));
                }
            }
        }

        // No path found
        return Collections.emptyList();
    }

    // Example usage
    public static void main(String[] args) {
        // Creating a graph using adjacency list representation
        // Each neighbor has a vertex and a cost (edge weight)
        Map<Character, List<Node>> graph = new HashMap<>();
        graph.put('A', Arrays.asList(new Node('B', 1, 0, null), new Node('C', 4, 0, null)));
        graph.put('B', Arrays.asList(new Node('C', 3, 0, null), new Node('D', 2, 0, null)));
        graph.put('C', Arrays.asList(new Node('D', 1, 0, null)));
        graph.put('D', new ArrayList<>());

        // Heuristic function (straight-line distance to D)
        Map<Character, Integer> heuristics = new HashMap<>();
        heuristics.put('A', 7);
        heuristics.put('B', 6);
        heuristics.put('C', 2);
        heuristics.put('D', 0);

        char start = 'A';
        char goal = 'D';

        List<Character> path = aStar(graph, start, goal, heuristics);

        if (!path.isEmpty()) {
            System.out.println("Path found: " + path);
            // Output: Path found: [A, B, D]
        } else {
            System.out.println("No path found from " + start + " to " + goal);
        }
    }
}
```

**Explanation:**
- **Node Class:** Represents each node with its current cost (`g`), heuristic (`h`), total cost (`f`), and a reference to its parent node.
- **Priority Queue:** Orders nodes based on their `f` value to prioritize exploration.
- **Heuristics Map:** Stores the heuristic estimate for each node.
- **Path Reconstruction:** Traces back from the goal node to the start node using parent references.

**Time Complexity:** O(E) where E is the number of edges, but depends on the heuristic's accuracy.

**Space Complexity:** O(V) where V is the number of vertices.

**When to Use:**
- Pathfinding in maps and games.
- Robot motion planning.
- Network routing.

---

### **3. Minimum Spanning Trees**

Minimum Spanning Trees (MST) are subsets of a graph that connect all vertices together without any cycles and with the minimum possible total edge weight. They are useful in designing efficient networks, such as computer, electrical, and transportation networks.

#### **3.1 Kruskal's Algorithm**

**Overview:**
Kruskal's Algorithm builds the MST by adding edges in increasing order of their weight, ensuring that no cycles are formed.

**How It Works:**
1. **Sort** all edges in non-decreasing order of their weight.
2. **Initialize** an empty MST.
3. **Iterate** through the sorted edges and add the edge to the MST if it doesn't form a cycle.
4. **Repeat** until the MST contains (V-1) edges, where V is the number of vertices.

**Example:**
Consider the following graph:

```
    A
   / \
  1   4
 /     \
B-------C
 \     /
  3   2
   \ /
    D
```

**Edge Weights:**
- A-B: 1
- A-C: 4
- B-C: 3
- B-D: 2
- C-D: 2

**Steps:**
1. Sort edges: A-B (1), B-D (2), C-D (2), B-C (3), A-C (4)
2. Add A-B (1) to MST.
3. Add B-D (2) to MST.
4. Add C-D (2) to MST.
5. Skip B-C (3) as it forms a cycle.
6. MST contains A-B, B-D, C-D.

**Java Implementation:**

```java
import java.util.*;

public class KruskalAlgorithm {
    // Class to represent an edge
    static class Edge implements Comparable<Edge> {
        char source;
        char destination;
        int weight;

        Edge(char source, char destination, int weight) {
            this.source = source;
            this.destination = destination;
            this.weight = weight;
        }

        // Compare edges based on their weight
        public int compareTo(Edge other) {
            return this.weight - other.weight;
        }
    }

    // Union-Find structure for cycle detection
    static class UnionFind {
        Map<Character, Character> parent;

        UnionFind(Set<Character> vertices) {
            parent = new HashMap<>();
            for (char vertex : vertices) {
                parent.put(vertex, vertex);
            }
        }

        // Find the root parent of a vertex
        public char find(char vertex) {
            if (parent.get(vertex) != vertex)
                parent.put(vertex, find(parent.get(vertex))); // Path compression
            return parent.get(vertex);
        }

        // Union two sets
        public void union(char vertex1, char vertex2) {
            char root1 = find(vertex1);
            char root2 = find(vertex2);
            if (root1 != root2)
                parent.put(root1, root2);
        }
    }

    // Function to perform Kruskal's algorithm
    public static List<Edge> kruskalMST(List<Edge> edges, Set<Character> vertices) {
        List<Edge> mst = new ArrayList<>();
        Collections.sort(edges); // Sort edges by weight

        UnionFind uf = new UnionFind(vertices);

        for (Edge edge : edges) {
            char root1 = uf.find(edge.source);
            char root2 = uf.find(edge.destination);

            if (root1 != root2) {
                mst.add(edge);
                uf.union(root1, root2);
            }
        }

        return mst;
    }

    // Example usage
    public static void main(String[] args) {
        List<Edge> edges = new ArrayList<>();
        edges.add(new Edge('A', 'B', 1));
        edges.add(new Edge('A', 'C', 4));
        edges.add(new Edge('B', 'C', 3));
        edges.add(new Edge('B', 'D', 2));
        edges.add(new Edge('C', 'D', 2));

        Set<Character> vertices = new HashSet<>(Arrays.asList('A', 'B', 'C', 'D'));

        List<Edge> mst = kruskalMST(edges, vertices);

        System.out.println("Edges in the Minimum Spanning Tree:");
        for (Edge edge : mst) {
            System.out.println(edge.source + " - " + edge.destination + " : " + edge.weight);
        }
        /*
        Output:
        Edges in the Minimum Spanning Tree:
        A - B : 1
        B - D : 2
        C - D : 2
        */
    }
}
```

**Explanation:**
- **Edge Class:** Represents each edge with source, destination, and weight.
- **Union-Find Class:** Helps in detecting cycles by managing disjoint sets.
- **Kruskal's Function:** Sorts edges and adds them to the MST if they don't form a cycle.

**Time Complexity:** O(E log E) due to sorting of edges.

**Space Complexity:** O(V + E)

**When to Use:**
- Designing efficient network layouts.
- Clustering data points.
- Building efficient road networks.

---

#### **3.2 Prim's Algorithm**

**Overview:**
Prim's Algorithm also finds the Minimum Spanning Tree of a graph but starts from a single node and grows the MST by adding the cheapest possible connection from the tree to another vertex.

**How It Works:**
1. **Initialize** a tree with a single vertex, chosen arbitrarily.
2. **Grow** the tree by adding the cheapest edge from the tree to a vertex not yet in the tree.
3. **Repeat** until all vertices are included in the tree.

**Example:**
Using the same graph as in Kruskal's example:

```
    A
   / \
  1   4
 /     \
B-------C
 \     /
  3   2
   \ /
    D
```

**Steps:**
1. Start at A.
2. Choose the smallest edge from A: A-B (1).
3. From A and B, choose the smallest edge: B-D (2).
4. From A, B, D, choose the smallest edge: C-D (2).
5. MST contains A-B, B-D, C-D.

**Java Implementation:**

```java
import java.util.*;

public class PrimAlgorithm {
    // Class to represent an edge
    static class Edge implements Comparable<Edge> {
        char vertex;
        int weight;

        Edge(char vertex, int weight) {
            this.vertex = vertex;
            this.weight = weight;
        }

        // Compare edges based on weight
        public int compareTo(Edge other) {
            return this.weight - other.weight;
        }
    }

    // Function to perform Prim's algorithm
    public static List<String> primMST(Map<Character, List<Edge>> graph, char start) {
        List<String> mst = new ArrayList<>();
        Set<Character> visited = new HashSet<>();
        PriorityQueue<Edge> pq = new PriorityQueue<>();

        // Start from the initial node
        visited.add(start);
        pq.addAll(graph.get(start));

        while (!pq.isEmpty()) {
            Edge current = pq.poll();
            if (!visited.contains(current.vertex)) {
                visited.add(current.vertex);
                mst.add("" + start + " - " + current.vertex + " : " + current.weight);

                // Add all edges from the current vertex to the priority queue
                for (Edge edge : graph.get(current.vertex)) {
                    if (!visited.contains(edge.vertex)) {
                        pq.add(edge);
                    }
                }
            }
        }

        return mst;
    }

    // Example usage
    public static void main(String[] args) {
        // Creating a graph using adjacency list representation
        Map<Character, List<Edge>> graph = new HashMap<>();
        graph.put('A', Arrays.asList(new Edge('B', 1), new Edge('C', 4)));
        graph.put('B', Arrays.asList(new Edge('A', 1), new Edge('C', 3), new Edge('D', 2)));
        graph.put('C', Arrays.asList(new Edge('A', 4), new Edge('B', 3), new Edge('D', 2)));
        graph.put('D', Arrays.asList(new Edge('B', 2), new Edge('C', 2)));

        char start = 'A';
        List<String> mst = primMST(graph, start);

        System.out.println("Edges in the Minimum Spanning Tree using Prim's Algorithm:");
        for (String edge : mst) {
            System.out.println(edge);
        }
        /*
        Output:
        Edges in the Minimum Spanning Tree using Prim's Algorithm:
        A - B : 1
        B - D : 2
        D - C : 2
        */
    }
}
```

**Explanation:**
- **Edge Class:** Represents each edge with the connected vertex and weight.
- **Priority Queue:** Selects the edge with the smallest weight.
- **Visited Set:** Tracks nodes already included in the MST.
- **MST List:** Stores the edges included in the MST.

**Time Complexity:** O(E log V) where V is the number of vertices and E is the number of edges.

**Space Complexity:** O(V + E)

**When to Use:**
- Designing least-cost network connections.
- Clustering data.
- Creating efficient road and transportation systems.

---

## **Week 2: Advanced Graph Algorithms and Network Flow Algorithms**

### **4. Advanced Graph Algorithms**

Advanced Graph Algorithms solve more complex problems related to graph structures, such as determining the order of tasks, identifying strongly connected components, and finding optimal pairings in bipartite graphs.

#### **4.1 Topological Sorting**

**Overview:**
Topological Sorting orders the vertices of a Directed Acyclic Graph (DAG) such that for every directed edge u → v, vertex u comes before vertex v in the ordering. It is useful in scheduling tasks, resolving dependencies, and organizing data.

**How It Works:**
1. **Identify** vertices with no incoming edges.
2. **Remove** these vertices and their outgoing edges from the graph.
3. **Add** the removed vertices to the topological order.
4. **Repeat** until all vertices are processed.

**Example:**
Consider the following tasks with dependencies:

```
Task 5 -> Task 2
Task 5 -> Task 0
Task 4 -> Task 0
Task 4 -> Task 1
Task 2 -> Task 3
Task 3 -> Task 1
```

**Topological Order:** 5, 4, 2, 3, 1, 0

**Java Implementation:**

```java
import java.util.*;

public class TopologicalSort {
    // Function to perform Topological Sort using DFS
    public static List<Character> topologicalSort(Map<Character, List<Character>> graph, Set<Character> vertices) {
        Set<Character> visited = new HashSet<>();
        Deque<Character> stack = new ArrayDeque<>();

        for (char vertex : vertices) {
            if (!visited.contains(vertex)) {
                topologicalSortUtil(vertex, visited, stack, graph);
            }
        }

        List<Character> order = new ArrayList<>();
        while (!stack.isEmpty()) {
            order.add(stack.pop());
        }
        return order;
    }

    // Utility function for DFS
    private static void topologicalSortUtil(char vertex, Set<Character> visited, Deque<Character> stack, Map<Character, List<Character>> graph) {
        visited.add(vertex);

        for (char neighbor : graph.get(vertex)) {
            if (!visited.contains(neighbor)) {
                topologicalSortUtil(neighbor, visited, stack, graph);
            }
        }

        stack.push(vertex);
    }

    // Example usage
    public static void main(String[] args) {
        // Creating a DAG using adjacency list representation
        Map<Character, List<Character>> graph = new HashMap<>();
        graph.put('5', Arrays.asList('2', '0'));
        graph.put('4', Arrays.asList('0', '1'));
        graph.put('2', Arrays.asList('3'));
        graph.put('3', Arrays.asList('1'));
        graph.put('1', new ArrayList<>());
        graph.put('0', new ArrayList<>());

        Set<Character> vertices = new HashSet<>(Arrays.asList('5', '4', '2', '3', '1', '0'));

        List<Character> order = topologicalSort(graph, vertices);
        System.out.println("Topological Order:");
        System.out.println(order);
        // Output: [5, 4, 2, 3, 1, 0]
    }
}
```

**Explanation:**
- **Graph Representation:** Uses an adjacency list for a Directed Acyclic Graph.
- **Visited Set:** Tracks visited nodes to prevent revisiting.
- **Stack:** Stores the order of nodes based on completion of DFS.

**Time Complexity:** O(V + E)

**Space Complexity:** O(V)

**When to Use:**
- Task scheduling with dependencies.
- Resolving symbol dependencies in linkers.
- Organizing build systems.

---

#### **4.2 Strongly Connected Components (Kosaraju's Algorithm)**

**Overview:**
Strongly Connected Components (SCCs) in a directed graph are subsets of vertices where every vertex is reachable from every other vertex in the same subset. Kosaraju's Algorithm efficiently finds all SCCs in a graph.

**How It Works:**
1. **Perform DFS** on the original graph, keeping track of the order in which nodes finish.
2. **Reverse** the graph by reversing all the edges.
3. **Perform DFS** on the reversed graph in the order obtained from step 1.
4. **Each DFS** in step 3 identifies an SCC.

**Example:**
Consider the following directed graph:

```
A -> B
B -> C
C -> A
B -> D
D -> E
E -> F
F -> D
G -> F
G -> H
H -> G
```

**SCCs:**
- [A, B, C]
- [D, E, F]
- [G, H]

**Java Implementation:**

```java
import java.util.*;

public class KosarajuAlgorithm {
    // Function to perform DFS and fill stack
    private static void fillOrder(char vertex, Set<Character> visited, Deque<Character> stack, Map<Character, List<Character>> graph) {
        visited.add(vertex);
        for (char neighbor : graph.get(vertex)) {
            if (!visited.contains(neighbor)) {
                fillOrder(neighbor, visited, stack, graph);
            }
        }
        stack.push(vertex);
    }

    // Function to reverse the graph
    private static Map<Character, List<Character>> reverseGraph(Map<Character, List<Character>> graph, Set<Character> vertices) {
        Map<Character, List<Character>> reversed = new HashMap<>();
        for (char vertex : vertices) {
            reversed.put(vertex, new ArrayList<>());
        }
        for (char vertex : graph.keySet()) {
            for (char neighbor : graph.get(vertex)) {
                reversed.get(neighbor).add(vertex);
            }
        }
        return reversed;
    }

    // Function to perform DFS on reversed graph and collect SCC
    private static void dfs(char vertex, Set<Character> visited, List<Character> component, Map<Character, List<Character>> graph) {
        visited.add(vertex);
        component.add(vertex);
        for (char neighbor : graph.get(vertex)) {
            if (!visited.contains(neighbor)) {
                dfs(neighbor, visited, component, graph);
            }
        }
    }

    // Function to find all SCCs using Kosaraju's Algorithm
    public static List<List<Character>> findSCCs(Map<Character, List<Character>> graph, Set<Character> vertices) {
        Deque<Character> stack = new ArrayDeque<>();
        Set<Character> visited = new HashSet<>();

        // Step 1: Fill vertices in stack according to their finishing times
        for (char vertex : vertices) {
            if (!visited.contains(vertex)) {
                fillOrder(vertex, visited, stack, graph);
            }
        }

        // Step 2: Reverse the graph
        Map<Character, List<Character>> reversedGraph = reverseGraph(graph, vertices);

        // Step 3: Perform DFS on reversed graph
        visited.clear();
        List<List<Character>> sccs = new ArrayList<>();

        while (!stack.isEmpty()) {
            char vertex = stack.pop();
            if (!visited.contains(vertex)) {
                List<Character> component = new ArrayList<>();
                dfs(vertex, visited, component, reversedGraph);
                sccs.add(component);
            }
        }

        return sccs;
    }

    // Example usage
    public static void main(String[] args) {
        // Creating a directed graph using adjacency list representation
        Map<Character, List<Character>> graph = new HashMap<>();
        graph.put('A', Arrays.asList('B'));
        graph.put('B', Arrays.asList('C', 'D'));
        graph.put('C', Arrays.asList('A'));
        graph.put('D', Arrays.asList('E'));
        graph.put('E', Arrays.asList('F'));
        graph.put('F', Arrays.asList('D'));
        graph.put('G', Arrays.asList('F', 'H'));
        graph.put('H', Arrays.asList('G'));

        Set<Character> vertices = new HashSet<>(Arrays.asList('A', 'B', 'C', 'D', 'E', 'F', 'G', 'H'));

        List<List<Character>> sccs = findSCCs(graph, vertices);

        System.out.println("Strongly Connected Components:");
        for (List<Character> component : sccs) {
            System.out.println(component);
        }
        /*
        Output:
        Strongly Connected Components:
        [A, C, B]
        [D, F, E]
        [G, H]
        */
    }
}
```

**Explanation:**
- **Graph Representation:** Directed graph using an adjacency list.
- **fillOrder Function:** Performs DFS and records the order of completion.
- **reverseGraph Function:** Reverses all edges in the graph.
- **dfs Function:** Identifies all nodes in an SCC.
- **findSCCs Function:** Combines all steps to find all SCCs.

**Time Complexity:** O(V + E)

**Space Complexity:** O(V + E)

**When to Use:**
- Analyzing social networks.
- Compiler optimization.
- Detecting cycles in directed graphs.

---

#### **4.3 Bipartite Graphs and Matching (Hopcroft-Karp Algorithm)**

**Overview:**
A Bipartite Graph is a graph whose vertices can be divided into two disjoint sets such that every edge connects a vertex from one set to the other. Matching in bipartite graphs involves pairing vertices from different sets such that no two pairs share a vertex. The Hopcroft-Karp Algorithm efficiently finds the maximum matching in bipartite graphs.

**How It Works:**
1. **Initialize** all matches as unpaired.
2. **Repeatedly find** all shortest augmenting paths using BFS.
3. **Augment** the matching along these paths using DFS.
4. **Repeat** until no more augmenting paths are found.

**Example:**
Consider a bipartite graph with sets U = {A, B, C} and V = {1, 2, 3} with edges:

- A-1, A-2
- B-1
- C-2, C-3

**Maximum Matching:** A-1, C-2

**Java Implementation:**

Implementing the Hopcroft-Karp Algorithm is complex for beginners. Below is a simplified version focusing on understanding the concept.

```java
import java.util.*;

public class HopcroftKarp {
    private final int INF = Integer.MAX_VALUE;
    private int U, V;
    private List<List<Integer>> adj;
    private int[] pairU, pairV, dist;

    public HopcroftKarp(int U, int V) {
        this.U = U;
        this.V = V;
        adj = new ArrayList<>();
        for (int i = 0; i < U; i++)
            adj.add(new ArrayList<>());
    }

    // Add edge from u to v
    public void addEdge(int u, int v) {
        adj.get(u).add(v);
    }

    // BFS to build layers
    private boolean bfs() {
        Queue<Integer> queue = new LinkedList<>();
        dist = new int[U];
        Arrays.fill(dist, INF);

        for (int u = 0; u < U; u++) {
            if (pairU[u] == -1) {
                dist[u] = 0;
                queue.add(u);
            }
        }

        boolean foundAugmentingPath = false;

        while (!queue.isEmpty()) {
            int u = queue.poll();
            for (int v : adj.get(u)) {
                if (pairV[v] != -1 && dist[pairV[v]] == INF) {
                    dist[pairV[v]] = dist[u] + 1;
                    queue.add(pairV[v]);
                }
                else if (pairV[v] == -1) {
                    foundAugmentingPath = true;
                }
            }
        }

        return foundAugmentingPath;
    }

    // DFS to find augmenting paths
    private boolean dfs(int u) {
        for (int v : adj.get(u)) {
            if (pairV[v] == -1 || (dist[pairV[v]] == dist[u] + 1 && dfs(pairV[v]))) {
                pairU[u] = v;
                pairV[v] = u;
                return true;
            }
        }
        dist[u] = INF;
        return false;
    }

    // Function to find maximum matching
    public int maxMatching() {
        pairU = new int[U];
        pairV = new int[V];
        Arrays.fill(pairU, -1);
        Arrays.fill(pairV, -1);

        int result = 0;

        while (bfs()) {
            for (int u = 0; u < U; u++) {
                if (pairU[u] == -1) {
                    if (dfs(u))
                        result++;
                }
            }
        }

        return result;
    }

    // Example usage
    public static void main(String[] args) {
        // Bipartite graph with U = {0,1,2} and V = {0,1,2}
        HopcroftKarp hk = new HopcroftKarp(3, 3);
        // Adding edges (U -> V)
        hk.addEdge(0, 0); // A-1
        hk.addEdge(0, 1); // A-2
        hk.addEdge(1, 0); // B-1
        hk.addEdge(2, 1); // C-2
        hk.addEdge(2, 2); // C-3

        int maxMatch = hk.maxMatching();
        System.out.println("Maximum Matching Size: " + maxMatch);
        // Output: Maximum Matching Size: 2
    }
}
```

**Explanation:**
- **Graph Representation:** Bipartite graph divided into two sets U and V.
- **Pair Arrays:** `pairU` and `pairV` store the matching pairs.
- **BFS and DFS:** Used to find augmenting paths and increase the matching size.
- **Max Matching:** The total number of matched pairs.

**Time Complexity:** O(√V * E)

**Space Complexity:** O(V + E)

**When to Use:**
- Job assignments where workers are matched to tasks.
- Matching students to projects.
- Network connectivity and resource allocation.

---

### **5. Network Flow Algorithms**

Network Flow Algorithms deal with finding the optimal way to send flow through a network. These algorithms are fundamental in fields like transportation, telecommunications, and logistics.

#### **5.1 Ford-Fulkerson Method**

**Overview:**
The Ford-Fulkerson Method computes the maximum flow in a flow network. It works by finding augmenting paths and increasing the flow until no more augmenting paths can be found.

**How It Works:**
1. **Initialize** all flows to zero.
2. **While** there exists an augmenting path from the source to the sink:
   - Find the minimum residual capacity along the path.
   - **Augment** the flow along the path by this minimum capacity.
3. **Repeat** until no augmenting paths remain.

**Example:**
Consider the following flow network:

```
    Source (S)
    /      \
   10       10
  /          \
A-----10-----B
  \          /
   10       10
    \      /
    Sink (T)
```

**Java Implementation:**

```java
import java.util.*;

public class FordFulkerson {
    static final int V = 6; // Number of vertices

    // Function to find if there is a path from source to sink using BFS
    private boolean bfs(int[][] residualGraph, int s, int t, int[] parent) {
        boolean[] visited = new boolean[V];
        Queue<Integer> queue = new LinkedList<>();
        queue.add(s);
        visited[s] = true;
        parent[s] = -1;

        while (!queue.isEmpty()) {
            int u = queue.poll();
            for (int v = 0; v < V; v++) {
                if (!visited[v] && residualGraph[u][v] > 0) {
                    queue.add(v);
                    parent[v] = u;
                    visited[v] = true;
                }
            }
        }

        return visited[t];
    }

    // Function to implement Ford-Fulkerson algorithm
    public int fordFulkerson(int[][] graph, int s, int t) {
        int u, v;

        // Create residual graph and fill it with original capacities
        int[][] residualGraph = new int[V][V];
        for (u = 0; u < V; u++)
            for (v = 0; v < V; v++)
                residualGraph[u][v] = graph[u][v];

        // Array to store the path
        int[] parent = new int[V];

        int maxFlow = 0; // Initialize max flow

        // Augment the flow while there is a path from source to sink
        while (bfs(residualGraph, s, t, parent)) {
            // Find the minimum residual capacity of the edges along the path filled by BFS
            int pathFlow = Integer.MAX_VALUE;
            for (v = t; v != s; v = parent[v]) {
                u = parent[v];
                pathFlow = Math.min(pathFlow, residualGraph[u][v]);
            }

            // Update residual capacities of the edges and reverse edges
            for (v = t; v != s; v = parent[v]) {
                u = parent[v];
                residualGraph[u][v] -= pathFlow;
                residualGraph[v][u] += pathFlow;
            }

            // Add path flow to overall flow
            maxFlow += pathFlow;
        }

        return maxFlow;
    }

    // Example usage
    public static void main(String[] args) {
        FordFulkerson ff = new FordFulkerson();

        // Example graph
        // Index 0: Source (S)
        // Index 1: A
        // Index 2: B
        // Index 3: C
        // Index 4: D
        // Index 5: Sink (T)

        int[][] graph = new int[V][V];

        // Adding edges and their capacities
        graph[0][1] = 10; // S -> A
        graph[0][2] = 10; // S -> B
        graph[1][3] = 10; // A -> C
        graph[2][3] = 10; // B -> C
        graph[3][4] = 10; // C -> D
        graph[4][5] = 10; // D -> T

        int s = 0; // Source
        int t = 5; // Sink

        System.out.println("The maximum possible flow is " + ff.fordFulkerson(graph, s, t));
        // Output: The maximum possible flow is 20
    }
}
```

**Explanation:**
- **Graph Representation:** Uses an adjacency matrix to represent capacities.
- **Residual Graph:** Represents the remaining capacities after each augmentation.
- **BFS Function:** Finds if there's a path from source to sink and records the path.
- **Flow Augmentation:** Updates the residual capacities based on the found path.

**Time Complexity:** O(E * max_flow)

**Space Complexity:** O(V^2)

**When to Use:**
- Network traffic optimization.
- Bipartite matching.
- Project selection.

---

#### **5.2 Edmonds-Karp Algorithm**

**Overview:**
The Edmonds-Karp Algorithm is an implementation of the Ford-Fulkerson Method that uses Breadth-First Search (BFS) to find the shortest augmenting paths. It guarantees a time complexity of O(VE^2) and is widely used for its efficiency and simplicity.

**How It Works:**
1. **Initialize** all flows to zero.
2. **While** there exists a shortest augmenting path from the source to the sink:
   - Find the minimum residual capacity along this path.
   - **Augment** the flow along the path by this minimum capacity.
3. **Repeat** until no more augmenting paths are found.

**Example:**
Using the same graph as in the Ford-Fulkerson example:

```
    Source (S)
    /      \
   10       10
  /          \
A-----10-----B
  \          /
   10       10
    \      /
    Sink (T)
```

**Java Implementation:**

The Edmonds-Karp Algorithm is essentially the Ford-Fulkerson Method with BFS for finding augmenting paths. Here's the implementation:

```java
import java.util.*;

public class EdmondsKarp {
    static final int V = 6; // Number of vertices

    // Function to perform BFS and find path using parent array
    private boolean bfs(int[][] residualGraph, int s, int t, int[] parent) {
        boolean[] visited = new boolean[V];
        Queue<Integer> queue = new LinkedList<>();
        queue.add(s);
        visited[s] = true;
        parent[s] = -1;

        while (!queue.isEmpty()) {
            int u = queue.poll();
            for (int v = 0; v < V; v++) {
                if (!visited[v] && residualGraph[u][v] > 0) {
                    queue.add(v);
                    parent[v] = u;
                    visited[v] = true;
                }
            }
        }

        return visited[t];
    }

    // Function to implement Edmonds-Karp algorithm
    public int edmondsKarp(int[][] graph, int s, int t) {
        int u, v;

        // Create residual graph and fill it with original capacities
        int[][] residualGraph = new int[V][V];
        for (u = 0; u < V; u++)
            for (v = 0; v < V; v++)
                residualGraph[u][v] = graph[u][v];

        int[] parent = new int[V];
        int maxFlow = 0;

        // Augment the flow while there is a path from source to sink
        while (bfs(residualGraph, s, t, parent)) {
            // Find the minimum residual capacity of the edges along the path filled by BFS
            int pathFlow = Integer.MAX_VALUE;
            for (v = t; v != s; v = parent[v]) {
                u = parent[v];
                pathFlow = Math.min(pathFlow, residualGraph[u][v]);
            }

            // Update residual capacities of the edges and reverse edges
            for (v = t; v != s; v = parent[v]) {
                u = parent[v];
                residualGraph[u][v] -= pathFlow;
                residualGraph[v][u] += pathFlow;
            }

            // Add path flow to overall flow
            maxFlow += pathFlow;
        }

        return maxFlow;
    }

    // Example usage
    public static void main(String[] args) {
        EdmondsKarp ek = new EdmondsKarp();

        // Example graph
        // Index 0: Source (S)
        // Index 1: A
        // Index 2: B
        // Index 3: C
        // Index 4: D
        // Index 5: Sink (T)

        int[][] graph = new int[V][V];

        // Adding edges and their capacities
        graph[0][1] = 10; // S -> A
        graph[0][2] = 10; // S -> B
        graph[1][3] = 10; // A -> C
        graph[2][3] = 10; // B -> C
        graph[3][4] = 10; // C -> D
        graph[4][5] = 10; // D -> T

        int s = 0; // Source
        int t = 5; // Sink

        System.out.println("The maximum possible flow using Edmonds-Karp is " + ek.edmondsKarp(graph, s, t));
        // Output: The maximum possible flow using Edmonds-Karp is 20
    }
}
```

**Explanation:**
- **Residual Graph:** Represents remaining capacities after each augmentation.
- **BFS Function:** Finds the shortest augmenting path.
- **Flow Augmentation:** Updates the residual capacities based on the found path.
- **Max Flow:** Accumulates the total flow from source to sink.

**Time Complexity:** O(V * E^2)

**Space Complexity:** O(V + E)

**When to Use:**
- Network routing.
- Bipartite matching.
- Project selection and resource allocation.

---

## **Summary and Exercises**

### **Summary:**
In this module, you have explored a variety of Graph Algorithms that are fundamental for solving complex problems involving networks and connections:

- **Graph Traversal Algorithms:** Learned how to navigate graphs using Depth-First Search (DFS) and Breadth-First Search (BFS).
  
- **Shortest Path Algorithms:** Understood how to find the shortest paths in graphs using Dijkstra's Algorithm, Bellman-Ford Algorithm, and A* Search Algorithm.
  
- **Minimum Spanning Trees:** Discovered how to connect all vertices in a graph with the minimum total edge weight using Kruskal's and Prim's Algorithms.
  
- **Advanced Graph Algorithms:** Delved into Topological Sorting for ordering tasks, identifying Strongly Connected Components with Kosaraju's Algorithm, and finding maximum matchings in Bipartite Graphs using the Hopcroft-Karp Algorithm.
  
- **Network Flow Algorithms:** Explored methods to determine the optimal flow through networks using the Ford-Fulkerson Method and the Edmonds-Karp Algorithm.

### **Exercises:**

1. **Graph Traversal:**
   - **DFS Implementation:**
     - Modify the DFS implementation to detect cycles in an undirected graph.
     - Implement iterative DFS using a stack instead of recursion.
   - **BFS Implementation:**
     - Use BFS to find the shortest path between two nodes in an unweighted graph.
     - Implement BFS to detect if a graph is bipartite.

2. **Shortest Path Algorithms:**
   - **Dijkstra's Algorithm:**
     - Extend Dijkstra's implementation to also return the actual path taken from the source to each node.
     - Compare the performance of Dijkstra's Algorithm with Bellman-Ford on a graph with both positive and negative edge weights.
   - **Bellman-Ford Algorithm:**
     - Implement the Bellman-Ford Algorithm to detect negative cycles in a graph.
   - **A* Search Algorithm:**
     - Modify the A* implementation to handle 2D grid-based pathfinding, such as finding a path in a maze.
     - Experiment with different heuristic functions and observe their impact on performance.

3. **Minimum Spanning Trees:**
   - **Kruskal's Algorithm:**
     - Implement Kruskal's Algorithm for a larger graph and visualize the MST.
     - Compare Kruskal's and Prim's Algorithms in terms of execution time and memory usage.
   - **Prim's Algorithm:**
     - Modify Prim's implementation to handle graphs represented with adjacency matrices instead of adjacency lists.

4. **Advanced Graph Algorithms:**
   - **Topological Sorting:**
     - Implement Topological Sorting using Kahn's Algorithm (BFS-based) and compare it with the DFS-based approach.
     - Detect cycles in a graph using Topological Sorting; explain why Topological Sorting is only possible for DAGs.
   - **Strongly Connected Components:**
     - Implement Kosaraju's Algorithm on a graph with multiple SCCs and verify the correctness of the output.
   - **Bipartite Graphs and Matching:**
     - Use the Hopcroft-Karp Algorithm to find the maximum matching in a real-world scenario, such as job assignments.

5. **Network Flow Algorithms:**
   - **Ford-Fulkerson Method:**
     - Implement the Ford-Fulkerson Method on a graph with multiple sources and sinks by adding a super source and super sink.
   - **Edmonds-Karp Algorithm:**
     - Compare the performance of the Edmonds-Karp Algorithm with a basic Ford-Fulkerson implementation on large graphs.
     - Apply the Edmonds-Karp Algorithm to solve real-world problems like traffic flow optimization.

6. **Combined Techniques:**
   - **Pathfinding with Constraints:**
     - Implement a program that finds the shortest path in a graph with constraints, such as avoiding certain nodes or edges.
   - **Optimizing Network Designs:**
     - Use Minimum Spanning Trees to design a network layout for a set of cities with varying connection costs, ensuring minimal total cost.

### **Further Reading and Resources:**

- **Books:**
  - *Introduction to Algorithms* by Cormen, Leiserson, Rivest, and Stein.
  - *Algorithms* by Robert Sedgewick and Kevin Wayne.
  - *Graph Algorithms* by Shimon Even.

- **Online Tutorials:**
  - [GeeksforGeeks Graph Algorithms](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)
  - [Khan Academy - Graph Theory](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/graph-representation)
  - [VisuAlgo](https://visualgo.net/en) for visualizing graph algorithms.

- **Video Lectures:**
  - [MIT OpenCourseWare - Advanced Graph Algorithms](https://ocw.mit.edu/courses/6-854j-advanced-algorithm-design-and-analysis-fall-2005/)
  - [Stanford University - CS 161: Design and Analysis of Algorithms](https://www.youtube.com/playlist?list=PLoROMvodv4rO1NB9TD4iUZ3qghGEGtqNX)
  - [Harvard's CS50 on YouTube](https://www.youtube.com/user/cs50tv)

- **Interactive Platforms:**
  - [Algorithm Visualizer](https://algorithm-visualizer.org/) for step-by-step execution of graph algorithms.
  - [LeetCode](https://leetcode.com/) and [HackerRank](https://www.hackerrank.com/domains/algorithms/graph) for practicing graph algorithm problems.
  - [GraphOnline](https://graphonline.ru/en/) for creating and visualizing graphs and running algorithms on them.

---

By completing this module on Graph Algorithms, you have gained a comprehensive understanding of how to navigate, analyze, and optimize complex networks. These skills are invaluable not only for technical interviews but also for real-world applications in software development, data analysis, and network design. Continue practicing these algorithms through the exercises and utilize the provided resources to deepen your mastery.
