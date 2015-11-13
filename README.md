# Unity-2D-Roguelike-Tutorial
Unity's 2D Roguelike Tutorial: A grid-based roguelike with random procedural generation of levels. 


## Things of note:

* **The game interestingly uses Physics2D/Rigidbody2D/Collider2D for movement/collision-detection.**
	* Not such an issue for smaller game boards, but could be overkill for larger boards.

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
## My Current Edits:

* Added some alpha in canvas color to see board for debugging setup.
	* Bug found: Player can actually move 1 tile during setup.

* Player is instantiated at runtime in `BoardManager.cs` (instead of existing in scene).

* Using Vector3.SmoothDamp for `SmoothMovement()` method in `MovingObject.cs`.
	* `rb2D.MovePosition(end);` to ensure player's transform position is integral after movement.

