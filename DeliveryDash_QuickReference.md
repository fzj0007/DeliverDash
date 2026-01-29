# Delivery Dash - Quick Reference Guide
## CS 4700: Essential Unity 2D Code Snippets

---

## 🎮 MOVEMENT & INPUT

### Basic Transform Movement
```csharp
// Move object
transform.Translate(x, y, 0);           // Local space
transform.Translate(x, y, 0, Space.World);  // World space

// Rotate object
transform.Rotate(0, 0, angle);

// With Time.deltaTime (ALWAYS USE THIS!)
float speed = 5f;
transform.Translate(0, speed * Time.deltaTime, 0);
```

### Keyboard Input (New Input System)
```csharp
using UnityEngine.InputSystem;  // Add at top

void Update()
{
    // Single key
    if (Keyboard.current.wKey.isPressed) { }
    
    // Multiple keys
    if (Keyboard.current.wKey.isPressed)
        move = 1f;
    else if (Keyboard.current.sKey.isPressed)
        move = -1f;
}
```

### Complete Car Controller Template
```csharp
using UnityEngine;
using UnityEngine.InputSystem;

public class Driver : MonoBehaviour
{
    [SerializeField] float moveSpeed = 5f;
    [SerializeField] float steerSpeed = 200f;
    
    void Update()
    {
        float move = 0f;
        float steer = 0f;
        
        // Get input
        if (Keyboard.current.wKey.isPressed) move = 1f;
        else if (Keyboard.current.sKey.isPressed) move = -1f;
        if (Keyboard.current.aKey.isPressed) steer = 1f;
        else if (Keyboard.current.dKey.isPressed) steer = -1f;
        
        // Apply movement
        float moveAmount = move * moveSpeed * Time.deltaTime;
        float steerAmount = steer * steerSpeed * Time.deltaTime;
        
        transform.Translate(0, moveAmount, 0);
        transform.Rotate(0, 0, steerAmount);
    }
}
```

---

## ⚙️ PHYSICS & COLLISION

### Collision Detection (Physical Barriers)
```csharp
void OnCollisionEnter2D(Collision2D collision)
{
    // Check what we hit
    Debug.Log("Hit: " + collision.gameObject.name);
    
    // Check by tag (RECOMMENDED)
    if (collision.collider.CompareTag("Wall"))
    {
        // Do something
    }
}

// Other collision methods:
void OnCollisionStay2D(Collision2D collision) { }   // While colliding
void OnCollisionExit2D(Collision2D collision) { }   // Stopped colliding
```

**Requirements for Collision:**
- Both objects need Collider2D
- At least one needs Rigidbody2D
- Neither collider is a trigger

### Trigger Detection (Pass-Through Zones)
```csharp
void OnTriggerEnter2D(Collider2D collision)
{
    // Check by tag
    if (collision.CompareTag("Package"))
    {
        Debug.Log("Picked up package!");
        Destroy(collision.gameObject);
    }
}

// Other trigger methods:
void OnTriggerStay2D(Collider2D collision) { }
void OnTriggerExit2D(Collider2D collision) { }
```

**Requirements for Triggers:**
- Both objects need Collider2D
- At least one needs Rigidbody2D
- At least one collider has "Is Trigger" checked

---

## 🏷️ TAGS & LAYERS

### Creating and Using Tags
```csharp
// Create tags: Inspector → Tag dropdown → Add Tag

// Check tag (FAST, RECOMMENDED)
if (collision.CompareTag("Package")) { }

// Check name (SLOW, NOT RECOMMENDED)
if (collision.gameObject.name == "Package") { }  // ❌ Avoid

// Find by tag
GameObject package = GameObject.FindGameObjectWithTag("Package");

// Find all with tag
GameObject[] enemies = GameObject.FindGameObjectsWithTag("Enemy");
```

**Common Tags:**
- Player, Enemy, Package, Customer, Boost, Wall, Ground

---

## 🎨 VARIABLES & SERIALIZATION

### Variable Types
```csharp
// Numbers
int score = 0;              // Whole numbers
float speed = 5.5f;         // Decimals (note the 'f')

// Logic
bool hasPackage = false;    // true or false

// Text
string playerName = "Alex"; // Text in quotes

// Unity types
Color carColor = Color.red;
Vector2 position = new Vector2(1, 2);
```

### SerializeField (Best Practice)
```csharp
// PRIVATE but visible in Inspector
[SerializeField] float speed = 5f;
[SerializeField] bool canJump = true;

// Organize with headers
[Header("Movement Settings")]
[SerializeField] float moveSpeed = 5f;
[SerializeField] float turnSpeed = 200f;

[Header("Jump Settings")]
[SerializeField] float jumpForce = 10f;
[SerializeField] int maxJumps = 2;
```

---

## 🎯 COMPONENTS

### GetComponent (Access Other Components)
```csharp
// Get component on SAME GameObject
SpriteRenderer sr = GetComponent<SpriteRenderer>();
Rigidbody2D rb = GetComponent<Rigidbody2D>();
ParticleSystem ps = GetComponent<ParticleSystem>();

// BEST PRACTICE: Cache in Start()
ParticleSystem particles;

void Start()
{
    particles = GetComponent<ParticleSystem>();
}

void SomeMethod()
{
    particles.Play();  // Use cached reference
}

// Get component from OTHER GameObject
SpriteRenderer otherSR = collision.GetComponent<SpriteRenderer>();
if (otherSR != null)  // Always check for null!
{
    otherSR.color = Color.red;
}
```

### Common Components
```csharp
// Transform (built-in, no GetComponent needed)
transform.position = new Vector3(0, 0, 0);
transform.rotation = Quaternion.identity;
transform.localScale = new Vector3(1, 1, 1);

// Sprite Renderer
GetComponent<SpriteRenderer>().color = Color.blue;
GetComponent<SpriteRenderer>().sprite = mySprite;

// Rigidbody2D
GetComponent<Rigidbody2D>().velocity = new Vector2(5, 0);
GetComponent<Rigidbody2D>().AddForce(new Vector2(100, 0));

// Particle System
GetComponent<ParticleSystem>().Play();
GetComponent<ParticleSystem>().Stop();

// Audio Source
GetComponent<AudioSource>().Play();
GetComponent<AudioSource>().PlayOneShot(clip);
```

---

## 💥 DESTROYING OBJECTS

### Destroy Methods
```csharp
// Destroy immediately
Destroy(gameObject);                    // This GameObject
Destroy(collision.gameObject);          // Other GameObject

// Destroy after delay
Destroy(gameObject, 2f);                // After 2 seconds
Destroy(collision.gameObject, 0.5f);    // After 0.5 seconds

// Destroy specific component
Destroy(GetComponent<SpriteRenderer>());
Destroy(this);  // Destroy this script only
```

**⚠️ Warning:** After calling Destroy(gameObject), the object still exists for the rest of the frame!

---

## 🎨 UI WITH TEXTMESHPRO

### Setup
```csharp
using TMPro;  // Add at top of script

public class UIManager : MonoBehaviour
{
    [SerializeField] TMP_Text scoreText;
    [SerializeField] TMP_Text boostText;
    int score = 0;
    
    void Start()
    {
        UpdateScoreText();
        boostText.gameObject.SetActive(false);  // Hide
    }
    
    void UpdateScoreText()
    {
        scoreText.text = "Score: " + score;
        // Or: scoreText.text = $"Score: {score}";  // String interpolation
    }
    
    void ShowBoost()
    {
        boostText.gameObject.SetActive(true);   // Show
    }
}
```

### Common UI Operations
```csharp
// Change text
tmpText.text = "New Text";
tmpText.text = "Score: " + score;
tmpText.text = $"Lives: {lives}/3";  // String interpolation

// Change color
tmpText.color = Color.red;
tmpText.color = new Color(1f, 0.5f, 0f);  // RGB (0-1)

// Show/Hide
tmpText.gameObject.SetActive(true);   // Show
tmpText.gameObject.SetActive(false);  // Hide

// Change font size
tmpText.fontSize = 48;
```

---

## 🎵 AUDIO

### Audio Source
```csharp
[SerializeField] AudioSource audioSource;
[SerializeField] AudioClip pickupSound;
[SerializeField] AudioClip crashSound;

void Start()
{
    audioSource.Play();  // Play/loop main audio
}

void OnTriggerEnter2D(Collider2D collision)
{
    // Play one-shot (doesn't interrupt main audio)
    audioSource.PlayOneShot(pickupSound);
    
    // Or play at point in world
    AudioSource.PlayClipAtPoint(crashSound, transform.position);
}
```

---

## ✨ PARTICLE SYSTEMS

### Controlling Particles
```csharp
ParticleSystem particles;

void Start()
{
    particles = GetComponent<ParticleSystem>();
    particles.Stop();  // Don't play at start
}

void OnTriggerEnter2D(Collider2D collision)
{
    if (collision.CompareTag("Package"))
    {
        particles.Play();               // Start playing
        // particles.Stop();            // Stop playing
        // particles.Clear();           // Clear all particles
        // particles.Pause();           // Pause
    }
}
```

---

## 📦 PREFABS

### Creating Prefabs
1. Set up GameObject perfectly in scene
2. Drag from Hierarchy to Project window
3. GameObject turns blue (prefab instance)

### Using Prefabs
```csharp
// Instantiate at runtime
[SerializeField] GameObject enemyPrefab;

void SpawnEnemy()
{
    Instantiate(enemyPrefab);  // At (0,0,0)
    
    // At specific position
    Instantiate(enemyPrefab, transform.position, Quaternion.identity);
    
    // With parent
    Instantiate(enemyPrefab, transform);
}
```

---

## 🎲 BOOLEAN LOGIC

### Comparison Operators
```csharp
if (score == 100)      // Equal to
if (score != 0)        // Not equal to
if (health > 0)        // Greater than
if (health < 100)      // Less than
if (speed >= 5)        // Greater than or equal
if (speed <= 10)       // Less than or equal
```

### Logical Operators
```csharp
// AND - Both must be true
if (hasKey && nearDoor) { }
if (grounded && !isJumping) { }

// OR - At least one must be true
if (pressingW || pressingUp) { }

// NOT - Inverts boolean
if (!hasPackage) { }  // Same as: if (hasPackage == false)
```

### Bool Flags for Game State
```csharp
bool hasPackage = false;
bool hasBoost = false;
bool isInvincible = false;

void OnTriggerEnter2D(Collider2D collision)
{
    // Only pick up if we don't have one
    if (collision.CompareTag("Package") && !hasPackage)
    {
        hasPackage = true;
    }
    
    // Only deliver if we have a package
    if (collision.CompareTag("Customer") && hasPackage)
    {
        hasPackage = false;  // Delivered!
        score += 100;
    }
}
```

---

## 🎬 UNITY LIFECYCLE METHODS

### Method Execution Order
```csharp
// Runs ONCE when object is created
void Awake() { }

// Runs ONCE before first frame
void Start() { }

// Runs EVERY frame (~60 times/second)
void Update() { }

// Runs EVERY fixed timestep (for physics)
void FixedUpdate() { }

// Runs EVERY frame AFTER Update
void LateUpdate() { }

// Runs when GameObject is destroyed
void OnDestroy() { }

// Runs when GameObject is disabled
void OnDisable() { }

// Runs when GameObject is enabled
void OnEnable() { }
```

**When to use each:**
- `Awake()`: Initialize references
- `Start()`: Initialize values (after Awake)
- `Update()`: Input, non-physics movement
- `FixedUpdate()`: Physics forces
- `LateUpdate()`: Camera following

---

## 🐛 DEBUGGING

### Console Logging
```csharp
// Basic logging
Debug.Log("Hello World");
Debug.Log("Score: " + score);
Debug.Log($"Position: {transform.position}");

// Warnings (yellow in Console)
Debug.LogWarning("Speed is too high!");

// Errors (red in Console)
Debug.LogError("Something broke!");

// Conditional logging
if (health <= 0)
    Debug.Log("Player died!");
```

### Visual Debugging
```csharp
// Draw lines in Scene view (not Game view)
void OnDrawGizmos()
{
    Gizmos.color = Color.red;
    Gizmos.DrawLine(start, end);
    Gizmos.DrawWireSphere(transform.position, 2f);
    Gizmos.DrawWireCube(transform.position, Vector3.one);
}
```

---

## ⚡ COMMON PATTERNS

### State Machine (Simple)
```csharp
enum GameState { Menu, Playing, Paused, GameOver }
GameState currentState = GameState.Menu;

void Update()
{
    switch (currentState)
    {
        case GameState.Menu:
            // Menu logic
            break;
        case GameState.Playing:
            // Game logic
            break;
        case GameState.Paused:
            // Pause logic
            break;
        case GameState.GameOver:
            // Game over logic
            break;
    }
}
```

### Timer Countdown
```csharp
[SerializeField] float timeRemaining = 60f;
[SerializeField] TMP_Text timerText;

void Update()
{
    if (timeRemaining > 0)
    {
        timeRemaining -= Time.deltaTime;
        timerText.text = $"Time: {timeRemaining:F1}";  // 1 decimal place
    }
    else
    {
        // Time's up!
        timeRemaining = 0;
        GameOver();
    }
}
```

### Cooldown System
```csharp
[SerializeField] float shootCooldown = 0.5f;
float nextShootTime = 0f;

void Update()
{
    if (Keyboard.current.spaceKey.isPressed && Time.time >= nextShootTime)
    {
        Shoot();
        nextShootTime = Time.time + shootCooldown;
    }
}
```

---

## 🎯 DELIVERY DASH COMPLETE TEMPLATE

### Delivery.cs
```csharp
using UnityEngine;

public class Delivery : MonoBehaviour
{
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
        if (collision.CompareTag("Package") && !hasPackage)
        {
            Debug.Log("Picked up package");
            hasPackage = true;
            spriteRenderer.color = packageColor;
            packageParticles.Play();
            Destroy(collision.gameObject, destroyDelay);
        }
        
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

### Driver.cs
```csharp
using UnityEngine;
using UnityEngine.InputSystem;
using TMPro;

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
        boostText.gameObject.SetActive(false);
    }
    
    void Update()
    {
        float move = 0f;
        float steer = 0f;
        
        if (Keyboard.current.wKey.isPressed) move = 1f;
        else if (Keyboard.current.sKey.isPressed) move = -1f;
        if (Keyboard.current.aKey.isPressed) steer = 1f;
        else if (Keyboard.current.dKey.isPressed) steer = -1f;
        
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
            boostText.gameObject.SetActive(true);
            Destroy(collision.gameObject);
        }
    }
    
    void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.collider.CompareTag("WorldCollision"))
        {
            currentSpeed = regularSpeed;
            boostText.gameObject.SetActive(false);
        }
    }
}
```

---

## 📖 QUICK TROUBLESHOOTING

| Problem | Solution |
|---------|----------|
| Input not working | Install Input System package, add `using UnityEngine.InputSystem;` |
| Collision not detected | Both need Colliders, one needs Rigidbody2D |
| Trigger not detected | Check "Is Trigger" on Collider, needs Rigidbody2D |
| Movement too fast | Multiply by Time.deltaTime |
| UI not showing | Check Canvas exists, UI element active, on correct layer |
| Null reference error | Check SerializeField assigned in Inspector |
| Object won't destroy | Check using correct reference (gameObject vs collision.gameObject) |
| Camera not following | Cinemachine Follow field assigned? |

---

## 🔧 USEFUL KEYBOARD SHORTCUTS

| Action | Windows | Mac |
|--------|---------|-----|
| Play/Stop | Ctrl + P | Cmd + P |
| Pause | Ctrl + Shift + P | Cmd + Shift + P |
| Focus GameObject | F | F |
| New GameObject | Ctrl + Shift + N | Cmd + Shift + N |
| Duplicate | Ctrl + D | Cmd + D |
| Delete | Delete | Delete |
| Save Scene | Ctrl + S | Cmd + S |
| Save Project | Ctrl + Shift + S | Cmd + Shift + S |

---

**Print this guide and keep it visible while coding!**
