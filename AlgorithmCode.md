## 1- Fractional Knapsack Problem: Greedy algorithm with Example
### What is Greedy Strategy?
- Greedy algorithms are like dynamic programming algorithms that are often used to solve optimal problems (find best solutions of the problem according to a particular criterion).

Greedy algorithms implement optimal local selections in the hope that those selections will lead to an optimal global solution for the problem to be solved. Greedy algorithms are often not too hard to set up, fast (time complexity is often a linear function or very much a second-order function). Besides, these programs are not hard to debug and use less memory. But the results are not always an optimal solution.
- There are two critical components of greedy decisions:

  - **Way of greedy selection**. You can select which solution is best at present and then solve the subproblem arising from making the last selection. The selection of greedy algorithms may depend on previous selections. But it cannot depend on any future selection or depending on the solutions of subproblems. The algorithm evolves in a way that makes selections in a loop, at the same time shrinking the given problem to smaller subproblems.
  - **Optimal substructure**. You perform the optimal substructure for a problem if the optimal solution of this problem contains optimal solutions to its subproblems.
A greedy algorithm has five components:

1 - A set of candidates, from which to create solutions.

2 - A selection function, to select the best candidate to add to the solution.

3 - A feasible function is used to decide if a candidate can be used to build a solution.

4 - An objective function, fixing the value of a solution or an incomplete solution.

5 - An evaluation function, indicating when you find a complete solution.

Steps of Algorithm
You see this is a problem of finding max. The list of packages is sorted in descending order of unit costs to consider branching.

**Step 1:** Node root represents the initial state of the knapsack, where you have not selected any package.
  - TotalValue = 0.
  - The upper bound of the root node UpperBound = M * Maximum unit cost.

**Step 2:** Node root will have child nodes corresponding to the ability to select the package with the largest unit cost. For each node, you re-calculate the parameters:
  - TotalValue = TotalValue (old) + number of selected packages * value of each package.
  - M = M (old) – number of packages selected * weight of each package.
  - UpperBound = TotalValue + M (new) * The unit cost of the packaced to be considered next.

**Step 3:** In child nodes, you will prioritize branching for the node having the larger upper bound. The children of this node correspond to the ability of selecting the next package having large unit cost. For each node, you must re-calculate the parameters TotalValue, M, UpperBound according to the formula mentioned in step 2.

**Step 4:** Repeat Step 3 with the note: for nodes with upper bound is lower or equal values to the temporary maximum cost of an option found, you do not need to branch for that node anymore.

**Step 5:** If all nodes are branched or cut off, the most expensive option is the one to look for.

Pseudo code for the algorithm:

Fractional Knapsack (Array W, Array V, int M)
1. for i <- 1 to size (V)
2. 	calculate cost[i] <- V[i] / W[i]
3. Sort-Descending (cost)
4. i ← 1
5. while (i <= size(V))
6. 	if  W[i] <= M 
7.		M ← M – W[i]
8.		total ← total + V[i];
9. 	if  W[i] > M
10. 		i ← i+1

The complexity of the algorithm:

If using a simple sort algorithm (selection, bubble…) then the complexity of the whole problem is O(n2).
If using quick sort or merge sort then the complexity of the whole problem is O(nlogn).

### Python3 code for Greedy Three

- Firstly, you define class KnapsackPackage.

```python
class KnapsackPackage(object): 
      
    """ Knapsack Package Data Class """
    def __init__(self, weight, value): 
        self.weight = weight 
        self.value = value 
        self.cost = value / weight 
  
    def __lt__(self, other): 
        return self.cost < other.cost 
```
- __lt__(self, other) Defines the behaviour of the less-than operator <

- You then create a function to perform the algorithm Greedy Three.

```python
class FractionalKnapsack(object):
    def __init__(self):
        
    def knapsackGreProc(self, W, V, M, n):
        packs = []
        for i in range(n): 
            packs.append(KnapsackPackage(W[i], V[i]))
            
        packs.sort(reverse = True)
        
        remain = M
        result = 0
        
        i = 0
        stopProc = False
        
        while (stopProc != True):
            if (packs[i].weight <= remain):
                remain -= packs[i].weight;
                result += packs[i].value;
                
                print("Pack ", i, " - Weight ", packs[i].weight, " - Value ", packs[i].value)
            
            if (packs[i].weight > remain):
                i += 1
                
            if (i == n):
                stopProc = True            
        
        print("Max Value:\t", result)  
```

Explanation of code:

  1 - Initialize weight and value for each knapsack package.

  2 - Sort knapsack packages by cost with descending order.
  
  3 - If select package i.
  
  4 - If select the number of package i is enough.
  
  5 - Stop when browsing all packages.
  
Here is Python3 code to run the above program with the first example:
  
```python
if __name__ == "__main__": 
    W = [15, 10, 2, 4] 
    V = [30, 25, 2, 6] 
    M = 37
    n = 4
    
    proc = FractionalKnapsack()
    proc.knapsackGreProc(W, V, M, n)
```
