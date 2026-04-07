# Delivery-Route-Optimization-Shortest-Path-Problem-

Definition of the problem: 
Delivery Route Optimization (Shortest Path Problem)
In modern logistics and transportation, finding the most efficient route between locations is crucial for saving fuel, time, and resources. The problem we are addressing is the Delivery Route Optimization problem, computationally known as the Single-Source Shortest Path problem. Given a complex network of delivery points (represented as nodes) and the distances between them (represented as edges), the goal is to find the shortest possible path from a starting warehouse to all other delivery destinations.
To solve this routing problem, we will implement two algorithms belonging to different design paradigms. The first is Dijkstra’s Algorithm, a Greedy approach that iteratively selects the closest unvisited delivery node to build the shortest path tree. The second is the Bellman-Ford Algorithm, which utilizes Dynamic Programming by repeatedly relaxing all paths to guarantee the shortest route, even in theoretical scenarios where network costs fluctuate deeply.
We will assess the performance of both algorithms on a large-scale routing dataset. While Dijkstra's algorithm is expected to be faster for standard maps, comparing it against Bellman-Ford will allow us to analyze the trade-offs between Greedy speed and Dynamic Programming's robust edge-case handling.

Algorithm 1 — Dijkstra’s Algorithm (Greedy))
This algorithm helps solve the problem by iteratively selecting the closest unvisited delivery node. It builds a shortest-path tree outward from the source node, confidently locking in the shortest distance to each location one by one. It is highly efficient for standard road networks where all distances (edge weights) are positive.
Algorithm 2: Bellman-Ford Algorithm (Dynamic Programming):
This algorithm solves the problem by over-estimating the distances at first, and then repeatedly "relaxing" all the paths in the graph to find better routes. By remembering and updating these optimal sub-routes, it guarantees the absolute shortest path. While generally slower than Dijkstra's, it is incredibly robust and can handle edge cases like negative weight cycles (which could represent a scenario where traveling a certain route yields a massive resource credit).
Pseudocode of the selected algorithms:
Algorithm 1: Dijkstra’s Algorithm (Greedy) 
FUNCTION Dijkstra(Graph, source):
    // Initialize distances to all nodes as infinity, and source to 0
    FOR EACH node v IN Graph:
        distance[v] = INFINITY
        previous[v] = NULL
    END FOR
    distance[source] = 0
    // Create a set of all unvisited nodes
    Create unvisitedSet containing all nodes in Graph
    WHILE unvisitedSet is NOT empty:
        // Greedily pick the unvisited node with the smallest known distance
        u = node in unvisitedSet with minimum distance[u]
        REMOVE u FROM unvisitedSet
        // Explore all adjacent neighbors of u
        FOR EACH neighbor v OF u:
            IF v is IN unvisitedSet:
                // Calculate the distance to v through u
                alt_distance = distance[u] + weight(u, v)
                // If this new path is strictly shorter, update the distance
                IF alt_distance < distance[v]:
                    distance[v] = alt_distance
                    previous[v] = u
                END IF
            END IF
        END FOR
    END WHILE
    RETURN distance, previous





Algorithm 2: Bellman-Ford Algorithm (Dynamic Programming) 
FUNCTION BellmanFord(Graph, source):
    // Initialize distances to all nodes as infinity, and source to 0
    FOR EACH node v IN Graph:
        distance[v] = INFINITY
        previous[v] = NULL
    END FOR
    distance[source] = 0
    V = number of vertices in Graph
    // Step 1: Relax all edges (V - 1) times 
    FOR i FROM 1 TO V - 1:
        FOR EACH edge (u, v) IN Graph:
            alt_distance = distance[u] + weight(u, v)
            // If a shorter path is found, update it
            IF distance[u] != INFINITY AND alt_distance < distance[v]:
                distance[v] = alt_distance
                previous[v] = u
            END IF
        END FOR
    END FOR
    // Step 2: Check for negative-weight cycles
    // If we can still find a shorter path, a negative cycle exists
    FOR EACH edge (u, v) IN Graph:
        IF distance[u] != INFINITY AND distance[u] + weight(u, v) < distance[v]:
            PRINT "Error: Graph contains a negative-weight cycle"
            RETURN NULL
        END IF
    END FOR
    RETURN distance, previous
