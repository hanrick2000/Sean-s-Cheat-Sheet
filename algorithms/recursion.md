<extoc></extoc>

# Recursion

## Breadth-First Search (BFS-1)

__Problems__

__P1. Level order treverse__

__P2. Bipartite__

The graph can be divided into two parts, in either of  which there is no direct edges between nodes.

![Bipartite Graph](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/Simple-bipartite-graph.svg/440px-Simple-bipartite-graph.svg.png)

- use two explored sets
- make sure nodes of two consequent levels do not have nodes in common.

__P3. Determine whether a binary tree is a complete binary tree__

- find the first node that misses one or two children node.
- ensure the nodes behind have no child.

## Best-First Search (BFS-2)

Dijkstra's algorithm - Search with PriorityQueue

__Problems__

__P1. find the shortest path cost from source node to  any other nodes in the graph__

- 点到面
- 使用Min Heap记录candidates
- Any node can only be expanded once but can be generated more than once.

## Depth First Search (DFS, Back-tracking) 

- Draw recursion tree
    - How many levels are there?
    - How many branches can we make from the current code?
    - **Two kinds of recursion tree**
        - I. in each level, there exists **only two branches**, that is, to add and not to add.
            - **base case should add to result and return**
        - II. in each level, there exists many branches that depends on what choices are left. **(NOT RECOMMENDED)**
            - **base case should add to result and may not return**
- **Issues and tricks**
    - **inplace**
        - **split the input array into two parts** by using **`swap`** (Problem: permutation)
            - `Arranged characters | Candidate characters`
        - use two resizable container respectively record the arranged charcters and candidate charcters**. In Java, use `StringBuilder` to record arranged characters and use `Set`/`List`/`boolean[]` to record candidates.
    - **remove duplicate**
        - **sort the array first then use a while loop to move index ** in each function call when using recursion tree I
        - use extra space like `HashSet` in Java to record used characters in each level

### P1. subsets

### P2. make up 99 cents with 4 kinds of coins
    - 4 levels in total

### P3. 

### P4. Permutations

### P5. List all valid combination of factors that form an integer.

- Recursion I. 
    - on each level, we have lots of branches, which represent all possible number of current factor
    - factors go down as along as level increase
```
          12
    /            \
   6^0           6^1
  /   \          /   \
 4^0  4^1       4^0  4^1
 ...
```

- Recursion II.
    - on each level, we have lots of branches, which represent all the possible and smaller or equal factors.
    - **only expand factors that are less than or equal to the previous factor**
    
```
                12
        /    |      |    \
        6(2) 4(3)  3(4)  2(6)
       /     |      |     |
      2      3      2     2(3)
                    |     |
                    2(v)  x
```

- Memorization
    ```
    List<List<Integer>> findCombination(int num, int[] factors, int index, Map<Integer, List<List<Integer>>> mem) {
        if (mem.containsKey(num)) return mem.get(num);
        if (num == 1) return new ArrayList<>();
        
        List<List<Integer>> newRes = new ArrayList<>();
        for (int i = index; i < factors.length; i++) {
            if (num % factors[i] == 0) {
                List<List<Integer>> res = findCombination(num / factors[i], factors, index);
                if (res.size() == 0) newRes.add(new ArrayList<>(){{add(factors[i]);}});
                else {
                    for (List<Integer> one: res) {
                        List<Integer> newOne = new ArrayList<>(one);
                        newOne.add(factors[i]);
                        newRes.add(newOne);
                    }
                }
            }
        }
        return newRes
    }
    ```

### P6. Print all permutations of ([{

- dfs
- use stack to determine which right parenthesis to add (because we need to do linear scan)

## From S^T to S*T

Viterbi Algorithm

Coke Range Machine


