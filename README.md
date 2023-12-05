- 👋 Hi, I’m @Huker07
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Huker07/Huker07 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pygame
import sys
import random

# Initialize the game
pygame.init()

# Set the game window size
width = 640
height = 480

# Create the game window
screen = pygame.display.set_mode((width, height))

# Set the title of the game window
pygame.display.set_caption('Snake Game')

# Load the snake image
snake_img = pygame.image.load('snake.png')

# Load the food image
food_img = pygame.image.load('food.png')

# Initialize the game clock
clock = pygame.time.Clock()

# Game variables
snake_size = 20
snake_speed = 15

# Snake coordinates
snake_coords = [[100, 50], [90, 50], [80, 50]]
snake_direction = 'RIGHT'

# Food coordinates
food_coords = [random.randint(0, (width//snake_size)) * snake_size, random.randint(0, (height//snake_size)) * snake_size]

# Main game loop
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Check for arrow key presses
    keys = pygame.key.get_pressed()
    if keys[pygame.K_UP] and snake_direction != 'DOWN':
        snake_direction = 'UP'
    if keys[pygame.K_DOWN] and snake_direction != 'UP':
        snake_direction = 'DOWN'
    if keys[pygame.K_LEFT] and snake_direction != 'RIGHT':
        snake_direction = 'LEFT'
    if keys[pygame.K_RIGHT] and snake_direction != 'LEFT':
        snake_direction = 'RIGHT'

    # Update the snake's position
    if snake_direction == 'UP':
        snake_coords.insert(0, [snake_coords[0][0], snake_coords[0][1] - snake_size])
    if snake_direction == 'DOWN':
        snake_coords.insert(0, [snake_coords[0][0], snake_coords[0][1] + snake_size])
    if snake_direction == 'LEFT':
        snake_coords.insert(0, [snake_coords[0][0] - snake_size, snake_coords[0][1]])
    if snake_direction == 'RIGHT':
        snake_coords.insert(0, [snake_coords[0][0] + snake_size, snake_coords[0][1]])

    # Check for collisions with the food
    if snake_coords[0] == food_coords:
        food_coords = [random.randint(0, (width//snake_size)) * snake_size, random.randint(0, (height//snake_size)) * snake_size]
    else:
        snake_coords.pop()

    # Check for collisions with the walls or the snake's tail
    if snake_coords[0][0] < 0 or snake_coords[0][0] >= width or snake_coords[0][1] < 0 or snake_coords[0][1] >= height:
        print('Game Over')
        pygame.quit()
        sys.exit()
    for i in range(1, len(snake_coords)):
        if snake_coords[0] == snake_coords[i]:
            print('Game Over')
            pygame.quit()
            sys.exit()

    # Draw the snake and food on the screen
    screen.fill((0, 0, 0))
    for coord in snake_coords:
        screen.blit(snake_img, (coord[0], coord[1]))
    screen.blit(fo
