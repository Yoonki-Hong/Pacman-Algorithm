# AI 인공지능
See Midterm and Final Project:
https://sites.google.com/hanyang.ac.kr/2021ai

## Environment / Dependencies
```bash
Windows 10
Anaconda 4.10.1
Python 2.7
```

## Getting Started
Files you'll edit:
* search.py : Where all of your search algorithms will reside.
* searchAgents.py : Where all of your search-based agents will reside.

Files you may read but NOT edit:
* pacman.py : The main file that runs Pacman games. This file describes a Pacman GameState type, which you use in this project.
* game.py : The logic behind how the Pacman world works. This file describes several supporting types like AgentState, Agent, Direction, and Grid.
* util.py : Useful data structures for implementing search algorithms.

The simplest agent in searchAgents.py is called the GoWestAgent, which always goes West (a trivial reflex agent). This agent can occasionally win:
```bash
python pacman.py --layout testMaze --pacman GoWestAgent
```

But, things get ugly for this agent when turning is required:
```bash
python pacman.py --layout tinyMaze --pacman GoWestAgent
```

Note that pacman.py supports a number of options that can each be expressed in a long way (e.g., --layout) or a short way (e.g., -l). You can see the list of all options and their default values via:
```bash
python pacman.py -h
```

## Task1: Finding a Fixed Food Dot using Depth First Search
Implement the depth-first search (DFS) algorithm in the depthFirstSearch function in search.py. To make your algorithm complete, write the graph search version of DFS, which avoids expanding any already visited states.

Your code should quickly find a solution for:
```bash
python pacman.py -l tinyMaze -p SearchAgent
python pacman.py -l mediumMaze -p SearchAgent
python pacman.py -l bigMaze -z .5 -p SearchAgent
```
If you use a Stack as your data structure, the solution found by your DFS algorithm for mediumMaze should have a length of 130 (provided you push successors onto the fringe in the order provided by getSuccessors; you might get 246 if you push them in the reverse order).

## Task2: Breadth First Search
Implement the breadth-first search (BFS) algorithm in the breadthFirstSearch function in search.py. Again, write a graph search algorithm that avoids expanding any already visited states. Test your code the same way you did for depth-first search.
```bash
python pacman.py -l mediumMaze -p SearchAgent -a fn=bfs
python pacman.py -l bigMaze -p SearchAgent -a fn=bfs -z .5
```
Does BFS find a least cost solution? If not, check your implementation.

If Pacman moves too slowly for you, try the option --frameTime 0.

If you've written your search code generically, your code should work equally well for the eight-puzzle search problem without any changes.
```bash
python eightpuzzle.py
```

## Task3: Varying the Cost Function
While BFS will find a fewest-actions path to the goal, we might want to find paths that are "best" in other senses.

Implement the uniform-cost graph search algorithm in the uniformCostSearch function in search.py.

```bash
python pacman.py -l mediumMaze -p SearchAgent -a fn=ucs
python pacman.py -l mediumDottedMaze -p StayEastSearchAgent
python pacman.py -l mediumScaryMaze -p StayWestSearchAgent
```

## Task4: Greedy Algorithm
Sometimes, even with breath, depth-first search, finding the optimal path through all the dots is hard. In these cases, we'd still like to find a reasonably good path, quickly. In this section, you'll write an agent that always greedily eats the closest dot.

Implement the function findPathToClosestDot in searchAgents.py. Our agent solves this maze (suboptimally!) in under a second with a path cost of 350:
```bash
python pacman.py -l bigSearch -p ClosestDotSearchAgent -z .5
```