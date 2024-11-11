# Pacman-UC_Berkeley-Cs188
Project: Search in Pacman's World
Introduction
This project involves implementing various search algorithms to enable Pacman to navigate through mazes efficiently. The primary goal is to build general search algorithms and apply them to different search problems within the Pacman world.

Files Modified
search.py: Contains the implementation of generic search algorithms.
searchAgents.py: Contains the implementation of specific search agents that utilize the search algorithms.
Search Algorithms Implemented in search.py
1. Depth-First Search (DFS)
Function: depthFirstSearch(problem)
Description: Implements a graph-based DFS algorithm. It uses a stack (implemented via a list) to keep track of nodes to visit next. The algorithm explores as far as possible along each branch before backtracking.
Approach:
Initialize a stack with the start state.
Loop until the stack is empty:
Pop a node from the stack.
If the node hasn't been visited:
Mark it as visited.
If it's the goal state, return the actions to reach it.
Push all unvisited successors onto the stack.
2. Breadth-First Search (BFS)
Function: breadthFirstSearch(problem)
Description: Implements a graph-based BFS algorithm. It uses a queue to explore nodes level by level, ensuring the shortest path is found in an unweighted graph.
Approach:
Initialize a queue with the start state.
Loop until the queue is empty:
Dequeue a node.
If the node hasn't been visited:
Mark it as visited.
If it's the goal state, return the actions to reach it.
Enqueue all unvisited successors.
3. Uniform Cost Search (UCS)
Function: uniformCostSearch(problem)
Description: Implements UCS using a priority queue where the priority is the cumulative cost from the start state. It ensures the least costly path is found in graphs with varying step costs.
Approach:
Initialize a priority queue with the start state and a cost of 0.
Loop until the queue is empty:
Pop the node with the lowest cost.
If the node hasn't been visited:
Mark it as visited.
If it's the goal state, return the actions to reach it.
For each unvisited successor, calculate the new cost and update the queue.
4. A* Search Algorithm
Function: aStarSearch(problem, heuristic)
Description: Enhances UCS by incorporating a heuristic function to estimate the cost to the goal. It uses a priority queue where the priority is the sum of the cumulative cost and the heuristic estimate.
Approach:
Initialize a priority queue with the start state and the heuristic cost.
Loop until the queue is empty:
Pop the node with the lowest combined cost.
If the node hasn't been visited:
Mark it as visited.
If it's the goal state, return the actions to reach it.
For each unvisited successor, calculate the new cost and heuristic, then update the queue.
Search Agents Implemented in searchAgents.py
1. CornersProblem
Class: CornersProblem(search.SearchProblem)
Description: A search problem where Pacman must navigate through all four corners of the maze.
State Representation: A tuple containing Pacman's current position and a tuple of booleans indicating which corners have been visited.
Methods:
getStartState(): Returns the start state.
isGoalState(state): Checks if all corners have been visited.
getSuccessors(state): Generates successors by moving in all possible directions and updating the corners visited.
Heuristic:
Function: cornersHeuristic(state, problem)
Description: Estimates the cost to reach the goal by calculating the Manhattan distance to the nearest unvisited corner.
2. FoodSearchProblem
Class: FoodSearchProblem
Description: Pacman must collect all the food dots in the maze.
State Representation: A tuple containing Pacman's current position and a Grid of remaining food positions.
Methods:
getStartState(): Returns the start state.
isGoalState(state): Checks if all food has been consumed.
getSuccessors(state): Generates successors by moving in all possible directions and updating the food grid.
Heuristic:
Function: foodHeuristic(state, problem)
Description: Estimates the cost to collect all remaining food. One approach is to use the maximum Manhattan distance to any remaining food dot.
3. ClosestDotSearchAgent
Class: ClosestDotSearchAgent(SearchAgent)
Description: An agent that greedily moves towards the nearest food dot, reducing computation time at the expense of possibly not finding the optimal path.
Methods:
registerInitialState(state): Initializes the agent and finds a path to the closest dot repeatedly until all food is consumed.
findPathToClosestDot(gameState): Finds a path to the nearest food dot using BFS.
Helper Class:
Class: AnyFoodSearchProblem(PositionSearchProblem)
Description: A search problem that defines any food dot as a goal state.
Observations and Results
DFS:

Can quickly find a solution but not guaranteed to be the shortest path.
May explore deep into one branch before considering others.
BFS:

Guarantees the shortest path in terms of the number of actions.
Explores nodes level by level, which can lead to high memory usage.
UCS:

Finds the least costly path when actions have different costs.
Useful when moving in certain directions or areas has different costs.
A*:

More efficient than UCS when a good heuristic is used.
The quality of the heuristic significantly affects performance.
Ensures optimality if the heuristic is admissible and consistent.
CornersProblem Heuristic:

Using the minimum distance to the nearest unvisited corner helps guide the search efficiently.
Admissibility and consistency are crucial for A* to find the optimal path.
FoodSearchProblem Heuristic:

A simple heuristic like the maximum distance to any food dot provides a lower bound.
More sophisticated heuristics can further reduce the number of nodes expanded.
ClosestDotSearchAgent:

Provides a practical solution when optimality is less critical.
Demonstrates that greedy approaches can be effective in certain scenarios.
Conclusion
By implementing these search algorithms and agents, we enhanced Pacman's ability to navigate mazes efficiently. The project reinforced understanding of fundamental search strategies in artificial intelligence and highlighted the importance of heuristics in optimizing search performance.
