<extoc></extoc>

# Graph

## Representation

**Graph** can be represented using **Adjacency Matrix**, **Adjacency List** and **hash table**.

Following is an example undirected graph with 5 vertices.

![Graph](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/undirectedgraph.png)

![Adjacency Matrix](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacencymatrix.png)

![Adjecency List](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/listadjacency.png)

__Adjacency Matrix vs. Adjacency Lists__

- Adjacency Matrix
    - Time: Edge removal $$O(1)$$, Query of Edge $$O(1)$$
    - Space: $$O(V^2)$$
- Adjacency List
    - Time: Query of Edge $$O(V)$$
    - Space: $$O(V + E)$$


## Graph Search Algorithms

__Draw the Search Graph of Problems__

- What does it store on each level?
- How many different states should we try to put on each level?

__Tip__

- Checking existed and Writing existed nodes should be put at the same place.

### Generic Tree Search Algorithm (BFS and DFS)

Reference - [USC-CSCI561-Lecture-Week2]

__Three points__

- Initial state
- Expansion/generation rule
- Termination condition

```c
function TreeSearch(problem) return a solution or failure

frontier <- makeQueue(makeNodes(problem.INITIAL_STATE))
loop do
    if isEmpty(frontiers) then return failure
    node <- removeFirst(frontiers)
    if goalTest() applied to node.state succeeds
        then return solution(node)
    frontiers <- insertAll(EXPAND(node, problem))
```

__Expand Function__

```python
// @Return: a set of nodes
def expand(node, problem):
    successors = set([])
    for (action, result) in problem.get_successors(node.state):
        s = node(empty)
        s.state = result
        s.parent_node = node
        s.action = action
        s.path_cost = node.path_cost + get_step_cost(node, action, s)
        s.depth = node.depth + 1
        successors.add(s)
    return successors

```


__Note:__

- Always remove elements from the front
- BFS places new elements at the end of the queue. FIFO.
- DFS places new elements at the front of the queue(stack). LILO.


## Check if there exists a loop

### in a Directed Graph

1. DFS and check if there is duplicate explored node in one path

2. Topological Sorting

**Idea** 

- A circle does not have any nodes with zero in-degree, while other graphs always do.
- So we keep removing nodes with zero in-degrees from the graph and see if there are nodes left.

**Steps**

- construct edge map (out) and in-degree map
- remove nodes with zero indegree
- keep removing
- if there are nodes left, there exists loops.

### in a Undirected Graph

1. Union-find (Disjoint Set)

[Princeton Slide](https://www.cs.princeton.edu/~rs/AlgsDS07/01UnionFind.pdf)

A disjoint-set data structure is a data structure that keeps track of the belongings of nodes.

- Each node has one pointer
- The root has empty pointer
- Each subset only have one root

```
1 -> 2 -> 3
5 -> 2
4 -> 3
```

- Operations
    - ```find``` O(n)
        - Eg. ```find(1) = 3```, ```find(4) = 3```
        - 1 and 4 belongs to same subset.
    - ```union(A, B)``` O(n)
        - ```rootA = find(A)```
        - ```rootB = find(B)```
        - ```connect rootA -> rootB```
- Steps to find circle - find the superfluous edge that contributes to the disjoint-set.
    - given nodes and edges
    - use a parent array to record the parent of each node: ```parent[node.length]```
    - initialize all nodes to be disjoint sets
        - for each node, ```parent[i] = -1```
        - for each edge A -> B,
            - ```rootA = find(A)```
            - ```rootB = find(B)```
            - if rootA != rootB: union(A, B)
            - else: return Circle Detected

[LeetCode 685. Redundant Connection II](https://www.youtube.com/watch?v=lnmJT5b4NlM)



