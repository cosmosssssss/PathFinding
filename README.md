A* PathFinding
===
This project used Blueprint to implement A* algorithm in UE4 and achieved the AI character pathfinding event. I wrote custom event in the AI character blueprint, and I put the function in the Grid blueprint. So AI characters can call timer event, and the Grid can call the function without multi-AI characters' influence.  

Playing instruction
--
* Press Num '1' button: The system will automatically explore the all grids in the map except for the red ones
* Press Num '2' button: The system starts to find the shortest route from their start girds to the destination; after finding the shortest route, they will move to the destination through the path.

Implementation description
--
### 1. Setting grids
The grid is created by a plane, a box collision and a particle component:
* The plane I used is provided by UE4, but I assigned a new materials for it so that I could distinguish it when I put it on the ground. The red grid means it is blocked so it won't be explored anymore (AI character cannot cross it). 
* The box collision is used for detecting of ray.
* The particle component will be set active when the grid is scaned.

### 2. Explore all the grids
* Using the Function "Multiboxtraceforobjects" to scan the grid nearby. Explore all the grids in the map one by one by looping around and count the number of steps to each position. 
* Grids might be scaned more than once. Thus, we need to compare the data that was previously stored with the data that is now being explored. Then saved the shortest data into an array.

### 3. Pathfinding
* This event starts from the destination to the AI character, since it can reduce computation.
* The shortest path is selected through a series of comparisons.
* The path will be marked by green grids.

### 4. Moving AI character
* Using the function "AI MOVE TO", and let the AI character move forward one grid by one grid. And the target grid (next grid) is already stored in an array during pathfinding. However, we can clearly see that when AI character is moving, it always pauses as he moves. That's because I set the next grid as the target place, so AI character will stop in the target grid and then start to move to next grid.
* We use timeline to fix this problem, but in this way, the game can only be played by one person.

Future work
--
* Add more different types of grid in order to make this game more interesting.
* Try to figure out another way to allow the AI character to move.
