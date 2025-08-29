## 🎮 Tutorial 1 – Creating a 2D Platformer

**Goal:** Build a simple 2D platformer where a character can run, jump, and interact with the environment.  

**Steps:**
1. Open Godot and create a new 2D project.  
2. Add a `KinematicBody2D` node → rename it `Player`.  
3. Attach a script to handle **movement & jumping**:  
   ```gdscript
   extends KinematicBody2D
   
   var speed = 200
   var gravity = 900
   var jump_force = -400
   var velocity = Vector2.ZERO
   
   func _physics_process(delta):
       velocity.y += gravity * delta
       velocity.x = Input.get_action_strength("ui_right") - Input.get_action_strength("ui_left")
       velocity.x *= speed
       
       if is_on_floor() and Input.is_action_just_pressed("ui_up"):
           velocity.y = jump_force
       
       velocity = move_and_slide(velocity, Vector2.UP)