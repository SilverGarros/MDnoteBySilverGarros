#### 键盘监控

###### 使用 PyGame 库的代码

```py	
import pygame
import sys

# 初始化Pygame
pygame.init()

# 设置窗口大小和标题（可以忽略）
pygame.display.set_mode((100, 100))
pygame.display.set_caption("Keyboard Monitoring")

# 主循环
running = True
while running:
    # 处理事件
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # 获取当前按键状态
    keys = pygame.key.get_pressed()

    # 检测特定按键
    if keys[pygame.K_w]:
        print("W key pressed")
    if keys[pygame.K_s]:
        print("S key pressed")
    if keys[pygame.K_a]:
        print("A key pressed")
    if keys[pygame.K_d]:
        print("D key pressed")

# 退出Pygame
pygame.quit()
sys.exit()

```



###### 代码1可用：

```python
from pynput import keyboard


def on_press(key):
    print('{0} pressed'.format(key))


with keyboard.Listener(on_press=on_press) as listener:
    listener.join()
```



```python
from pynput import keyboard


def on_press(key):
    try:
        # 按键按下时执行的操作
        print('Key {0} pressed'.format(key.char))

        # 在这里添加你希望执行的其他操作

    except AttributeError:
        # 特殊按键按下时执行的操作
        print('Special key {0} pressed'.format(key))

        # 在这里添加你希望执行的其他操作


def on_release(key):
    # 按键释放时执行的操作
    print('{0} released'.format(key))

    # 在这里添加你希望执行的其他操作

    if key == keyboard.Key.esc:
        # 按下Esc键时停止监听
        return False


# 启动监听器
with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()

```

###### 手柄初始化

```python
import pygame

pygame.init()
joystick = pygame.joystick.Joystick(0)
joystickNum = pygame.joystick.get_count()
print(joystickNum)
joystick.init()  # 手柄初始化

screen = pygame.display.set_mode((1040, 960))
character_position = [400, 300]
character_speed = 5

running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        if event.type == pygame.JOYBALLMOTION:
            print(event)

        if event.type == pygame.JOYAXISMOTION:
            print(event)
            if event.axis == 0:  # 左摇杆 X 轴
                character_position[0] += int(event.value * character_speed)
            elif event.axis == 1:  # 左摇杆 Y 轴
                character_position[1] += int(event.value * character_speed)
            elif event.axis == 3:  # 右摇杆 X 轴
                # 根据手柄的 X 轴移动视角
                pass
            elif event.axis == 4:  # 右摇杆 Y 轴
                # 根据手柄的 Y 轴移动视角
                pass

    screen.fill((0, 0, 0))  # 清空画面
    pygame.draw.circle(screen, (255, 0, 0), character_position, 20)  # 绘制角色
    pygame.display.update()  # 更新画面

pygame.quit()
```

###### 创建窗口内监视

``` python
import tkinter as tk
from pynput import mouse, keyboard

def on_key_press(key):
    print(f'Key {key} pressed')

def on_key_release(key):
    print(f'Key {key} released')

def on_mouse_click(x, y, button, pressed):
    if pressed:
        print(f'Mouse clicked at ({x}, {y}) with {button} button pressed')
    else:
        print(f'Mouse clicked at ({x}, {y}) with {button} button released')

def create_window():
    root = tk.Tk()
    root.title('Window Monitoring')

    # 创建一个空白的 Label，用于捕获键盘和鼠标事件
    label = tk.Label(root, text='Monitor Window')
    label.pack()

    # 监听键盘事件
    with keyboard.Listener(on_press=on_key_press, on_release=on_key_release) as key_listener:
        # 监听鼠标事件
        with mouse.Listener(on_click=on_mouse_click) as mouse_listener:
            # 启动 Tkinter 主循环
            root.mainloop()

            # 停止监听键盘和鼠标事件
            key_listener.join()
            mouse_listener.join()

if __name__ == "__main__":
    create_window()

```

