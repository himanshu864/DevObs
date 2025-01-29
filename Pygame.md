#python #game #dev 

# Installation

```zsh
python3 -m pip install pygame
```

Might have to create virtual environment.

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

1. **Display Surface**:
	- The game window.
	- Is always displayed.
	- Must be unique.
2. **(regular) surface:**
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

**Render Text**

Anti-aliasing : smooth edges

```python
test_font = pygame.font.Font("font/Pixeltype.ttf", 50) # None, default
text_surface = test_font.render("my text", False, 'Black')

while True:
    screen.blit(text_surface, (150, 50))
```

