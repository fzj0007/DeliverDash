# Delivery Dash - Complete 2D Game Development Tutorial
## CS 4700: Game Dev | Mini-Project 1

---

## **Project Overview**

**Game Concept**: Create a top-down 2D delivery game where players drive a car to pick up packages and deliver them to customers while avoiding obstacles and collecting speed boosts.

**Learning Outcomes**: By completing this project, you will understand:
- Core C# programming concepts (methods, variables, conditionals)
- Unity physics system (colliders, rigidbodies, triggers)
- Input handling and player control
- Object-oriented programming basics
- Unity's component system
- UI implementation
- Game state management


## **Section 1: Project Setup & Introduction**

### Learning Objectives
- Create a new Unity 2D project
- Understand the Unity interface layout
- Set up proper project organization

### Steps

1. **Create New Project**
   - Open Unity Hub
   - Click "New Project"
   - Select "2D (Build-In Render Pipeline)" template
   - Name: "DeliveryDash"
   - Location: Choose your preferred directory
   - Click "Create Project"


2. **Organize Project Structure**
   - In Project window, create folders:
     - `Scenes` (for game levels)
     - `Scripts` (for C# code)
     - `Sprites` (for 2D images)
     - `Prefabs` (for reusable objects)
     - `Materials` (for physics materials)
     - `UI` (for user interface elements)


## **Section 2: Introducing Methods**

### Learning Objectives
- Learn about Unity's built-in methods (Start, Update)
- Create your first script

### Conceptual Overview

**Unity's Special Methods:**
- `Start()` - Runs once when the game starts
- `Update()` - Runs every frame (60+ times per second)

### Steps

1. **Create the Driver Script**
   - Right-click in Scripts folder
   - Create → C# Script
   - Name: "Driver"
   - Double-click to open in your code editor

2. **Understand the Default Code**
   ```csharp
   using UnityEngine;
   
   public class Driver : MonoBehaviour
   {
       // Start is called before the first frame update
       void Start()
       {
           
       }
   
       // Update is called once per frame
       void Update()
       {
           
       }
   }
   ```

3. **Add Debug Messages**
   ```csharp
   void Start()
   {
       Debug.Log("Game has started!");
   }
   
   void Update()
   {
       Debug.Log("Update is running...");
   }
   ```

4. **Test Your Script**
   - Create empty GameObject: GameObject → Create Empty
   - Name it "Car"
   - Add Driver script: drag script onto Car in Inspector
   - Click Play
   - Open Console window: Window → General → Console
   - Observe the messages (Stop after a few seconds!)

---

## **Section 3: Transform.Translate()**

### Learning Objectives
- Understand the Transform component
- Learn how to move objects in 2D space
- Practice using Unity's coordinate system

### Conceptual Overview

**Transform Component**: Every GameObject has a Transform that stores its position, rotation, and scale.

**Translate()**: Moves an object by adding to its current position.
- `Translate(x, y, z)` in 2D, we use x and y
- Positive Y = up, Negative Y = down
- Positive X = right, Negative X = left

### Steps

1. **Add Movement Code**
   ```csharp
   void Update()
   {
       transform.Translate(0, 0.01f, 0);
   }
   ```

2. **Test Movement**
   - Click Play
   - Watch your Car move upward
   - Notice it moves in Scene view and Game view

3. **Experiment with Different Values**
   ```csharp
   // Move right
   transform.Translate(0.01f, 0, 0);
   
   // Move diagonally
   transform.Translate(0.01f, 0.01f, 0);
   
   // Move down
   transform.Translate(0, -0.01f, 0);
   ```

4. **Understanding the Numbers**
   - The third parameter (z) is 0 in 2D games
   - Larger values = faster movement
   - Small values (0.01f) because Update runs ~60 times/second

**💡 Key Takeaway**: Transform.Translate() moves objects relative to their current position. The 'f' after numbers means "float" (decimal number).

---

## **Section 4: Introducing Variables**

### Steps

1. **Declare a Speed Variable**
   ```csharp
   public class Driver : MonoBehaviour
   {
       float moveSpeed = 0.01f;
       
       void Update()
       {
           transform.Translate(0, moveSpeed, 0);
       }
   }
   ```

2. **Test with Different Values**
   - Change `moveSpeed = 0.02f;`
   - Play and observe faster movement
   - Try `0.001f` for slower movement

3. **Add More Variables**
   ```csharp
   float moveSpeed = 0.01f;
   float turnSpeed = 0.1f;
   int numberOfDeliveries = 0;
   bool hasPackage = false;
   ```

---

## **Section 5: Using SerializeField**

### Learning Objectives
- Understand public vs private variables
- Learn to expose variables in the Inspector
- Practice adjusting values without recompiling

### Conceptual Overview

**Access Modifiers:**
- `public` - Visible everywhere, including Inspector
- `private` - Only visible within the script (default)

**[SerializeField]**: Makes private variables visible in Inspector while keeping them private in code (best practice).

### Steps

1. **Compare Public and Private**
   ```csharp
   public float moveSpeed = 0.01f;      // Visible in Inspector
   private float turnSpeed = 0.1f;      // Hidden in Inspector
   float rotationSpeed = 50f;           // Also private (default)
   ```
   
2. **Test in Unity**
   - Select Car GameObject
   - See moveSpeed in Inspector
   - turnSpeed and rotationSpeed are hidden

3. **Use SerializeField (Best Practice)**
   ```csharp
   [SerializeField] float moveSpeed = 0.01f;
   [SerializeField] float turnSpeed = 0.1f;
   [SerializeField] float rotationSpeed = 50f;
   ```

4. **Benefits of SerializeField**
   - Variables visible in Inspector for easy tuning
   - Still private (can't be accessed by other scripts accidentally)
   - Values persist between play sessions
   - Can adjust while game is running (for testing)

5. **Organize Your Variables**
   ```csharp
   public class Driver : MonoBehaviour
   {
       [Header("Movement Settings")]
       [SerializeField] float currentSpeed = 5f;
       [SerializeField] float steerSpeed = 200f;
       
       [Header("Speed Variations")]
       [SerializeField] float boostSpeed = 10f;
       [SerializeField] float regularSpeed = 5f;
       
       void Update()
       {
           transform.Translate(0, currentSpeed * Time.deltaTime, 0);
       }
   }
   ```

**💡 Key Takeaway**: Use [SerializeField] for values you want to adjust in the Inspector while keeping proper encapsulation. It's the Unity best practice!

---

## **Section 6: Keyboard Input & If Statements**

### Learning Objectives
- Handle keyboard input using Unity's Input System
- Implement basic player control

### Conceptual Overview

**Unity Input System**: The modern way to handle player input in Unity.

### Steps

1. **Install Input System Package**
   - Window → Package Manager
   - Switch to "Unity Registry"
   - Find "Input System"
   - Click "Install"
   - Allow Unity to restart

2. **Set Up Input System**
   - Add to Driver.cs:
   ```csharp
   using UnityEngine.InputSystem;
   ```

3. **Detect Single Key Press**
   ```csharp
   void Update()
   {
       if (Keyboard.current.wKey.isPressed)
       {
           Debug.Log("W key is pressed!");
       }
   }
   ```

4. **Multiple Keys with If-Else**
   ```csharp
   void Update()
   {
       if (Keyboard.current.wKey.isPressed)
       {
           Debug.Log("Moving forward");
           transform.Translate(0, 0.1f, 0);
       }
       else if (Keyboard.current.sKey.isPressed)
       {
           Debug.Log("Moving backward");
           transform.Translate(0, -0.1f, 0);
       }
   }
   ```

5. **Add Rotation Input**
   ```csharp
   void Update()
   {
       // Forward/Backward
       if (Keyboard.current.wKey.isPressed)
       {
           transform.Translate(0, 0.1f, 0);
       }
       else if (Keyboard.current.sKey.isPressed)
       {
           transform.Translate(0, -0.1f, 0);
       }
       
       // Left/Right Rotation
       if (Keyboard.current.aKey.isPressed)
       {
           transform.Rotate(0, 0, 1f);
       }
       else if (Keyboard.current.dKey.isPressed)
       {
           transform.Rotate(0, 0, -1f);
       }
   }
   ```

6. **Using Variables for Input**
   ```csharp
   void Update()
   {
       float move = 0f;
       float steer = 0f;
       
       if (Keyboard.current.wKey.isPressed)
           move = 1f;
       else if (Keyboard.current.sKey.isPressed)
           move = -1f;
           
       if (Keyboard.current.aKey.isPressed)
           steer = 1f;
       else if (Keyboard.current.dKey.isPressed)
           steer = -1f;
   }
   ```

---

## **Section 7: Moving Our Car**

### Learning Objectives
- Combine movement and rotation
- Use variables to control speed
- Implement smooth car controls

### Steps

1. **Clean Movement System**
   ```csharp
   [SerializeField] float moveSpeed = 5f;
   [SerializeField] float steerSpeed = 200f;
   
   void Update()
   {
       float move = 0f;
       float steer = 0f;
       
       // Get input
       if (Keyboard.current.wKey.isPressed)
           move = 1f;
       else if (Keyboard.current.sKey.isPressed)
           move = -1f;
           
       if (Keyboard.current.aKey.isPressed)
           steer = 1f;
       else if (Keyboard.current.dKey.isPressed)
           steer = -1f;
       
       // Apply movement
       float moveAmount = move * moveSpeed;
       float steerAmount = steer * steerSpeed;
       
       transform.Translate(0, moveAmount, 0);
       transform.Rotate(0, 0, steerAmount);
   }
   ```

2. **Test and Tune**
   - Play the game
   - Adjust moveSpeed in Inspector (try 3-8)
   - Adjust steerSpeed in Inspector (try 100-300)

3. **Understanding the Formula**
   - `move` is -1, 0, or 1
   - Multiply by speed to get actual movement
   - This pattern is standard in game development

**💡 Key Takeaway**: Separating input detection from movement application makes code cleaner and easier to tune.

---

## **Section 8: Using Time.deltaTime**

### Learning Objectives
- Understand frame-rate independence
- Learn why Time.deltaTime is crucial
- Implement smooth, consistent movement

### Conceptual Overview

**The Problem**: Update() runs at different speeds on different computers
- Fast PC: 144 FPS → 144 movements/second
- Slow PC: 30 FPS → 30 movements/second
- Result: Inconsistent game speed!

**The Solution**: Time.deltaTime
- Time since last frame (in seconds)
- ~0.016 seconds at 60 FPS
- ~0.007 seconds at 144 FPS
- Multiply movement by this to normalize

### Steps

1. **Add Time.deltaTime**
   ```csharp
   void Update()
   {
       float move = 0f;
       float steer = 0f;
       
       if (Keyboard.current.wKey.isPressed)
           move = 1f;
       else if (Keyboard.current.sKey.isPressed)
           move = -1f;
           
       if (Keyboard.current.aKey.isPressed)
           steer = 1f;
       else if (Keyboard.current.dKey.isPressed)
           steer = -1f;
       
       // TIME.DELTATIME ADDED HERE!
       float moveAmount = move * moveSpeed * Time.deltaTime;
       float steerAmount = steer * steerSpeed * Time.deltaTime;
       
       transform.Translate(0, moveAmount, 0);
       transform.Rotate(0, 0, steerAmount);
   }
   ```

2. **Adjust Speed Values**
   - Because we're multiplying by a small number (~0.016), we need bigger speeds
   - Change moveSpeed to 5-10
   - Change steerSpeed to 200-300

3. **Test Frame Rate Independence**
   - Play game
   - Movement should feel smooth
   - Speed is now in "units per second" rather than "units per frame"

**💡 Key Takeaway**: ALWAYS multiply movement by Time.deltaTime for frame-rate independent games. This is a fundamental Unity principle!

---

## **Section 9: Colliders & Rigidbodies**

### Learning Objectives
- Understand Unity's physics system
- Add Colliders for collision detection
- Use Rigidbody2D for physics simulation

### Conceptual Overview

**Colliders**: Invisible shapes that define object boundaries
- BoxCollider2D - Rectangles
- CircleCollider2D - Circles
- PolygonCollider2D - Custom shapes

**Rigidbody2D**: Applies physics (gravity, forces, collisions)
- Dynamic - Full physics
- Kinematic - Controllable, but affected by collisions
- Static - Doesn't move

### Steps

1. **Add Sprite to Car**
   - Find or create a simple car sprite (rectangle for now)
   - Select Car GameObject
   - Add Component → Sprite Renderer
   - Drag sprite into Sprite field
   - Set Order in Layer: 1

2. **Add Collider**
   - With Car selected
   - Add Component → Box Collider 2D
   - You'll see green outline in Scene view
   - Adjust size to match sprite

3. **Add Rigidbody2D**
   - Add Component → Rigidbody 2D
   - Set Body Type: Kinematic (we control movement, not physics)
   - Set Gravity Scale: 0 (no gravity in this game)
   - Check "Freeze Rotation Z" (prevent spinning on collision)

4. **Create Ground/Obstacle**
   - GameObject → 2D Object → Sprite → Square
   - Name: "Wall"
   - Position it in front of the car
   - Add Component → Box Collider 2D

5. **Test Collision**
   - Play game
   - Drive into the wall
   - Car should stop (physical collision detected)

6. **Rigidbody2D Settings Explained**
   ```
   Body Type:
   - Dynamic: Full physics, affected by forces/gravity
   - Kinematic: Script-controlled, but can collide
   - Static: Never moves (for walls, ground)
   
   Constraints:
   - Freeze Position: Prevent movement on axis
   - Freeze Rotation: Prevent spinning
   ```

**💡 Key Takeaway**: Colliders define "where" an object is, Rigidbody2D defines "how" it behaves physically. Together they enable collision detection.

---

## **Section 10: Using OnCollisionEnter2D()**

### Learning Objectives
- Detect collision events in code
- Respond to different collision types
- Understand Unity's collision callbacks

### Conceptual Overview

**Collision Callbacks**: Methods Unity automatically calls when collisions occur
- `OnCollisionEnter2D()` - When collision starts
- `OnCollisionStay2D()` - While colliding
- `OnCollisionExit2D()` - When collision ends

**Requirements for Collision**:
- Both objects have Colliders
- At least one has a Rigidbody2D
- Neither collider is set to "Trigger"

### Steps

1. **Add Collision Detection**
   ```csharp
   void OnCollisionEnter2D(Collision2D collision)
   {
       Debug.Log("Collision detected with: " + collision.gameObject.name);
   }
   ```

2. **Create Different Obstacles**
   - Create several Square sprites
   - Name them: "Wall", "Rock", "Tree"
   - Add BoxCollider2D to each
   - Position them around the scene

3. **Test Collision**
   - Play game
   - Drive into obstacles
   - Check Console for collision messages

4. **Respond to Specific Collisions**
   ```csharp
   void OnCollisionEnter2D(Collision2D collision)
   {
       if (collision.gameObject.name == "Wall")
       {
           Debug.Log("Hit a wall!");
           // Could add damage, sound effect, etc.
       }
       else if (collision.gameObject.name == "Rock")
       {
           Debug.Log("Hit a rock!");
       }
   }
   ```

5. **Slow Down on Collision**
   ```csharp
   [SerializeField] float currentSpeed = 5f;
   [SerializeField] float regularSpeed = 5f;
   [SerializeField] float slowSpeed = 2f;
   
   void OnCollisionEnter2D(Collision2D collision)
   {
       Debug.Log("Bumped into something!");
       currentSpeed = slowSpeed;
   }
   ```

   Update Update() method:
   ```csharp
   float moveAmount = move * currentSpeed * Time.deltaTime;
   ```

**💡 Key Takeaway**: OnCollisionEnter2D() lets us respond to physical collisions. Use it for impacts, damage, sound effects, or game state changes.

---

## **Section 11: Using OnTriggerEnter2D()**

### Learning Objectives
- Understand the difference between Collisions and Triggers
- Implement pickup systems
- Create non-blocking interactions

### Conceptual Overview

**Collision vs Trigger**:
- **Collision**: Physical barrier, objects bounce/stop
- **Trigger**: Invisible detection zone, objects pass through

**When to Use Triggers**:
- Pickups (coins, packages)
- Checkpoints
- Detection zones
- Invisible boundaries

### Steps

1. **Create Package GameObject**
   - GameObject → 2D Object → Sprite → Square
   - Name: "Package"
   - Change Sprite color to yellow/gold
   - Scale: (0.5, 0.5, 1)

2. **Add Trigger Collider**
   - Add Component → Box Collider 2D
   - ✅ Check "Is Trigger" box
   - Notice the collider turns green in Scene view

3. **Create Delivery Script**
   - Create new script: "Delivery"
   - Attach to Car GameObject
   ```csharp
   using UnityEngine;
   
   public class Delivery : MonoBehaviour
   {
       void OnTriggerEnter2D(Collider2D collision)
       {
           Debug.Log("Triggered by: " + collision.gameObject.name);
       }
   }
   ```

4. **Test Trigger**
   - Play game
   - Drive through the Package
   - Car passes through (no physical collision)
   - Console shows "Triggered by: Package"

5. **Compare Collision vs Trigger**
   Create two test objects:
   ```
   CollisionTest:
   - Box Collider 2D (Is Trigger: OFF)
   
   TriggerTest:
   - Box Collider 2D (Is Trigger: ON)
   ```
   Drive into both and observe the difference.

6. **Implement Package Pickup**
   ```csharp
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.gameObject.name == "Package")
       {
           Debug.Log("Picked up package!");
           Destroy(collision.gameObject);
       }
   }
   ```

**💡 Key Takeaway**: Triggers detect when objects enter an area without physically blocking them. Perfect for pickups, zones, and sensors!

---

## **Section 12: Introducing Cinemachine**

### Learning Objectives
- Install and configure Cinemachine
- Create smooth camera following
- Understand virtual cameras

### Conceptual Overview

**Cinemachine**: Unity's powerful camera system
- Smooth following
- Look-ahead
- Dead zones
- Professional camera movement

### Steps

1. **Install Cinemachine**
   - Window → Package Manager
   - Find "Cinemachine"
   - Click Install

2. **Create Virtual Camera**
   - GameObject → Cinemachine → 2D Camera
   - Name automatically: "CM vcam1"

3. **Configure Virtual Camera**
   - Select CM vcam1
   - In Inspector, find "Follow" field
   - Drag Car GameObject into Follow field

4. **Adjust Camera Settings**
   ```
   Body:
   - Dead Zone Width: 0.1
   - Dead Zone Height: 0.1
   - Lookahead Time: 0.2
   
   Aim:
   - Dead Zone Width: 0.2
   - Dead Zone Height: 0.2
   ```

5. **Adjust Main Camera**
   - Select Main Camera
   - Check that Cinemachine Brain component was added automatically
   - Set Background to desired color (dark gray for roads)

6. **Test Camera**
   - Play game
   - Drive around
   - Camera smoothly follows car
   - Try different speeds and directions

**💡 Key Takeaway**: Cinemachine handles complex camera behavior with simple setup. It's industry-standard for Unity camera control.

---

## **Section 13: Add Assets To Project**

### Learning Objectives
- Import sprite assets
- Organize project files
- Configure sprite settings

### Steps

1. **Gather or Create Assets**
   You'll need:
   - Car sprite (top-down view)
   - Road/ground tiles
   - Package sprite
   - Customer sprite
   - Obstacle sprites (rocks, trees)
   - Boost pad sprite

2. **Import Sprites**
   - Drag image files into Project → Sprites folder
   - Or: Assets → Import New Asset

3. **Configure Sprite Import Settings**
   For each sprite:
   - Select sprite in Project window
   - Inspector → Texture Type: Sprite (2D and UI)
   - Pixels Per Unit: 100 (default is good)
   - Filter Mode: Point (no filter) for pixel art
   - Compression: None for quality
   - Click Apply

4. **Create Sprite Atlas (Optional, for performance)**
   - Right-click in Project
   - Create → 2D → Sprite Atlas
   - Name: "GameAtlas"
   - Drag all sprites onto it

5. **Organize Assets**
   ```
   Sprites/
   ├── Characters/
   │   └── Car.png
   ├── Environment/
   │   ├── Road.png
   │   ├── Grass.png
   │   └── Buildings.png
   ├── Items/
   │   ├── Package.png
   │   ├── Customer.png
   │   └── Boost.png
   └── Obstacles/
       ├── Rock.png
       └── Tree.png
   ```

**💡 Key Takeaway**: Proper asset organization and import settings save time and prevent issues later in development.

---

## **Section 14: Car & Background**

### Learning Objectives
- Apply sprites to GameObjects
- Set up sprite layers
- Create a basic game environment

### Steps

1. **Apply Car Sprite**
   - Select Car GameObject
   - In Sprite Renderer component
   - Drag car sprite into Sprite field
   - Adjust scale if needed: (1, 1, 1)

2. **Create Background**
   - GameObject → 2D Object → Sprite → Square
   - Name: "Background"
   - Position: (0, 0, 0)
   - Scale: (20, 20, 1)
   - Sprite Renderer → Sprite: Grass/road texture
   - Order in Layer: -10 (behind everything)

3. **Set Up Sprite Layers**
   ```
   -10: Background
   0: Roads, Ground tiles
   1: Obstacles
   2: Pickups
   3: Car
   4: Effects
   5: UI Elements
   ```

4. **Configure Car Sprite Renderer**
   - Select Car
   - Sprite Renderer → Order in Layer: 3
   - This ensures car appears on top

5. **Adjust Collider to Match Sprite**
   - Select Car
   - Box Collider 2D → Edit Collider button
   - Drag edges to match car sprite shape
   - Or adjust Size/Offset values

6. **Test Visual Setup**
   - Play game
   - Car should be clearly visible
   - Movement should feel right for the sprite size
   - Adjust camera orthographic size if needed (Main Camera → Size: 5-10)

**💡 Key Takeaway**: Proper sprite layering and scaling are crucial for visual clarity. Use Order in Layer to control what appears on top.

---

## **Section 15: Create A Level**

### Learning Objectives
- Design a game level
- Use tilemaps for efficient level creation
- Create a road network

### Steps

1. **Install 2D Tilemap Editor (if not installed)**
   - Window → Package Manager
   - Find "2D Tilemap Editor"
   - Install

2. **Create Tilemap**
   - GameObject → 2D Object → Tilemap → Rectangular
   - This creates:
     - Grid (parent)
     - Tilemap (child)

3. **Create Tile Palette**
   - Window → 2D → Tile Palette
   - Create New Palette
   - Name: "RoadPalette"
   - Grid: Rectangle
   - Cell Size: Automatic

4. **Create Tiles**
   - Select road sprite in Project
   - Drag onto Tile Palette window
   - Repeat for grass, corners, intersections

5. **Paint Your Level**
   - Select tool from Tile Palette (pencil, fill, etc.)
   - Select tile
   - Click in Scene view to paint
   - Create a simple road layout:
   ```
   G G G G G G G
   G R R R R R G
   G R G G G R G
   G R G P G R G
   G R G G G R G
   G R R R R R G
   G G G G G G G
   
   G = Grass, R = Road, P = Package
   ```

6. **Add Visual Interest**
   - Place trees/rocks off the road
   - Create parking areas
   - Add customer locations
   - Design pickup/delivery zones

7. **Set Tilemap Layer**
   - Select Tilemap
   - Tilemap Renderer → Order in Layer: 0

**💡 Key Takeaway**: Tilemaps are efficient for creating large, tile-based levels. They automatically handle sprite batching for better performance.

---

## **Section 16: Add Collision Blocks**

### Learning Objectives
- Add collision to tilemaps
- Create boundary walls
- Optimize collision detection

### Steps

1. **Add Tilemap Collider**
   - Select Tilemap GameObject
   - Add Component → Tilemap Collider 2D
   - Play test - collision works but is inefficient

2. **Optimize with Composite Collider**
   - Add Component → Composite Collider 2D
   - Rigidbody2D is automatically added
   - Set Rigidbody2D:
     - Body Type: Static
     - Simulated: ✅
   - Tilemap Collider 2D:
     - Used By Composite: ✅

3. **Adjust Collision Layers**
   - Select Tilemap
   - Layer: Create new layer "Ground"
   - Assign Tilemap to Ground layer

4. **Create Invisible Walls (Boundaries)**
   - GameObject → 2D Object → Sprite → Square
   - Name: "Boundary_Top"
   - Remove Sprite Renderer (or disable it)
   - Add Box Collider 2D
   - Scale to cover top edge of play area
   - Repeat for all four sides

5. **Test Collisions**
   - Play game
   - Car should collide with roads/obstacles
   - Car should not drive off the map

6. **Tag Collision Objects**
   - Select boundary walls
   - Tag → Add Tag → "WorldCollision"
   - Assign tag to all boundaries

**💡 Key Takeaway**: Composite Collider combines multiple tile colliders into one, greatly improving performance. Always optimize collision detection!

---

## **Section 17: Using Tags In Unity**


### Learning Objectives
- Understand Unity's Tag system
- Create custom tags
- Use tags for object identification

### Conceptual Overview

**Tags**: Labels we attach to GameObjects to identify them in code
- More efficient than comparing names
- Standard way to categorize objects
- Can be used for filtering and searching

### Steps

1. **Create Custom Tags**
   - Any GameObject → Inspector → Tag → Add Tag
   - Click '+' to add new tags:
     - "Package"
     - "Customer"
     - "Boost"
     - "WorldCollision"

2. **Assign Tags to Objects**
   - Select package GameObject
   - Tag dropdown → "Package"
   - Select customer GameObject
   - Tag dropdown → "Customer"

3. **Update Delivery Script to Use Tags**
   ```csharp
   void OnTriggerEnter2D(Collider2D collision)
   {
       // OLD WAY (inefficient):
       // if (collision.gameObject.name == "Package")
       
       // NEW WAY (efficient):
       if (collision.CompareTag("Package"))
       {
           Debug.Log("Picked up package!");
           Destroy(collision.gameObject);
       }
   }
   ```

4. **Update Driver Script**
   ```csharp
   void OnCollisionEnter2D(Collision2D collision)
   {
       if (collision.collider.CompareTag("WorldCollision"))
       {
           Debug.Log("Hit a wall!");
           currentSpeed = regularSpeed;
       }
   }
   ```

5. **Benefits of Tags**
   - ✅ Faster than string comparison of names
   - ✅ Typo-safe (autocomplete in IDE)
   - ✅ Can find objects: `GameObject.FindGameObjectWithTag("Package")`
   - ✅ Easy to categorize and organize

6. **Tag Best Practices**
   - Keep tag names simple and clear
   - Use PascalCase: "Package" not "package"
   - Don't overuse - consider Layers for complex systems
   - Document your tag usage

**💡 Key Takeaway**: Tags are the standard way to identify object types in Unity. Always use `CompareTag()` instead of name comparison!

---

## **Section 18: Introducing Bools**


### Steps

1. **Add Package State Tracking**
   ```csharp
   public class Delivery : MonoBehaviour
   {
       bool hasPackage = false;
       
       void OnTriggerEnter2D(Collider2D collision)
       {
           if (collision.CompareTag("Package"))
           {
               Debug.Log("Picked up package!");
               hasPackage = true;
               Destroy(collision.gameObject);
           }
       }
   }
   ```

2. **Create Customer Delivery System**
   - GameObject → 2D Object → Sprite → Circle
   - Name: "Customer"
   - Tag: "Customer"
   - Color: Blue
   - Add: Box Collider 2D (Is Trigger: ✅)

3. **Implement Delivery Logic**
   ```csharp
   bool hasPackage = false;
   
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.CompareTag("Package") && !hasPackage)
       {
           Debug.Log("Picked up package");
           hasPackage = true;
           Destroy(collision.gameObject);
       }
       
       if (collision.CompareTag("Customer") && hasPackage)
       {
           Debug.Log("Delivered package!");
           hasPackage = false;
       }
   }
   ```

4. **Understanding Boolean Operators**
   ```csharp
   // && = AND (both must be true)
   if (hasPackage && nearCustomer)
   
   // || = OR (at least one must be true)
   if (hasPackage || hasBoost)
   
   // ! = NOT (inverts the value)
   if (!hasPackage)  // same as: if (hasPackage == false)
   ```

5. **Prevent Multiple Pickups**
   ```csharp
   if (collision.CompareTag("Package") && !hasPackage)
   {
       // Will only trigger if we DON'T have a package
       // Prevents picking up multiple packages
       hasPackage = true;
       Destroy(collision.gameObject);
   }
   ```

**💡 Key Takeaway**: Bools are essential for tracking game state. Use them to control what actions are possible at any time.

---

## **Section 19: Introducing Prefabs**

### Learning Objectives
- Understand what Prefabs are
- Create reusable game objects
- Use Prefabs for efficient level design

### Conceptual Overview

**Prefab**: A reusable GameObject template
- Create once, use many times
- Edit one, update all instances
- Essential for game development
- Perfect for: Enemies, pickups, obstacles, projectiles

### Steps

1. **Create Package Prefab**
   - Set up one Package GameObject perfectly:
     - Sprite
     - Collider (Is Trigger: ✅)
     - Tag: "Package"
     - Scale
   - Drag from Hierarchy to Prefabs folder
   - GameObject turns blue (prefab instance)

2. **Create Multiple Instances**
   - Drag Package prefab from Project to Scene
   - Place multiple around your level
   - They're all identical

3. **Edit the Prefab**
   - Double-click Package prefab in Project
   - Enter Prefab Mode
   - Change sprite color to bright yellow
   - Exit Prefab Mode (arrow in Hierarchy)
   - ALL instances update automatically!

4. **Create More Prefabs**
   Create prefabs for:
   - Customer
   - Boost pad
   - Obstacles (rock, tree)
   - Walls/barriers

5. **Override Instance Properties**
   - Select one Package instance
   - Change its position/scale
   - Inspector shows "Overrides"
   - Can revert to prefab defaults

6. **Prefab Best Practices**
   ```
   Good Prefab Structure:
   Package (Parent)
   ├── Sprite
   ├── Collider
   ├── Particle Effect
   └── Script
   
   Name: "Package_Prefab"
   Location: Prefabs/Items/
   ```

**💡 Key Takeaway**: Prefabs are crucial for workflow efficiency. Set up objects once, reuse everywhere, edit in one place!

---

## **Section 20: How To Destroy Objects**

### Learning Objectives
- Use Destroy() function
- Understand delayed destruction
- Manage object lifecycle

### Conceptual Overview

**Destroy()**: Removes GameObjects from the scene
- Immediate or delayed
- Affects entire GameObject and children
- Can destroy specific components

**Syntax**: `Destroy(what, optionalDelay)`

### Steps

1. **Immediate Destruction**
   ```csharp
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.CompareTag("Package"))
       {
           Debug.Log("Package collected!");
           Destroy(collision.gameObject);  // Destroyed immediately
       }
   }
   ```

2. **Delayed Destruction**
   ```csharp
   [SerializeField] float destroyDelay = 0.5f;
   
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.CompareTag("Package"))
       {
           Debug.Log("Package collected!");
           Destroy(collision.gameObject, destroyDelay);
       }
   }
   ```

3. **Why Use Delay?**
   - Play pickup animation
   - Show particle effects
   - Fade out audio
   - Smoother visual feedback

4. **Destroy Customer After Delivery**
   ```csharp
   if (collision.CompareTag("Customer") && hasPackage)
   {
       Debug.Log("Package delivered!");
       hasPackage = false;
       Destroy(collision.gameObject);  // Customer satisfied, removed
   }
   ```

5. **Destroy Component vs GameObject**
   ```csharp
   // Destroy entire GameObject
   Destroy(gameObject);
   
   // Destroy specific component
   Destroy(GetComponent<SpriteRenderer>());
   
   // Destroy this script
   Destroy(this);
   ```

6. **Common Mistake: Destroying Too Early**
   ```csharp
   // WRONG - Destroys before delay ends
   Destroy(gameObject, 2f);
   Debug.Log("This won't print!");  // Script destroyed!
   
   // RIGHT - Use Invoke for delayed code
   Destroy(gameObject, 2f);
   ```

7. **Safety Check Before Destruction**
   ```csharp
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision != null && collision.gameObject != null)
       {
           if (collision.CompareTag("Package"))
           {
               Destroy(collision.gameObject, destroyDelay);
           }
       }
   }
   ```

**💡 Key Takeaway**: Destroy() removes objects from memory. Use delays for better visual feedback, but be careful about destroying objects that still need to run code!

---

## **Section 21: Using GetComponent**

### Learning Objectives
- Access other components via code
- Understand component-based architecture
- Control particle systems, sounds, etc.

### Conceptual Overview

**GetComponent**: Retrieves a component attached to a GameObject
- Unity is component-based (not inheritance)
- Each component adds functionality
- Scripts communicate through components

**Syntax**: `GetComponent<ComponentType>()`

### Steps

1. **Add Particle System**
   - Select Car GameObject
   - Add Component → Effects → Particle System
   - Configure particle system:
     ```
     Duration: 1
     Looping: ✅
     Start Lifetime: 0.5
     Start Speed: 2
     Start Size: 0.2
     Emission Rate: 10
     Shape: Cone
     ```
   - Stop it: Click "Stop" in Play mode or uncheck at start

2. **Control Particles from Script**
   ```csharp
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.CompareTag("Package") && !hasPackage)
       {
           Debug.Log("Picked up package");
           hasPackage = true;
           
           // Play particle effect
           GetComponent<ParticleSystem>().Play();
           
           Destroy(collision.gameObject);
       }
   }
   ```

3. **Stop Particles on Delivery**
   ```csharp
   if (collision.CompareTag("Customer") && hasPackage)
   {
       Debug.Log("Delivered package!");
       hasPackage = false;
       
       // Stop particle effect
       GetComponent<ParticleSystem>().Stop();
       
       Destroy(collision.gameObject);
   }
   ```

4. **Cache Component Reference (Optimization)**
   ```csharp
   // Inefficient - GetComponent every frame/trigger
   GetComponent<ParticleSystem>().Play();
   
   // Efficient - Get once, store, reuse
   ParticleSystem packageParticles;
   
   void Start()
   {
       packageParticles = GetComponent<ParticleSystem>();
   }
   
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.CompareTag("Package"))
       {
           packageParticles.Play();  // Use cached reference
       }
   }
   ```

5. **GetComponent on Other Objects**
   ```csharp
   void OnTriggerEnter2D(Collider2D collision)
   {
       // Get component from colliding object
       SpriteRenderer sr = collision.GetComponent<SpriteRenderer>();
       if (sr != null)
       {
           sr.color = Color.red;  // Change color of hit object
       }
   }
   ```

6. **Common Components to GetComponent**
   ```csharp
   // Transform (position, rotation, scale)
   Transform myTransform = GetComponent<Transform>();
   // Or just use: transform (lowercase, built-in)
   
   // Rigidbody2D (physics)
   Rigidbody2D rb = GetComponent<Rigidbody2D>();
   
   // Sprite Renderer (visuals)
   SpriteRenderer sr = GetComponent<SpriteRenderer>();
   
   // Collider
   BoxCollider2D collider = GetComponent<BoxCollider2D>();
   
   // Audio Source
   AudioSource audio = GetComponent<AudioSource>();
   
   // Your custom scripts
   Driver driverScript = GetComponent<Driver>();
   ```

**💡 Key Takeaway**: GetComponent is how scripts interact with other components. Cache references in Start() for better performance!

---

## **Section 22: Boosts & Bumps**

### Learning Objectives
- Implement speed boost mechanic
- Handle collision penalties
- Create dynamic gameplay feel

### Steps

1. **Create Boost Prefab**
   - GameObject → 2D Object → Sprite → Square
   - Name: "Boost"
   - Sprite: Bright green/yellow
   - Tag: "Boost"
   - Add: Box Collider 2D (Is Trigger: ✅)
   - Save as Prefab

2. **Update Driver Script for Boosts**
   ```csharp
   [Header("Speed Settings")]
   [SerializeField] float currentSpeed = 5f;
   [SerializeField] float steerSpeed = 200f;
   [SerializeField] float boostSpeed = 10f;
   [SerializeField] float regularSpeed = 5f;
   
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.CompareTag("Boost"))
       {
           Debug.Log("Speed boost activated!");
           currentSpeed = boostSpeed;
           Destroy(collision.gameObject);  // Remove boost pad
       }
   }
   ```

3. **Reset Speed on Wall Collision**
   ```csharp
   void OnCollisionEnter2D(Collision2D collision)
   {
       if (collision.collider.CompareTag("WorldCollision"))
       {
           Debug.Log("Bumped into wall!");
           currentSpeed = regularSpeed;  // Slow down
       }
   }
   ```

4. **Complete Driver Script**
   ```csharp
   using UnityEngine;
   using UnityEngine.InputSystem;
   
   public class Driver : MonoBehaviour
   {
       [Header("Speed Settings")]
       [SerializeField] float currentSpeed = 5f;
       [SerializeField] float steerSpeed = 200f;
       [SerializeField] float boostSpeed = 10f;
       [SerializeField] float regularSpeed = 5f;
       
       void Start()
       {
           currentSpeed = regularSpeed;
       }
       
       void Update()
       {
           float move = 0f;
           float steer = 0f;
           
           if (Keyboard.current.wKey.isPressed)
               move = 1f;
           else if (Keyboard.current.sKey.isPressed)
               move = -1f;
               
           if (Keyboard.current.aKey.isPressed)
               steer = 1f;
           else if (Keyboard.current.dKey.isPressed)
               steer = -1f;
           
           float moveAmount = move * currentSpeed * Time.deltaTime;
           float steerAmount = steer * steerSpeed * Time.deltaTime;
           
           transform.Translate(0, moveAmount, 0);
           transform.Rotate(0, 0, steerAmount);
       }
       
       void OnTriggerEnter2D(Collider2D collision)
       {
           if (collision.CompareTag("Boost"))
           {
               currentSpeed = boostSpeed;
               Destroy(collision.gameObject);
           }
       }
       
       void OnCollisionEnter2D(Collision2D collision)
       {
           if (collision.collider.CompareTag("WorldCollision"))
           {
               currentSpeed = regularSpeed;
           }
       }
   }
   ```

5. **Place Boosts in Level**
   - Drag Boost prefab into scene
   - Place strategically:
     - On long straightaways
     - Before difficult turns
     - Near packages
   - Create 5-10 boost pads

6. **Test Gameplay Feel**
   - Regular speed: 5
   - Boost speed: 10 (2x faster)
   - Adjust values for your game's feel

**💡 Key Takeaway**: Speed variations create exciting gameplay. Boosts reward skillful play, collisions provide consequences.

---

## **Section 23: Adding UI Text**

### Learning Objectives
- Create Canvas for UI
- Add TextMeshPro text
- Update UI from code

### Steps

1. **Install TextMeshPro**
   - GameObject → UI → Text - TextMeshPro
   - Click "Import TMP Essentials"
   - Click "Import TMP Examples & Extras" (optional)

2. **Create UI Canvas**
   - GameObject → UI → Canvas
   - Canvas automatically created with:
     - Canvas component
     - Canvas Scaler
     - Graphic Raycaster
   - EventSystem also created

3. **Configure Canvas**
   - Canvas Scaler:
     - UI Scale Mode: Scale With Screen Size
     - Reference Resolution: 1920x1080
     - Match: 0.5 (balance width/height)

4. **Create Boost Text**
   - Right-click Canvas → UI → Text - TextMeshPro
   - Name: "BoostText"
   - Position: Top-center of screen
   - Rect Transform:
     - Anchor: Top-Center
     - Pos X: 0, Pos Y: -50
     - Width: 300, Height: 60
   - TextMeshPro settings:
     - Text: "SPEED BOOST!"
     - Font Size: 40
     - Alignment: Center
     - Color: Yellow (#FFFF00)
     - Font Style: Bold

5. **Add UI Reference to Driver Script**
   ```csharp
   using TMPro;  // Add this at top
   
   public class Driver : MonoBehaviour
   {
       [Header("Speed Settings")]
       [SerializeField] float currentSpeed = 5f;
       [SerializeField] float steerSpeed = 200f;
       [SerializeField] float boostSpeed = 10f;
       [SerializeField] float regularSpeed = 5f;
       
       [Header("UI")]
       [SerializeField] TMP_Text boostText;
       
       void Start()
       {
           currentSpeed = regularSpeed;
           boostText.gameObject.SetActive(false);  // Hide at start
       }
   }
   ```

6. **Connect UI in Inspector**
   - Select Car GameObject
   - Driver script → Boost Text field
   - Drag BoostText UI element into field

7. **Show/Hide UI on Boost**
   ```csharp
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.CompareTag("Boost"))
       {
           currentSpeed = boostSpeed;
           boostText.gameObject.SetActive(true);  // Show text
           Destroy(collision.gameObject);
       }
   }
   
   void OnCollisionEnter2D(Collision2D collision)
   {
       if (collision.collider.CompareTag("WorldCollision"))
       {
           currentSpeed = regularSpeed;
           boostText.gameObject.SetActive(false);  // Hide text
       }
   }
   ```

8. **Additional UI Elements (Optional)**
   Create:
   - Score counter
   - Deliveries completed
   - Timer
   - Instructions

   Example Score Text:
   ```csharp
   [SerializeField] TMP_Text scoreText;
   int score = 0;
   
   void Start()
   {
       UpdateScoreUI();
   }
   
   void UpdateScoreUI()
   {
       scoreText.text = "Score: " + score;
   }
   
   // In Delivery.cs
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.CompareTag("Customer") && hasPackage)
       {
           score += 100;
           UpdateScoreUI();
       }
   }
   ```

**💡 Key Takeaway**: TextMeshPro provides high-quality, performant UI text. Always use TMP instead of legacy UI Text!

---

## **Section 24: Complete Delivery System**

### Learning Objectives
- Finalize package pickup/delivery system
- Add visual feedback
- Polish gameplay loop

### Steps

1. **Final Delivery Script**
   ```csharp
   using UnityEngine;
   
   public class Delivery : MonoBehaviour
   {
       [Header("Package Settings")]
       [SerializeField] bool hasPackage = false;
       [SerializeField] float destroyDelay = 0.5f;
       [SerializeField] Color packageColor = Color.yellow;
       [SerializeField] Color normalColor = Color.white;
       
       SpriteRenderer spriteRenderer;
       ParticleSystem packageParticles;
       
       void Start()
       {
           spriteRenderer = GetComponent<SpriteRenderer>();
           packageParticles = GetComponent<ParticleSystem>();
       }
       
       void OnTriggerEnter2D(Collider2D collision)
       {
           // Pick up package
           if (collision.CompareTag("Package") && !hasPackage)
           {
               Debug.Log("Picked up package");
               hasPackage = true;
               spriteRenderer.color = packageColor;
               packageParticles.Play();
               Destroy(collision.gameObject, destroyDelay);
           }
           
           // Deliver to customer
           if (collision.CompareTag("Customer") && hasPackage)
           {
               Debug.Log("Delivered package!");
               hasPackage = false;
               spriteRenderer.color = normalColor;
               packageParticles.Stop();
               Destroy(collision.gameObject);
           }
       }
   }
   ```

2. **Add Particle Effects**
   - Select Car
   - Configure Particle System:
     ```
     Main Module:
     - Start Color: Yellow (for package)
     - Start Size: 0.3
     - Start Speed: 1
     - Start Lifetime: 1
     
     Emission:
     - Rate over Time: 20
     
     Shape:
     - Shape: Circle
     - Radius: 0.5
     ```

3. **Color Feedback System**
   - Car changes color when carrying package
   - Helps player know current state
   - Visual = intuitive gameplay

4. **Create Multiple Delivery Routes**
   - Place 3-5 Package/Customer pairs
   - Customer positions marked clearly
   - Packages spread around map

5. **Test Complete Loop**
   1. Drive to package (trigger enters)
   2. Package destroyed after delay
   3. Car color changes
   4. Particles activate
   5. Drive to customer
   6. Customer destroyed
   7. Car returns to normal
   8. Ready for next delivery

**💡 Key Takeaway**: Complete game loops with clear feedback create satisfying gameplay. Players should always know their current state and objectives.

---

## **Section 25: Polish & Optimization**

### Learning Objectives
- Add audio feedback
- Optimize performance
- Final polish pass

### Steps

1. **Add Sound Effects**
   - Import audio files:
     - Engine sound (looping)
     - Pickup sound
     - Delivery sound
     - Collision sound
     - Boost sound

2. **Configure Audio**
   ```csharp
   [Header("Audio")]
   [SerializeField] AudioSource engineSound;
   [SerializeField] AudioClip pickupSound;
   [SerializeField] AudioClip deliverySound;
   [SerializeField] AudioClip collisionSound;
   
   void Start()
   {
       engineSound.Play();  // Loop engine sound
   }
   
   void OnTriggerEnter2D(Collider2D collision)
   {
       if (collision.CompareTag("Package"))
       {
           AudioSource.PlayClipAtPoint(pickupSound, transform.position);
       }
   }
   ```

3. **Performance Optimization**
   - Use object pooling for frequently spawned objects
   - Combine sprites into atlas
   - Use Composite Collider for tilemaps
   - Cache GetComponent calls
   - Disable particle systems when off-screen

4. **Visual Polish**
   - Add dust particles when driving
   - Screen shake on collision
   - Camera smoothing adjustments
   - Better sprite animations (optional)

5. **Gameplay Tuning**
   - Test all speed values
   - Ensure level is beatable
   - Balance difficulty curve
   - Add checkpoints (optional)

**💡 Key Takeaway**: Polish separates good games from great games. Small details (sounds, particles, feedback) create professional feel.

---

## **Section 26: Wrap Up & Next Steps**

### What You've Learned

**Programming Concepts:**
- Methods and functions
- Variables and data types
- Conditional statements (if/else)
- Boolean logic
- Time-based calculations

**Unity Systems:**
- Transform manipulation
- Input handling
- Physics (Colliders, Rigidbodies, Triggers)
- Tag system
- Prefab workflow
- Component architecture (GetComponent)
- Particle systems
- UI with TextMeshPro

**Game Development:**
- Player control systems
- Pickup/delivery mechanics
- State management
- Visual feedback
- Level design basics

### Project Extensions

**Easy Additions:**
1. Score system with UI counter
2. Timer countdown
3. Multiple levels
4. Sound effects and music
5. Win/lose conditions

**Medium Challenges:**
1. AI customer movement
2. Multiple package types
3. Upgrade system
4. Save/load game state
5. Dynamic difficulty

**Advanced Features:**
1. Minimap system
2. Traffic obstacles
3. Weather effects
4. Leaderboard
5. Mobile controls

### Resources for Continued Learning

- Unity Manual: docs.unity3d.com
- Unity Learn: learn.unity.com
- C# Documentation: docs.microsoft.com/dotnet/csharp
- Game Dev communities: Reddit r/gamedev, Unity forums

---

## **Common Issues & Solutions**

### Input Not Working
- ✅ Input System package installed?
- ✅ Using `UnityEngine.InputSystem`?
- ✅ Script attached to GameObject?

### Collisions Not Detected
- ✅ Both objects have Colliders?
- ✅ At least one has Rigidbody2D?
- ✅ Colliders not marked as triggers (unless intended)?
- ✅ Objects on same Z-axis (2D)?

### Triggers Not Working
- ✅ Collider marked "Is Trigger"?
- ✅ At least one has Rigidbody2D?
- ✅ Using OnTriggerEnter2D (not OnTriggerEnter)?

### UI Not Showing
- ✅ Canvas in scene?
- ✅ EventSystem in scene?
- ✅ UI element active?
- ✅ Camera rendering UI layer?

### Movement Too Fast/Slow
- ✅ Using Time.deltaTime?
- ✅ Speed values reasonable (5-15 typically)?
- ✅ Fixed Timestep correct? (Edit → Project Settings → Time)

### Objects Not Destroying
- ✅ Correct GameObject reference?
- ✅ Not destroying too early?
- ✅ No null reference errors?

---

## **Quick Reference Card**

### Essential Code Snippets

**Movement:**
```csharp
transform.Translate(x, y, 0);
transform.Rotate(0, 0, angle);
```

**Input:**
```csharp
if (Keyboard.current.wKey.isPressed) { }
```

**Collision:**
```csharp
void OnCollisionEnter2D(Collision2D collision) { }
```

**Trigger:**
```csharp
void OnTriggerEnter2D(Collider2D collision) { }
```

**Tags:**
```csharp
if (collision.CompareTag("Package")) { }
```

**Destroy:**
```csharp
Destroy(gameObject);
Destroy(gameObject, delay);
```

**Components:**
```csharp
GetComponent<ComponentType>()
```

**UI:**
```csharp
tmpText.text = "New Text";
gameObject.SetActive(false);
```

---

## **Congratulations!**

You've completed the Delivery Dash tutorial and learned fundamental Unity 2D game development skills. These concepts form the foundation for more complex games. Keep practicing, experimenting, and building!

**Next Project: TileMania** (2D platformer mechanics)
