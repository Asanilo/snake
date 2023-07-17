import pygame
import random

# 初始化游戏
pygame.init()

# 定义屏幕大小和颜色
screen_width = 640
screen_height = 480
bg_color = (0, 0, 0)
text_color = (255, 255, 255)

# 定义蛇的属性
snake_size = 20
snake_color = (0, 255, 0)

# 定义计分板属性
score = 0
font_size = 24

# 定义游戏难度
speed = 10

# 创建游戏窗口
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("贪吃蛇游戏")

clock = pygame.time.Clock()

# 加载字体
font = pygame.font.Font(None, font_size)

# 定义贪吃蛇的类
class Snake:
    def __init__(self):
        self.size = 1
        self.positions = [(screen_width // 2, screen_height // 2)]
        self.direction = random.choice([pygame.K_LEFT, pygame.K_RIGHT, pygame.K_UP, pygame.K_DOWN])

    def get_head_position(self):
        return self.positions[0]

    def update(self):
        cur = self.get_head_position()
        x, y = self.direction
        new = ((cur[0] + (x * snake_size)) % screen_width, (cur[1] + (y * snake_size)) % screen_height)
        if new in self.positions[2:]:
            self.reset()
        else:
            self.positions.insert(0, new)
            if len(self.positions) > self.size:
                self.positions.pop()
    
    def reset(self):
        self.size = 1
        self.positions = [(screen_width // 2, screen_height // 2)]
        self.direction = random.choice([pygame.K_LEFT, pygame.K_RIGHT, pygame.K_UP, pygame.K_DOWN])

    def render(self):
        for p in self.positions:
            pygame.draw.rect(screen, snake_color, (p[0], p[1], snake_size, snake_size))

# 定义食物的类
class Food:
    def __init__(self):
        self.position = (0,0)
        self.color = (255, 0, 0)
        self.randomize_position()

    def randomize_position(self):
        self.position = (random.randint(0, screen_width // snake_size - 1) * snake_size,
                         random.randint(0, screen_height // snake_size - 1) * snake_size)

    def render(self):
        pygame.draw.rect(screen, self.color, (self.position[0], self.position[1], snake_size, snake_size))

# 创建蛇和食物的实例
snake = Snake()
food = Food()

# 更新计分板
def update_score():
    score_text = font.render("Score: " + str(score), True, text_color)
    screen.blit(score_text, (10, 10))

# 游戏主循环
running = True
game_over = False
while running:
    while game_over:
        screen.fill(bg_color)
        game_over_text = font.render("Game Over!", True, text_color)
        restart_text = font.render("Press Enter to restart or Esc to quit.", True, text_color)
        screen.blit(game_over_text, (screen_width // 2 - 80, screen_height // 2 - 20))
        screen.blit(restart_text, (screen_width // 2 - 140, screen_height // 2 + 20))
        pygame.display.update()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
                game_over = False
            elif event.type == pygame.KEYDOWN:
                if event.key == pygame.K_RETURN:
                    snake.reset()
                    score = 0
                    speed = 10
                    game_over = False
                elif event.key == pygame.K_ESCAPE:
                    running = False
                    game_over = False

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT and snake.direction != (1, 0):
                snake.direction = (-1, 0)
            elif event.key == pygame.K_RIGHT and snake.direction != (-1, 0):
                snake.direction = (1, 0)
            elif event.key == pygame.K_UP and snake.direction != (0, 1):
                snake.direction = (0, -1)
            elif event.key == pygame.K_DOWN and snake.direction != (0, -1):
                snake
