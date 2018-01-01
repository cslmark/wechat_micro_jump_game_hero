![计算](http://upload-images.jianshu.io/upload_images/576195-fd957e0c51330db5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


调试时，修改 debug 为 True，真实运行时，设置为 False。停顿时间设置为 2s，如果电脑运算速度太快，保险起见可以设置为 2s。


原理：

1. adb 截图
1. 找到小人臀部坐标（hsv 色相紫黑色）
1. 找到下一桥墩的顶点坐标
1. 找到下一桥墩的极左/极右点坐标
1. 计算出下一桥墩的中心点坐标
1. 从小人臀部到下一桥墩中心点计算出跳远距离
1. 将距离换算为长按时长
1. 使用 adb 跳

更新日志：

**2018-01-01**

目的只是找到极点，并不需要二值化，去除相关代码。速度快。

目前以 距离 x 1.5 作为长按时长，基本能跳到目标中心位置。

**2017-12-30**

去除垂直投影图的方案，使用直接识别背景的方式去除背景，并二值化，以误别“极点”。速度仍然慢。

**2017-12-29**

第一可用版本，准确性不高，速度慢，使用垂直投影图进行目标查找。


## 开发环境搭建


### 系统环境

笔者环境：

    $ uname -a
    Darwin rmbp-finn.lan 17.3.0 Darwin Kernel Version 17.3.0: Thu Nov  9 18:09:22 PST 2017; root:xnu-4570.31.3~1/RELEASE_X86_64 x86_64

    $ python --version
    Python 2.7.10
    
    测试机：小米5

### 安装 Python 2.7

略。

### (可选安装) virtualenv, virtualenvwrapper

略。

### 安装 adb

略。

### 工程搭建


先 fork 一份到自己账户。然后：

    $ mkvirtualenv wechat_micro_jump_game_hero
    $ cdvitualenv
    $ git clone ...
    $ cd wechat_micro_jump_game_hero
    $ echo `pwd` > ../.project
    $ pip install pipenv
    $ pipenv install

手机连上电脑，打开跳一跳小游戏，并点击开始，之后：

    $ python main.py
