# Delivery Dash - Student Progress Checklist
## CS 4700: Game Design Studio 4 | Mini-Project 1

**Student Name:** _________________________  **Date Started:** __________

---

## 📋 Section Completion Tracker

### Part 1: Fundamentals (Sections 1-6)
- [ ] **Section 1**: Project Setup & Introduction 
  - Project created and organized
  - Initial scene saved
  
- [ ] **Section 2**: Introducing Methods 
  - Driver script created
  - Start() and Update() understood
  - Debug.Log tested
  
- [ ] **Section 3**: Transform.Translate() 
  - Basic movement implemented
  - Coordinate system understood
  
- [ ] **Section 4**: Introducing Variables
  - Speed variable declared
  - Different variable types explored
  
- [ ] **Section 5**: Using SerializeField 
  - Variables visible in Inspector
  - Can adjust values in Unity
  
- [ ] **Section 6**: Keyboard Input & If Statements 
  - Input System package installed
  - WASD controls working
  - Conditional logic implemented


---

### Part 2: Movement & Physics (Sections 7-11)
- [ ] **Section 7**: Moving Our Car 
  - Combined movement and rotation
  - Smooth car controls
  
- [ ] **Section 8**: Using Time.deltaTime 
  - Frame-rate independent movement
  - Speed values adjusted
  
- [ ] **Section 9**: Colliders & Rigidbodies 
  - Car has sprite, collider, and rigidbody
  - Basic collision working
  
- [ ] **Section 10**: OnCollisionEnter2D()
  - Collision detection in code
  - Response to obstacles
  
- [ ] **Section 11**: OnTriggerEnter2D() 
  - Trigger system understood
  - Package pickup prototype working


---

### Part 3: Camera & Assets (Sections 12-14)
- [ ] **Section 12**: Introducing Cinemachine 
  - Cinemachine installed
  - Virtual camera following car
  
- [ ] **Section 13**: Add Assets To Project 
  - All sprites imported
  - Assets organized properly
  
- [ ] **Section 14**: Car & Background 
  - Car sprite applied
  - Background/environment set up
  - Sprite layers configured


---

### Part 4: Level Design (Sections 15-17)
- [ ] **Section 15**: Create A Level (15 min)
  - Tilemap system set up
  - Basic road layout created
  
- [ ] **Section 16**: Add Collision Blocks (10 min)
  - Tilemap collision working
  - Boundary walls created
  
- [ ] **Section 17**: Using Tags In Unity (12 min)
  - Custom tags created
  - Tag-based detection implemented
  - Code uses CompareTag()



---

### Part 5: Game Mechanics (Sections 18-22)
- [ ] **Section 18**: Introducing Bools 
  - hasPackage state tracking
  - Boolean logic understood
  
- [ ] **Section 19**: Introducing Prefabs 
  - Package prefab created
  - Multiple prefabs in use
  - Prefab editing understood
  
- [ ] **Section 20**: How To Destroy Objects 
  - Destroy() implemented
  - Delayed destruction working
  
- [ ] **Section 21**: Using GetComponent 
  - Particle system controlled from code
  - Component references cached
  
- [ ] **Section 22**: Boosts & Bumps 
  - Speed boost mechanic working
  - Collision slowdown implemented

---

### Part 6: UI & Polish (Sections 23-26)
- [ ] **Section 23**: Adding UI Text
  - TextMeshPro installed
  - Boost text working
  - UI updates from code
  
- [ ] **Section 24**: Complete Delivery System
  - Full pickup/delivery loop
  - Visual feedback (color, particles)
  - Multiple packages/customers
  
- [ ] **Section 25**: Polish & Optimization 
  - Sound effects added
  - Performance optimized
  - Final polish pass
  
- [ ] **Section 26**: Wrap Up & Documentation (Variable)
  - Code reviewed and commented
  - README/documentation written
  - Build created

---

## 🎯 Core Mechanics Checklist

### Movement System
- [ ] Car moves forward/backward (W/S)
- [ ] Car rotates left/right (A/D)
- [ ] Movement smooth and frame-rate independent
- [ ] Speed values feel appropriate

### Collision System
- [ ] Car collides with walls/obstacles
- [ ] Car can't drive off map
- [ ] Collision slows car to regular speed

### Pickup System
- [ ] Packages have trigger colliders
- [ ] Car picks up package on contact
- [ ] Can only carry one package at a time
- [ ] Visual feedback when carrying package

### Delivery System
- [ ] Customers have trigger colliders
- [ ] Can only deliver when carrying package
- [ ] Customer disappears after delivery
- [ ] Car returns to normal state

### Boost System
- [ ] Boost pads trigger speed increase
- [ ] Boost pads destroyed on collection
- [ ] Speed resets on collision
- [ ] UI shows boost status

---

## 📊 Quality Standards

### Code Quality
- [ ] All variables have clear names (camelCase)
- [ ] SerializeField used appropriately
- [ ] GetComponent calls cached when possible
- [ ] No commented-out debug code in final version
- [ ] Code organized and readable
- [ ] Comments explain complex logic

### Visual Polish
- [ ] Sprites clearly visible and appropriately scaled
- [ ] Camera follows smoothly
- [ ] Particle effects play at right times
- [ ] UI elements properly positioned
- [ ] Colors provide clear feedback

### Level Design
- [ ] Level is completable
- [ ] 3-5 package/customer pairs
- [ ] 5-10 boost pads strategically placed
- [ ] Obstacles provide challenge but not frustration
- [ ] Clear visual distinction between elements

### User Experience
- [ ] Controls feel responsive
- [ ] Player always knows current objective
- [ ] Feedback for all player actions
- [ ] No confusing game states
- [ ] Win condition clear

---

## 🚀 Extension Features (Optional)

### Easy Extensions (Pick 2-3)
- [ ] Score counter for completed deliveries
- [ ] Timer countdown
- [ ] Multiple difficulty levels
- [ ] More particle effects
- [ ] Additional sound effects
- [ ] Background music

### Medium Extensions (Pick 1-2)
- [ ] Second level
- [ ] Different package types (colors, points)
- [ ] Obstacles that move
- [ ] Power-up variety (shield, jump, etc.)
- [ ] Combo system for fast deliveries

### Advanced Extensions (Challenge yourself!)
- [ ] Minimap system
- [ ] Traffic/NPC cars
- [ ] Day/night cycle
- [ ] Mobile touch controls
- [ ] Save/load system

---

## 📝 Submission Checklist

### Required Files
- [ ] Unity project folder (zipped)
- [ ] Playable build (Windows, Mac, or WebGL)
- [ ] Design document (PDF)
- [ ] Video demo (2-3 minutes)
- [ ] README with controls and features

### Design Document Sections
- [ ] Game title and description (1 paragraph)
- [ ] Controls explanation
- [ ] Core mechanics breakdown
- [ ] Features implemented list
- [ ] Challenges faced and solutions
- [ ] What you learned
- [ ] Future improvements (if time permitted)

### Video Demo Content
- [ ] Shows title/start screen
- [ ] Demonstrates basic movement
- [ ] Shows package pickup
- [ ] Shows delivery to customer
- [ ] Demonstrates boost mechanic
- [ ] Shows collision behavior
- [ ] Highlights any unique features

### Code Submission
- [ ] All scripts included
- [ ] No missing references in Inspector
- [ ] Project runs without errors
- [ ] Build tested and works
- [ ] Assets properly organized


---

## 💡 Key Concepts Mastered

After completing this project, check off concepts you understand:

### C# Programming
- [ ] Methods (Start, Update, custom)
- [ ] Variables (int, float, bool, string)
- [ ] SerializeField attribute
- [ ] If/else conditional statements
- [ ] Boolean operators (&&, ||, !)
- [ ] Method parameters and return values

### Unity Fundamentals
- [ ] GameObject and Component architecture
- [ ] Transform (position, rotation, scale)
- [ ] Translate() and Rotate()
- [ ] Time.deltaTime
- [ ] Tag system
- [ ] GetComponent<>()
- [ ] Destroy()

### Physics System
- [ ] Collider2D (Box, Circle, Polygon)
- [ ] Rigidbody2D (Dynamic, Kinematic, Static)
- [ ] OnCollisionEnter2D()
- [ ] OnTriggerEnter2D()
- [ ] Trigger vs Collision

### Unity Systems
- [ ] Input System (Keyboard)
- [ ] Sprite Renderer and layers
- [ ] Particle System basics
- [ ] Cinemachine virtual camera
- [ ] Tilemap and Tile Palette
- [ ] Composite Collider
- [ ] Prefab workflow

### UI Development
- [ ] Canvas and UI scaling
- [ ] TextMeshPro
- [ ] SetActive() for showing/hiding
- [ ] Updating UI from code

---

## 🎓 Reflection Questions

Answer these after completing the project:

1. **What was the most challenging part of this project?**
   
   _____________________________________________________________

2. **What concept finally "clicked" for you?**
   
   _____________________________________________________________

3. **What would you do differently if you started over?**
   
   _____________________________________________________________

4. **What feature are you most proud of?**
   
   _____________________________________________________________

5. **What will you research/learn next?**
   
   _____________________________________________________________

---

## 📚 Resources Used

Track helpful resources you discovered:

- [ ] Unity Manual: ____________________________________________
- [ ] Tutorial Videos: ________________________________________
- [ ] Forums/Discussions: _____________________________________
- [ ] Documentation: __________________________________________
- [ ] Classmate Help: _________________________________________

---

## ✅ Final Self-Assessment

Rate your understanding (1-5 scale, 5 being expert):

| Concept | Rating | Notes |
|---------|--------|-------|
| C# Basics | ___/5 | |
| Unity Editor | ___/5 | |
| Physics System | ___/5 | |
| Input Handling | ___/5 | |
| UI Implementation | ___/5 | |
| Game Design | ___/5 | |

**Overall Confidence:** ___/5

**Ready for next project (TileMania)?** ☐ Yes ☐ Need more practice

---

## 🎮 Play Testing Notes

Have 2-3 people play your game and record feedback:

**Tester 1:** _____________________
- Controls feel: ☐ Easy ☐ Medium ☐ Difficult
- Most fun part: _________________________________________
- Suggestions: __________________________________________

**Tester 2:** _____________________
- Controls feel: ☐ Easy ☐ Medium ☐ Difficult
- Most fun part: _________________________________________
- Suggestions: __________________________________________

**Tester 3:** _____________________
- Controls feel: ☐ Easy ☐ Medium ☐ Difficult
- Most fun part: _________________________________________
- Suggestions: __________________________________________

---

**Completed Date:** __________  
**Grade Received:** __________  
**Instructor Feedback:**

