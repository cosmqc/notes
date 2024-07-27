An issue that affects all generic search algorithms is the possibility of multiple paths leading to the same node. This can cause cycles (meaning the search tree will be infinite) and wasted computation. The solution to this is **pruning**.
### Pruning
Principle:
>Do not expand paths to nodes that have been considered for expansion

A node is considered *for expansion* when the frontier returns a path ending in that node to the search algorithms. Also called visited, expanded, considered, etc.

Implementation
- Frontier needs to keep track of nodes that are visited by remembering the end nodes of returned paths (usually by storing them in a set)
- When trying to add a **new path** to the frontier, it is only added if it doesn't end in a node that's already in the set. If that check fails, that path is discarded/**pruned**.
- When asking the frontier to return the next path, ...


### Search heuristic
Idea:
> Don't ignore information about the goal when selecting paths. Often there is extra knowledge that can be used to guide the search.

h(n) is an **estimate** of the cost of the shortest path from node n to a goal node
- needs to be efficient to compute
- can be extended to paths -> h(<n0, n1, ..., nk>) = h(nk)
- h is admissible iff:
	- for all n, the cost ( h(n) )is non-negative
	- there is no path from n to a goal node with a cost less than h(n). In other words, h(n) must be less than or equal to the actual cost, meaning it must never overestimate the cost.
- a heuristic function is found by solving a simpler, less constrained version of the problem (some examples below)

#### Example heuristic functions
- If nodes are points on a plane and the cost is the distance, h(n) could be the euclidean distance (as the bird flies) from n to the closest goal
- If nodes are locations and the cost is time, h(n) could be the euclidean distance divided by the maximum speed
- If nodes are locations in a cardinal maze, h(n) can be the Manhattan distance (most direct path if there were no walls). 

## Best-first search strategy
Idea
> Select the path whose end is closest to a goal according to the heuristic function

- a greedy strategy that selects a path on the frontier with the lowest h-value
- treats the frontier as a priority queue ordered by h
- by exploring more 'promising' paths first, tends to be more efficient than LCFS
- **does not guarantee finding an optimal solution**

## A* search strategy
Idea
- Don't be as wasteful as LCFS
- Don't be as greedy as best-first search
- Estimate the cost of paths as if they could be extended to reach a goal in the best possible way

Evaluation function
> f(p) = cost(p) + h(n)
- p is a path, n is the last node on the path
- cost(p) = cost of paths p, actual cost from starting node to current node
- h(n) = an estimate of cost from n to goal, optimistic estimate to closest goal node
- f(p) = estimated total cost of path through p to goal

A* always finds an optimal solution if
- there is a solution
- there is no pruning
- the heuristic function is admissible

Properties:
- Doesn't always halt (if cycle, and no pruning)
- A* more efficient than LCFS if working with a good heuristic

### Effect of pruning on A*
![](images/Pasted%20image%2020240726103458.png)

Expensive paths (sa) was expanded before a cheaper one (sba) could be discovered because f(sa) < f(sb). h(a) is too low compared to h(b), this makes sa look better. (or 
equivalently h(b) is relatively too high making sb look worse.)

We need to create a stronger condition than admissibility to stop this from happening

### Monotonicity
A heuristic function is monotonic if for every two nodes n, and n' is reachable from n:
- h(n) <= cost(n, n') + h(n')
Simply put, the actual cost must always be more than the reduction in heuristic.

If h meets the monotonic requirement, A* using multiple-path pruning yields optimal results.

### Dominance relation
> for all n: h_a(n) >= h_c(n)

- Max of admissible heuristics is admissible
- Gets heuristic closer and closer to actual cost

