# Unity-2D-Roguelike-Tutorial
Unity's 2D Roguelike Tutorial: A grid-based roguelike with random procedural generation of levels. 


## Things of note:

* **The game interestingly uses Physics2D/Rigidbody2D/Collider2D for movement/collision-detection.**
	* Not such an issue for smaller game boards, but could be overkill for larger boards.
	* Bug prone: If not implemented properly, player & enemy can overlap on same tile.
		* This can actually happen in the given implementation.

* **There is no traditional internal data model of of the grid-based game board:**
	* e.g. No int[,] storing game tile types/positions as integers.
	* The game board tiles are instantiated sprite prefabs on-the-fly.

* **Movement & collision is done through the use of 2D components:**
	* The Walls, Exit, Player, Enemy, & Food prefabs all contain Collider2D components.
	* Player & Enemy both use `Rigidbody2D.MovePosition()` for movement.
	* Collisions are detected through `RaycastHit2D Physics2D.Linecast()` hits on colliders.

* **The game could easily be optimized by using a 2D array representation of the board.**
	* No need for the use of heavy "physics-based" components and methods.
	* Movement & collisions would be implemented by simple index lookups.
		* `Input.GetAxisRaw()` -> {-1,1} would be perfect for index arithmetic.

-----------------------
## Some Current Edits:

* Added UNITY_WEBGL to preprocessor directive for inputs in `Player.cs`.

* Added some alpha in canvas color to see board for debugging the setup.
	* Bugs found: Player can actually move 1 tile during setup & game over.
		* See Issues (closed) for quick fixes.

* Player is instantiated at runtime in `BoardManager.cs` (instead of already existing in scene).

**Experimentation:**

* Use `Vector3.SmoothDamp` for `SmoothMovement()` method in `MovingObject.cs`.
	* `rb2D.MovePosition(end);` to ensure player's transform position is integral after movement.

