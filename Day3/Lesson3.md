# Lesson Day 3

Today will be building our Game Controller object, creating the game UI, and making the game look nice.

### Steps
**1. Create GameController**
- Create a new empty game object and name it **GameController** in the Inspector window.

- Create a new script in the **Scripts** folder and name it **GameController**. Attach this script to the GameController object.

**2. Asteroid Spawning**
- **Live-Code GameController**
```
using UnityEngine;
using System.Collections;

public class GameController : MonoBehaviour {

	public SpaceShip ship; // reference to the ship object.
	public GameObject asteroidPrefab; // variable that will be assigned the Asteroid prefab.
	public int asteroidAmount = 10; // amount of asteroids that will spawn from prefab
	public float spawnDistance = 20f; // distance between asteroids

	// Use this for initialization
	void Start () {
		
		// spawn asteroids at random angles.
		for (int i = 0; i < asteroidAmount; i++) {
			GameObject asteroidObject = Instantiate (asteroidPrefab);

			asteroidObject.transform.SetParent (transform);
                        
			// spawn asteroids random between 0 - 360 degress
			float randomAngle = Random.Range (0, 2 * Mathf.PI);
			float randomHeightAngle = Random.Range (0, 2 * Mathf.PI);

			asteroidObject.transform.position = new Vector3 (
				Mathf.Cos(randomAngle) * spawnDistance,
				Mathf.Cos(randomHeightAngle) * spawnDistance,
				Mathf.Sin(randomAngle) * spawnDistance
			);
		}
	}
  ```
  **End Live-Code**
  
  - With **GameController** selected, click and drag the SpaceShip object into the Ship field. Do the same with for Asteroid Prefab field by dragging Asteroid. Game Controller object should now look like picture below. The Asteroids will now be spawned as children of the GameController object. Notice that Asteroids are spawned in all directions around the Ship object.
  
![](http://i.imgur.com/Hv1vjXL.png)
 
 **3. Create Game Timer UI**
  - Select the **Ship** object, create a new 3D object **3D Text**. Change name to **InfoText**.
  
  - Select text object and change Position to 0, 40, 100 respectivly.
  
  - Change **Anchor** to **Middle Center**, **Alignment** to **Center**, and **Font Size** to **120**.
  
  **4. Game Timer Logic**
  
   - **Live-Code GameController**
   
   - Add ```using UnityEngine.SceneManagement;``` to top of the script;
   
   - Declare the following variables
   ```
   public TextMesh infoText; // Reference to text object.
   private float gameTimer;
   private float gameOverTimer = 3f;
   ```
   - Save script and click **GameController** and drag **InfoText** object into GameController.
   
   - Add timer logic to Update method. This will keep track of the state of the game.
   ```// Update is called once per frame
	void Update () {

		// GameOver Logic
    
    //Counts how many asteroids there are.
		int remainingAsteroids = transform.GetComponentsInChildren<Asteroid> ().Length;
		bool isGameOver = (remainingAsteroids == 0);

		if (isGameOver == false) { 
			gameTimer += Time.deltaTime;

			infoText.text = "Game time: " + Mathf.Floor (gameTimer);
		} else {
			infoText.text = "You win!\nYour time: " + Mathf.Floor (gameTimer);

			gameOverTimer -= Time.deltaTime;
			if (gameOverTimer <= 0f) {
				SceneManager.LoadScene (SceneManager.GetActiveScene().name);
			}
		}
	}
  ```
  - Add ```using UnityEngine.SceneManagement;``` to the top of the script. This will load the game when the game timer runs out.
  
  **End Live-Code**
  
  - Select **GameController** object and drag the **InfoText** object into the field.
  
  ![](http://i.imgur.com/dukSZ4Q.png)
  
  - Save game and test logic.
  
  **5. Making it pretty**
  - 
  - Drag **Asteroid** prefab into the Hierarchy window.
  
  - Find the **Design** folder in the Project window and open. Drag the **Space Rock** prefab onto the **Asteroid** prefab in the Hierarchy window. Delete both cubes as not needed anymore. Re-apply your Asteroid Material again. Click **Apply** in the Inspector window to bind the new changes to the prefab. Delete the Asteroid out of the Hierachy window.
  
  - Drag the **Space View** into the **Scene** window. This will apply our space theme.
  
  - Drag the **Star Ship** prefab onto the **SpaceShip** object so that it is a child element of the Ship. You should now see your Space Vehicle in your Scene window. **Position** the Star Ship with the values of **0, -2.8, 7.8** respectivly. **Scale** this ship with values of **65, 77,4, 78.5**. This will allow ship to fit in window on build.
  
  - Save game and Play. Star Ship should now be positioned correctly.
  
  **6. Fixing Bullet firing location**
  - **Live-Code Ship**
  
  - Declare new variable ```public GameObject bulletOrigin;```
  
  - Change ```BulletObject.transform.position = transform.position;``` **TO** ```bulletObject.transform.position = bulletOrigin.transform.position;```
  - **End LIVE-CODE**
  
  - Select Ship, and create **New Empty Object** and name it **BulletOrigin**. Drag it under appropriate location in Inspector window.
  
![](http://i.imgur.com/Rel2fnD.png)
  
  - Change the Position of **BulletOrigin** to **-0.08, -1.89, 13.21** respectivly. This will now be the location from where the bullet fires from. **Note** you can make the bullet fire from any location if you change the location of **BulletOrigin**
  
  - Save game and Play. Bullet should now fire from the front of the ship.
  

### Stretch Goals
 - Change ship size, colors
 - Change bullet origin to fire from left or right of ship.
 - Change lighting in the game
 - Import Assets from the asset store.
 
 ### Change Game Difficulty
 - Change Amount of Asteroids that are spawned.
 - Change Spawn distance.
 - Shorten game timer.
 - Change Asteroid health.
 - Change Asteroid speed.
   
