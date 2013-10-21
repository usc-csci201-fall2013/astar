#Restaurant A*
by David Wilczynski

This document describes how A* is used in a previous version of the Restaurant. I believe I have included everything you need, but feel free to post questions in this repository's [issue tracker](https://github.com/usc-csci201-fall2013/astar/issues)

In this repository, you will see the following:
  + `README.md` &ndash; this document
  
  + `astar` &ndash; The `astar` package. Contains all the code to implement the astar traversal in the restaurant. You will NOT need to change it.
  
  + `RestaurantPanel.java` &ndash; The code that does the following major things:
    1. Creates the semaphore grid in its constructor. Initially, all the grid elements have 1 permit. It then acquires the permit for all the permanently allocated grid positions: the tables, the waiting areas, the cook areas, etc.
    1. Whenever a waiter is created, an astar object is initialized as follows:
```java
AStarTraversal aStarTraversal = new AStarTraversal(grid);
```
    1. Then, a waiter in instantiated in addPerson() as follows:
```java
WaiterAgent w = new WaiterAgent(name, aStarTraversal, restaurant, tables);
```
  
  + WaiterAgent.java &ndash; The waiter is the only agent who moves in this version.

In the `WaiterAgent` you will see all the `DoXXX()` calling the following:
```java
guiMoveFromCurrentPostionTo(Position to) {
	...
};
```

This routine calls A* and carries out the walk. There are two versions of the code:
  1. The code dithers if a square in the walk has been acquired by another waiter. Remember, this can happen because two different waiters can call astar "simultaneously." At the time, astar found those squares available. During the walk, however, a waiter could move into a square another waiter want to `moveInto()`. Waiting will usually work.
  
  1. The commented out code doesn't wait, but simply recomputes A*.
  
  1. As the walk is happening, animation calls are made. You will have to make different calls, but the idea is the same. You should use a grid with similar granularity to the one in the program, but then the actual animation walk will be at the pixel level, like it is in your v2.

###Discussion
I don't want to say too much here. Read the code, ask me for help, advice, whatever. Use the [issue tracker for this repository](https://github.com/usc-csci201-fall2013/astar/issues) to discuss.
