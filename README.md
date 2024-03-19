import pygame
import sys

# Initialize Pygame
pygame.init()

# Set up the screen
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Highlighted Players")

# Define colors
WHITE = (255, 255, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)

# Player class
class Player(pygame.sprite.Sprite):
    def __init__(self, color, x, y):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(color)
        self.rect = self.image.get_rect()
        self.rect.center = (x, y)

# Object class (e.g., an obstacle)
class Obstacle(pygame.sprite.Sprite):
    def __init__(self, color, x, y, width, height):
        super().__init__()
        self.image = pygame.Surface((width, height))
        self.image.fill(color)
        self.rect = self.image.get_rect()
        self.rect.center = (x, y)

# Create players
player = Player(WHITE, 400, 300)

# Create obstacles
obstacle = Obstacle(GREEN, 500, 350, 200, 50)

# Add players and obstacles to sprite groups
all_sprites = pygame.sprite.Group()
all_sprites.add(player, obstacle)

# Main game loop
running = True
while running:
    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Check if player is behind or in front of the obstacle
    if player.rect.bottom < obstacle.rect.top:
        player_color = RED  # Player is behind obstacle
    else:
        player_color = GREEN  # Player is in front of obstacle

    # Highlight player accordingly
    player.image.fill(player_color)

    # Update screen
    screen.fill((0, 0, 0))
    all_sprites.draw(screen)
    pygame.display.flip()

    # Limit frame rate
    pygame.time.delay(100)

# Quit Pygame
pygame.quit()
sys.exit()
