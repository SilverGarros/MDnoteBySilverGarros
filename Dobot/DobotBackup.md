###### 001

```python
import pygame
import DobotDllType as dType
from pynput import keyboard

running = None
CON_STR = {
    dType.DobotConnect.DobotConnect_NoError: "DobotConnect_NoError",
    dType.DobotConnect.DobotConnect_NotFound: "DobotConnect_NotFound",
    dType.DobotConnect.DobotConnect_Occupied: "DobotConnect_Occupied"}
api = dType.load()
state = dType.ConnectDobot(api, "", 115200)[0]
print("01 " + str(state))


def key_press(key):
    try:
        if key.char.lower() == 'a':
            print('A key pressed - Performing specific action for A key')
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZMode, 100, 0, 0, 0, isQueued=1)
        elif key.char.lower() == 'd':
            print('D key pressed - Performing specific action for D key')
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZMode, 0, 100, 0, 0, isQueued=1)
        elif key.char.lower() == 'w':
            print('W key pressed - Performing specific action for W key')
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZMode, 0, 50, 100, 0, isQueued=1)
        elif key.char.lower() == 's':
            print('S key pressed - Performing specific action for S key')
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZMode, 0, 50, 0, 100, isQueued=1)
    except AttributeError:
        print('Special key {0} pressed'.format(key))


def key_release(key):
    # 在键释放时停止机械臂运动
    dType.SetQueuedCmdStopExec(api)
    print('{0} released'.format(key))

    if key == keyboard.Key.esc:
        global running
        running = False


if state == dType.DobotConnect.DobotConnect_NoError:
    print("02 机械臂连接正常")
    dType.SetQueuedCmdClear(api)  # 初始化清空机械臂的指令
    dType.SetQueuedCmdStartExec(api)  # 开始执行队列指令
    Pose=dType.GetPose(api)
    print(Pose)
    # dType.SetHOMECmd(api, temp=0, isQueued=0)
    # dType.SetQueuedCmdStartExec(api)
    running = True

    # 启动监听器
    with keyboard.Listener(on_press=key_press, on_release=key_release) as listener:
        while running:
            # 在这里添加你希望执行的其他操作
            pass

    # 关闭监听器后断开机械臂连接
    listener.stop()
    listener.join()
dType.DisconnectDobot(api)
```

###### 002

```python
import pygame
import DobotDllType as dType
from pynput import keyboard

running = None
CON_STR = {
    dType.DobotConnect.DobotConnect_NoError: "DobotConnect_NoError",
    dType.DobotConnect.DobotConnect_NotFound: "DobotConnect_NotFound",
    dType.DobotConnect.DobotConnect_Occupied: "DobotConnect_Occupied"}
api = dType.load()
state = dType.ConnectDobot(api, "", 115200)[0]
print("01 " + str(state))


def key_press(key):
    try:
        if key.char.lower() == 'a':
            print('A key pressed - Performing specific action for A key')
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 10, 0, 0, 0, isQueued=0)
        elif key.char.lower() == 'd':
            print('D key pressed - Performing specific action for D key')
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 0, 10, 0, 0, isQueued=0)
        elif key.char.lower() == 'w':
            print('W key pressed - Performing specific action for W key')
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 0, 50, 10, 0, isQueued=0)
        elif key.char.lower() == 's':
            print('S key pressed - Performing specific action for S key')
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 0, 50, 0, 10, isQueued=0)
    except AttributeError:
        pass
        print('Special key {0} pressed'.format(key))


def key_release(key):
    # 在键释放时停止机械臂运动
    # dType.SetQueuedCmdStopExec(api)
    print('{0} released'.format(key))

    if key == keyboard.Key.esc:
        global running
        running = False


if state == dType.DobotConnect.DobotConnect_NoError:
    print("02 机械臂连接正常")
    dType.SetQueuedCmdClear(api)  # 初始化清空机械臂的指令
    dType.SetQueuedCmdStartExec(api)  # 开始执行队列指令
    Pose = dType.GetPose(api)
    print(Pose)
    # dType.SetHOMECmd(api, temp=0, isQueued=0)
    # dType.SetQueuedCmdStartExec(api)
    running = True

    # 启动监听器
    with keyboard.Listener(on_press=key_press, on_release=key_release) as listener:
        while running:
            # 在这里添加你希望执行的其他操作
            pass

    # 关闭监听器后断开机械臂连接
    listener.stop()
    listener.join()
dType.DisconnectDobot(api)
```

###### 003_231227_2 完美监视，但有延迟bug，为了实现窗口内监视备份

```python
import time
import tkinter as tk
import DobotDllType as dType
from pynput import keyboard
from pynput import mouse

'''程序运行参数'''

PTPMoveXYZParams = 10  # xyz移动的精度范围，单位mm,推荐5-20，切莫太大
PTPMoveSpeedAndAcceleration = (100, 50)  # 移动的速度和加速度百分比

running = None
EndEffectorSate = False
right_click_count = 0
CON_STR = {
    dType.DobotConnect.DobotConnect_NoError: "DobotConnect_NoError",
    dType.DobotConnect.DobotConnect_NotFound: "DobotConnect_NotFound",
    dType.DobotConnect.DobotConnect_Occupied: "DobotConnect_Occupied"}
api = dType.load()
state = dType.ConnectDobot(api, "", 115200)[0]
print("01 " + str(state))
dType.SetHOMEParams(api, 200, 200, 200, 200, isQueued=1)
dType.SetPTPJointParams(api, 200, 200, 200, 200, 200, 200, 200, 200, isQueued=1)
dType.SetPTPCommonParams(api, PTPMoveSpeedAndAcceleration[0], PTPMoveSpeedAndAcceleration[1], isQueued=1)


# dType.SetHOMECmd(api, temp=0, isQueued=1)


def mouse_click(x, y, button, pressed):
    global EndEffectorSate
    global right_click_count
    try:
        if button == mouse.Button.right:
            if pressed:
                right_click_count += 1
                if right_click_count % 2 == 0:
                    EndEffectorSate = not EndEffectorSate
                dType.SetEndEffectorGripper(api, EndEffectorSate, 0, 1)
                print('状态切换')
            else:
                pass
        elif button == mouse.Button.left:
            if pressed:
                dType.SetEndEffectorGripper(api, EndEffectorSate, 1, 1)
            else:
                dType.SetEndEffectorGripper(api, EndEffectorSate, 0, 1)
    except:
        pass

    # print(f'Click position： ({x}, {y})')
    # print(f'Click button： {button}')
    # print(f'Click state: {"Pressed" if pressed else "Release"}')


def key_press(key):
    try:
        k = PTPMoveXYZParams
        if isinstance(key, keyboard.KeyCode):
            # 处理字符按键
            char = key.char.lower()
            if char == 'w':
                dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, k, 0, 0, 0, isQueued=1)
            elif char == 's':
                dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, -k, 0, 0, 0, isQueued=1)
            elif char == 'a':
                dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 0, k, 0, 0, isQueued=1)
            elif char == 'd':
                dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 0, -k, 0, 0, isQueued=1)
            elif char == 'q':
                dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 0, 0, 0, k, isQueued=1)
            elif char == 'e':
                dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 0, 0, 0, -k, isQueued=1)
            elif char == 'r':
                dType.SetPTPCmd(api, dType.PTPMode.PTPMOVJXYZMode, 206.60475158691406, 0.0, 135.0940704345703, 0.0,
                                isQueued=1)

        elif key == keyboard.Key.ctrl_l:
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 0, 0, -k, 0, isQueued=1)
        elif key == keyboard.Key.space:
            dType.SetPTPCmd(api, dType.PTPMode.PTPMOVLXYZINCMode, 0, 0, k, 0, isQueued=1)

        elif key == keyboard.Key.esc:
            global running
            running = False

    except Exception as e:
        print(f"发生异常: {e}")


def key_release(key):
    # 在键释放时停止机械臂运动
    # dType.SetQueuedCmdStopExec(api)
    char = getattr(key, 'char', None)
    if char and char.lower() in ['w', 'a', 's', 'd', 'q', 'e']:
        dType.SetQueuedCmdClear(api)
        print('{0} released'.format(key))
    elif key in [keyboard.Key.space,keyboard.Key.ctrl_l]:
        dType.SetQueuedCmdClear(api)
        print('{0} released'.format(key))
    elif key == keyboard.Key.esc:
        global running
        running = False
    else:
        pass


if state == dType.DobotConnect.DobotConnect_NoError:
    print("02 机械臂连接正常")
    dType.SetQueuedCmdClear(api)  # 初始化清空机械臂的指令
    dType.SetQueuedCmdStartExec(api)  # 开始执行队列指令
    Pose = dType.GetPose(api)
    print(Pose)
    # dType.SetHOMECmd(api, temp=0, isQueued=0)
    # dType.SetQueuedCmdStartExec(api)
    running = True

    # 启动监听器
    MouseListener = mouse.Listener(on_click=mouse_click)
    MouseListener.start()
    KeyboardListener = keyboard.Listener(on_press=key_press, on_release=key_release)
    KeyboardListener.start()
    try:
        while running:
            time.sleep(0.1)
    except KeyboardInterrupt:
        # 捕获键盘中断信号
        print("键盘中断信号捕获，程序退出")
        dType.SetQueuedCmdClear(api)
        dType.SetQueuedCmdStopExec(api)
    finally:
        # 清理工作，确保机械臂停止等
        dType.SetQueuedCmdClear(api)
        dType.SetQueuedCmdStopExec(api)
        dType.SetEndEffectorGripper(api, 0, 0, 0)
        MouseListener.stop()
        KeyboardListener.stop()
        MouseListener.join()
        KeyboardListener.join()

dType.DisconnectDobot(api)

```

