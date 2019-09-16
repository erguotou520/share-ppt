title: 树莓派简述
speaker: erguotou
url: https://github.com/erguotou520/share-ppt

<slide class="bg-blue aligncenter" image="https://www.raspberrypi.org/homepage-9df4b/static/hero-shot-3ad1d131ea382fa6f006b18aefc820aa.png .dark">

# 树莓派简介 {.text-landing.text-shadow}

By erguotou {.text-intro}

[:fa-github: Github](https://github.com/erguotou520/shares-ppt){.button.ghost}

<slide class="bg-blue aligncenter" image="https://www.raspberrypi.org/homepage-9df4b/static/hero-shot-3ad1d131ea382fa6f006b18aefc820aa.png .dark">
# 它不是一个吃的！{.text-landing}

<slide class="slide-top" image="https://www.raspberrypi.org/homepage-9df4b/static/hero-shot-3ad1d131ea382fa6f006b18aefc820aa.png .right-bottom">
# 那它到底是个啥？

一个只有信用卡大小的卡片式电脑{.text-intro.animated.fadeInUp.delay-1s}

* 迷你{.flipInX}
* Arm芯片{.flipInX}
* GPIO{.flipInX}
* 高扩展性{.flipInX}
* 可玩性{.flipInX}
  {.text-cols.build}

<slide class="aligncenter" image="">
# 我可以用树莓派做什么

:::flexblock
### 一个完整的Linux系统

![](https://www.raspberrypi.org/app/uploads/2015/08/raspbian.png)

---
### 网络收音机/智能音响

[叮当开源智能音箱](https://github.com/wzpan/dingdang-robot)
![](http://shumeipai.nxez.com/wp-content/uploads/2017/07/20170702214228879-0.jpg)

---
### 无人机
![](http://photo.5imxbbs.com/forum/201503/15/195619gux1o2rd4or6x24w.jpg)

---

### 魔镜
![](https://gd1.alicdn.com/imgextra/i1/2567133025/TB21lx1aNjaK1RjSZKzXXXVwXXa_!!2567133025.jpg)
:::

<slide class="aligncenter" image="">
# 还有什么

:::flexblock
### 绘画机/打字机
![](https://www.raspberrypi.org/app/uploads/2019/09/ezgif-1-c1f8a88347a5.gif)

---
### 遥控小车
![](http://www.elecfans.com/uploads/allimg/150331/1772475-1503311013242R.jpg)

---

### 怀旧游戏机
![](https://www.meiyagroup.com.tw/wp-content/uploads/2018/08/Game-HAT-intro.jpg)

---

### Everything you can image
:::

<slide class="aligncenter" image="">
# 树莓派上都有些什么
各个版本硬件会有些差异{.text-subtitle}

![](https://lingshunlab.com/wp-content/uploads/2019/01/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2019-01-05-%E4%B8%8A%E5%8D%8810.21.16-1024x727.png){.size-40}

<slide class="" image="">
:::column
# 怎么玩

1. 有个点子/看到别人分享的好点子{.flipInX}
2. 刷相应的系统{.flipInX}
3. 可能需要学习一些Python代码来实现你的点子{.flipInX}
4. 注意安全{.flipInX}
  {.text-cols.build}
---
![](https://www.raspberrypi.org/app/uploads/2019/09/CPUK19_PHOTO4134-500x377.jpg){.side-40.right}
:::

<slide class="aligncenter" image="">
# 它的兄弟姐妹们

:::flexblock
### 香橙派
![](https://ae01.alicdn.com/kf/HTB1Lx9rbvLsK1Rjy0Fbq6xSEXXaC/Orange-Pi-3-H6-2GB-LPDDR3-AP6256-Bluetooth5-0-4-USB3-0-Support-Android-7-0.jpg_640x640.jpg)

---
### 香蕉派
![](https://cdn-reichelt.de/bilder/web/artikel_ws/A300/BANANA_PI_01.jpg)

---

### Nano PI
![](https://www.armbian.com/wp-content/uploads/2018/02/nanopineo.png)

---

### Arduino
![](https://cdn.sparkfun.com/assets/9/1/e/4/8/515b4656ce395f8a38000000.png)
:::

<slide class="content-center" image="">
# 一个亮灯demo
---

```python
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BOARD)
GPIO.setup(11, GPIO.OUT)
GPIO.output(11, True)
time.sleep(3)
GPIO.output(11, False)
GPIO.cleanup()
```

<slide class="content-center" image="">
# 来个升级版

呼吸灯效果{.text-subtitle}

---

```python
import RPi.GPIO as GPIO
import time
from math import sin, pi

GPIO.setmode(GPIO.BOARD)
GPIO.setup(11, GPIO.OUT)
p = GPIO.PWM(11, 500)
p.start(0)
try:
    while 1:
        for angle in range(0, 360, 1):
            duty = int((sin((angle / 180.0 - 0.5) * pi) + 1) * 50)
            p.ChangeDutyCycle(duty)
            time.sleep(0.003)
except KeyboardInterrupt:
    p.stop()
    GPIO.cleanup()
```

<slide class="content-center" image="">
# 一个蜂鸣器demo
---

```python
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BOARD)
GPIO.setup(16, GPIO.OUT)

# 脉宽调制（PWM）
p = GPIO.PWM(16, 50)  # 通道为 16 频率为 50Hz
p.start(0)
try:
    while 1:
        for dc in range(0, 101, 5):
            p.ChangeDutyCycle(dc)
            time.sleep(0.1)
        for dc in range(100, -1, -5):
            p.ChangeDutyCycle(dc)
            time.sleep(0.1)
except KeyboardInterrupt:
    pass
p.stop()
GPIO.cleanup()
```

<slide class="aligncenter" image="">
# 一个半成品项目
[https://github.com/erguotou520/home-air-health-monitor](https://github.com/erguotou520/home-air-health-monitor)

<slide class="bg-blue aligncenter" video="https://webslides.tv/static/videos/working.mp4 poster='https://webslides.tv/static/images/working.jpg' .dark">
# 感谢收听！！