#python #game #dev 

# Installation

1. Download and install `python` from [python.org].
2. Install `pygame` using `pip`.

```zsh
pip3 install pygame
```

---
# Getting Started

```python
import pygame
from sys import exit # closes entire code

pygame.init()

screen = pygame.display.set_mode((800, 600)) # set resolution
pygame.display.set_caption("Dark Souls") # window name
clock = pygame.time.Clock()

while True: # rendering until QUIT
    for event in pygame.event.get(): # check all events
        if event.type == pygame.QUIT: # red cross click
            pygame.quit()
            exit()
    # draw all our elements
    # update everything
    pygame.display.update()
    clock.tick(60) # frame rate
```

---
# Surface

3. **Display Surface**:
	- The game window.
	- Is always displayed.
	- Must be unique.
4. **(regular) surface:**
	- A single image (imported), color, text.
	- Needs to be on *display surface* to be visible.
	- Flexible amount.

#### **`blit`**: block image transfer

```python
# sky_suface = pygame.image.load("graphics/Sky.png")
screen = pygame.display.set_mode((800, 600))
text_surface = pygame.Surface((200, 200))
text_surface.fill('Green')

while True:
	screen.blit(text_surface, (20, 50))
```

Rendering `text_surface` at $[20, 50]$ on display surface.

![[Screenshot 2025-01-28 at 11.17.26 PM.png]]
Notice, `text_surface` renders 20px to left and 50px down. Hence,

> In `pygame` coordinates starts from $[0, 0]$ at top left and $x$ goes from left to right, while $y$ goes from up to down.

#### Render Text

Anti-aliasing : Smooth edges

```python
test_font = pygame.font.Font("font/Pixeltype.ttf", 50) # None, default
text_surface = test_font.render("my text", False, 'Black')

while True:
    screen.blit(text_surface, (150, 50))
```

---
# Animation

Animations in `pygame` are achieved by cycling through a sequence of images (frames) over time. Example: Snail Rendering and Animation

```python
screen.blit(img[snail_index // 5], (snail_x, GROUND_Y - img[0].get_height()))
snail_index = (snail_index + 1) % 10

snail_x -= SNAIL_SPEED
if snail_x < -snail_width:
	snail_x = WINDOW_WIDTH
```

Here we are changing snail frame at $5$ fps using `snail_index`. And are changing snail's x-coordinate at `SNAIL_SPEED` to make it infinitely loop from end to start.

> [!note]
> Be sure update background when animating, otherwise we get strange lagging results.

### `convert() and convert.alpha()`

Use `convert()` for solid background and `convert.alpha()` while loading images for better optimization and faster gameplay when working with `pygame`.

---

# Rectangle

Useful for

1. Precise placement of surface.
2. Basic Collision.

By default, we place surface using top left co-ordinates. But that can get tricky. Use rectangles for easy access and placements.

![[Screenshot 2025-02-02 at 2.27.34 PM.png]]

```python
# uncommon method to draw a rectangle
# player_rect = pygame.Rect(left, top, width, height)

# Common: To draw a rect. around a surface
player_surf = pygame.image.load("graphics/Player/player_stand.png")
player_rect = player_surf.get_rect(topleft = (800, 200))

while True:
	screen.blit(player_surf, player_rect) # render
	player_rect.x += 1 # move
	if player_rect.right >= 800:
		player.rect.left = 0
```

---
# Collision

To check if `rect1` is colliding with `rect2`.

```python
rect1.colliderect(rect2) # returns 0 or 1
```

To check if `(x, y)` point collides with `rect`.

```python
rect.collidepoint((x, y))
```

---
## Mouse

To get position of mouse. Returns `(x, y)` co-ordinates.

```python
pygame.mouse.get_pos()
```

To get mouse buttons pressed. Returns `(True, False, False)` if left button pressed. Similarly for middle and right button.

```python
pygame.mouse.get_pressed()
```

To get position of mouse while moving.

```python
while True:
	for event in pygame.event.get():
		if event.type == pygame.MOUSEMOTION:
			print(event.pos) # (x, y)
```

To check if mouse button is pressed or released.

```python
while True:
    for event in pygame.event.get():
        if event.type == pygame.MOUSEBUTTONDOWN:
            print("mouse button was pressed")
        if event.type == pygame.MOUSEBUTTONUP:
            print("mouse button was released")
```

---
# Draw Rectangle with colors

To draw any shape of any size & color, use 
`pygame.draw.shape(surface, color, (x,y))`
`pygame.draw.shape(surface, color, (x,y), width, border radius)`

```python
pygame.draw.rect(screen, 'Pink', score_rect)
screen.blit(score_surf, score_rect) # before to blit text after background

pygame.draw.line(screen, 'Black', (0, 0), (800, 400))
```

![[Screenshot 2025-02-05 at 3.31.10 PM.png | 500]]

---
# Keyboard Inputs

To detect jumping

```python
while True:
    for event in pygame.event.get():
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE and not is_jumping:
	                is_jumping = True

    keys = pygame.key.get_pressed() # get all keys states
    if keys[pygame.K_SPACE]:
        print("Space is pressed rn!")
```

Can work with keydowns and key ups separately for more control.

---
# Time Management

