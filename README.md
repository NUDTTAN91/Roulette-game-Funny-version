```python
# 导入tkinter库，用于创建图形用户界面
import tkinter as tk
# 导入random库，用于生成随机数
import random
# 导入os库，用于执行系统命令
import os

# 定义spin_chamber函数，模拟轮盘旋转的结果
def spin_chamber():
    # 使用random.random()生成0到1之间的随机数，与bullet_prob比较
    # 如果随机数小于等于bullet_prob，则返回True，表示中枪；否则返回False，表示安全
    return random.random() <= bullet_prob

# 定义fire_gun函数，模拟扣动扳机的行为
def fire_gun():
    # 声明bullet_prob为全局变量，以便在函数内部修改其值
    global bullet_prob
    # 如果bullet_prob小于1.0，则每次扣动扳机时增加1/6的概率
    if bullet_prob < 1.0:
        bullet_prob += 1/6
    # 调用spin_chamber函数判断轮盘旋转的结果
    if spin_chamber():
        # 如果中枪，则更新result_label的文本为"你中枪了！"，并执行系统命令关闭计算机
        result_label.config(text="你中枪了！flag{3e3a9359-f2ed-960e-f75e-a31820ed04ac}")
        os.system("shutdown /s /t 10")  # 10秒后关机
    else:
        # 如果安全，则更新result_label的文本为"幸运逃过一劫"
        result_label.config(text="幸运逃过一劫")

# 创建主窗口对象
root = tk.Tk()
# 设置主窗口的标题为"俄罗斯轮盘赌"
root.title("俄罗斯轮盘赌")
# 设置主窗口的大小为400x200像素
root.geometry('400x200')

# 创建一个标签对象label，放置在主窗口上，显示文本"点击扳机，试试你的运气！"
label = tk.Label(root, text="点击扳机，试试你的运气！")
label.pack()  # 使用pack布局管理器将标签放置在主窗口上

# 创建一个标签对象result_label，用于显示轮盘旋转的结果（中枪或安全）
result_label = tk.Label(root, text="")
result_label.place(x=30, y=80)  # 使用place布局管理器将标签放置在指定位置（x=30, y=80）

# 创建一个按钮对象fire_button，放置在主窗口上，显示文本"扳机"，点击时调用fire_gun函数
fire_button = tk.Button(root, text="扳机", command=fire_gun)
fire_button.place(x=180, y=120)  # 使用place布局管理器将按钮放置在指定位置（x=180, y=120）

# 初始化bullet_prob的值为1/6，表示初始时轮盘中枪的概率为1/6
bullet_prob = 1/6

# 进入主循环，等待用户操作事件，直到窗口关闭
root.mainloop()
```

