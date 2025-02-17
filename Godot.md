#game #dev 

# Installation

- Download Latest Godot from [Official Website](https://godotengine.org/)
- Initiate a 2D project (with git) to get started.
- Create three folders and import downloaded **assets**.

```
brackeys-2d-tutorial on  main [?]
❯ tree
.
├── assets
│   ├── fonts
│   ├── music
│   ├── sounds
│   └── sprites
├── scenes
└── scripts
```

---
# How Godot Works

- **Node**: A building block of a game (e.g., Sprite, TileMap, Camera, Physics, etc).
- **Scene**: A collection of nodes that function as a unit (e.g., a player, level, or UI).
- **Nesting**: Scenes can be made up of multiple nodes and nested inside other scenes.
- **Scene Tree**: A hierarchy where nodes are structured, with changes in one scene reflecting across all instances in the game.

---
# Player 1.0

1. Create a the game root scene:
	- Add Root Node 2D and save renamed Game root scene in its directory.
2. Set up player scene:
	- Create new scene with node `cmd + A` named `CharacterBody2D`.
	- Add another node named `AnimatedSprite2D` to add graphics to that character.
	- On the right, select `Sprite Frames` under Animation tab of inspector, and add a new sprite frame.
	- Add new frames to sprite sheet, resize to match your assets, and add sequentially.
	- Change texture to nearest inside project settings for crisp pixel art.
	- Adjust animation name, fps, autoplay and position.
	- Since physics nodes need shape to interact with objects, add `CollisionShape2D` node with circle shape under characterBody2D.
	- Save `player` scene and drag to `game` scene.
3. Integrate player into game:
	- Add a `Camera2D` node to `game` scene and adjust zoom. Build to see progress.
	- Add default script to `player` scene.

Building will make player fall off due to no floor collision. Add a `StaticBody2D` node with `WorldBoundaryShape2D` inside game script. Now you can move around with arrow keys and jump with space.

---
# World Building 1.0

We can start by deleting the temporary `StaticBody2D` group and use a `TileMap` node.

![[Screenshot 2025-02-13 at 3.45.51 PM.png]]

**TileSet**: Collection of tiles to paint from.
**TileMap**: Node used to paint tiles into our game.

- Select TileSet on inspector tab of TileMap. Adjust size.
- Drag tile asset to TileSet option at the bottom and select yes.
- Setup TileSet by erase wrong tiles and selecting one big tile by holding `shift`.

Now you can create an entire map for your game. But no collision.

- Add a new element in physics layer under TileSet in inspector tab. Now add physics to tiles by going to TileSet (bottom) and painting tiles with physics layer 0.
- `C` to clear physics. `F` to fill. Custom hit box per tile by cropping.

Now player can interact with the environment. But camera isn't following him.

Add camera to as a child of player node and smoothen it. 

---
# Platform 1.0

### Static Platforms

- Create a new scene with `AnimatableBody2D` as the root node.
- Add a `Sprite2D` node as a child.
- Drag the platform sprite into the Texture property of the Sprite2D.
- Enable "Region" in the Sprite2D properties and adjust the region to show only one platform tile.
- Add a `CollisionShape2D` node and set its shape to a rectangle matching the platform's size. Also able "One way collision" if you wanna jump on it from below.
- Rename the root node to "Platform" and save the scene.
- Instance the platform in your main scene as needed.
### Moving Platforms

- Select an instanced platform in your main scene.
- Add an `AnimationPlayer` node as a child of the platform.
- Create a new animation named "move" at bottom.
- Create a key frame for Platform 2 at position under transition tab.
- Set the animation length (e.g., 2 seconds).
- Create keyframe at 1s after adjusting the platform's position.
- Enable "Loop" mode in the AnimationPlayer.
- Set "Autoplay" to "move" in the AnimationPlayer properties.

---
# Pickups

### Coin Pickup

- Create a new scene with `Area2D` as the root node. (to only *detect* if colliding)
- Add an `AnimatedSprite2D` node as a child.
- Create new SpriteFrames for the coin animation.
- Add frames from the coin sprite sheet to create the animation.
- Set the animation to autoplay and adjust the speed as needed.
- Add a `CollisionShape2D` node and set its shape to a circle.
- Rename the root node to "Coin" and save the scene.
- Create a script for the Coin scene
- Delete default boilerplate and select node tab inside coin script. Connect `on_body_entered()` to detect coins colliding with any body (including moving platforms).
- Set player to 2nd physics layer and coin to 2nd mask, to only detect player and coin collision.
- Detect collision coin using `queue_free()`.

```gdscript
extends Area2D

func _on_body_entered(body: Node2D) -> void:
	queue_free() # coins 1+
```

---
# Dying 1.0

### Death Cam

- Set a below limit to `Camera2D` to prevent camera from following player to its death.

### Kill Zone

- Create a new scene with `Area2D` as the root node.
- Add a `CollisionShape2D` node and set its shape to world boundary to cover the area where the player should die (e.g., bottom of the screen).
- Rename the root node to "KillZone" and save the scene.
- Set it's mask to 2nd second to detect player collision.
- Create a script for the KillZone with `on_body_entered()`:
- Add a `Timer` to restart game after delay. Drag and drop with node to script while pressing `cmd`. Finally connect to `time_out` signal. Can adjust wait time.

```gdscript
extends Area2D

@onready var timer: Timer = $Timer

func _on_body_entered(body: Node2D) -> void:
	print("YOU DIED!")
	timer.start()

func _on_timer_timeout() -> void:
	get_tree().reload_current_scene()
```

---
# World Building 2.0

- Clean up scene tree by adding empty node named coins and platforms.
- Add a new background layer inside inspection tab of `TileMap` and fill up as you desire.

---
# Enemy

