#game #dev #python 

- Four types of data:
	- Bool
	- Int
	- Float
	- String
- Can typecast *dynamic* variables. Easy and flexible
- While *static* variables are Safe and Performant. Eg:
```gdscript
var damage: int = 15
# OR
var damage := 15
```

- Build-in functions, starts with `func _input()`, called by engine.
- Static functions:
```gdscript
func add(a: int, b: int) -> int:
	return a + b
```

- Random numbers:
```gdscript
const RNG = randf() # 0 to 1.
const A = randi_range(140, 200)
```

- Static arrays:
```gdscript
var arr: Array[String] = ["a", "b", "c"]
arr.remove_at(1)
arr.append("d")
```

- Looping arrays and dictionaries
```gdscript
func _ready():
	for i in 10:
		print(i)
	
	var charac = {
		"Enemy" : {"health": 100, "damage": 20},
		"Player": 12
	}

	for c in charac:
		print(c, charac[c])
```

**Enums**: is a datatype that contains a fixed set of Constants.

```gdscript
enum AnimationState {IDLE, JUMP, RUN}

var state = AnimationState.IDLE

@export var state : AnimationState
```

Can export enum defined variables to change using inspector.

**Match**: is switch-case of Godot.

```gdscript
enum AnimationState {IDLE, JUMP, RUN}

var animation = AnimationState.RUN

func _ready():
	match animation:
		AnimationState.IDLE:
			print("zzz")
		AnimationState.JUMP:
			print("weee")
		AnimationState.RUN:
			print("aahhhh")
		_:
			print("wtf")
```

`@onready` waits until all child nodes have been created.

`$path` is shorthand for writing `get_node("path")`

> Call down, signal up

