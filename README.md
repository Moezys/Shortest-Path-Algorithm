Shortest Path Finder
A Python implementation of a single-source shortest-path algorithm (similar to Dijkstra’s approach) that computes minimum distances and corresponding paths from a given start node to every other node in a weighted graph. This script also allows optional printing of the shortest path to a specific target node.

Overview
The shortest_path function takes:

graph: A Python dictionary where each key is a node name (string, integer, etc.), and each value is a list of tuples. Each tuple is (neighbor_node, edge_weight) representing a directed edge from the key node to neighbor_node with the given nonnegative weight.

start: The node from which we compute shortest distances to all other nodes.

(Optional) target: If provided, the function prints only the shortest path from start to this target node; otherwise, it prints all shortest paths from start to every other node.

The function returns two dictionaries:

distances: Maps every node to its shortest distance (a number) from start.

paths: Maps each node to a list representing the sequence of nodes along the shortest path from start to that node.


Graph Representation
In this implementation, the input graph is assumed to be directed and weighted. For example:

graph = {
    'A': [('B', 4), ('C', 2)],
    'B': [('C', 3), ('D', 2), ('E', 3)],
    'C': [('B', 1), ('D', 4), ('E', 5)],
    'D': [('E', 1)],
    'E': []
}
'A': [('B', 4), ('C', 2)] means:

There is an edge A → B with weight 4,

An edge A → C with weight 2.

Node 'E' has an empty list because it has no outgoing edges.

All node names (keys) in graph must appear in the dictionary. Even if a node is only a neighbor and has no outgoing edges, it must still be included as a key, mapping to an empty list.

How It Works
Initialization

unvisited is a list of all nodes (keys) in the graph.

distances is a dictionary that sets distances[start] = 0 and distance[node] = ∞ for all other nodes.

paths is a dictionary where each key maps to an empty list, except for paths[start] = [start].

Main Loop (Visiting Nodes)

While there are unvisited nodes:

Select the “current” node with the smallest tentative distance using min(unvisited, key=distances.get).

For each outgoing edge (neighbor, weight) from current, compute new_dist = distances[current] + weight.

If new_dist < distances[neighbor], update:

distances[neighbor] = new_dist

paths[neighbor] = paths[current] + [neighbor] (copy the path to current and append neighbor)

Remove current from unvisited (mark it visited).

Printing/Returning Results

If a target node is provided, only that node’s distance and path are printed (unless it is the same as start).

If no target is given, the function iterates over all nodes in graph (except start) and prints each distance and path.

Finally, the function returns the full distances and paths dictionaries for your own programmatic use.

Because we always pick the smallest-distance unvisited node at each step, this algorithm guarantees correct shortest paths for graphs with nonnegative weights (no negative edges).

Requirements
Python 3.6+

No external dependencies—only uses built-in modules (print, basic built-ins).

License
This code is released under the MIT License. Feel free to use, modify, and distribute it, provided you keep this license notice intact.

Thank you for using this shortest-path implementation! If you have any improvements or encounter issues, please open an issue or submit a pull request.