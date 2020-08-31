## Gallery Marker

### 一句话需求

读取特定文件夹中的子文件夹，展示该子文件夹中随机的图片，用户通过检阅图片作出该子文件夹是否能够成为 Top 文件夹的决定

### 需求分析

术语定义

1. Gallery         - 一个包含图片的文件夹
2. Image           - 一个 Gallery 中的某张图片
3. Collection      - 一个包含 Gallery 的文件夹
4. TOP             - 一个用来保存 Gallery 的文件夹
5. Status: Top     - Gallery 的状态，当 Gallery 处于该状态时认为该 Gallery 需要被移动到 TOP 中
6. Status: Skip    - Gallery 的状态，当 Gallery 处于该状态时认为该 Gallery 不需要被特殊处理
7. Status: Delete  - Gallery 的状态，当 Gallery 处于该状态时认为该 Gallery 需要被移除

App 功能分为两个部分，一是标注，二是处理

其中，标注部分描述为：

1. User 指定 Collection
1. App 读取特定 Collection，开始逐个展示其中的 Gallery
2. 当展示某个 Gallery 时，随机并逐个展示其中的特定数量的 Image
3. 当展示某个 Image 时，User 能使用按下特定按键标注该图片的状态
4. User 可以按下特定按键退出标注过程

处理部分描述为：

1. User 设置 TOP 后点击处理
2. App 读取 Gallery 标注信息，逐个处理 Gallery
3. 若 Gallery 状态为 Top，将该 Gallery 移动到 TOP 中
4. 若 Gallery 状态为 Skip，跳过对该 Gallery 的处理
5. 若 Gallery 状态为 Delete，将该 Gallery 删除

### 功能拆分

1. 标注：User ：设置 Collection
2. 标注：App  ：读取 Collection
3. 标注：App  ：轮播 Collection 中的 Gallery
4. 标注：App  ：随机轮播 5 张 Gallery 中的 Image
5. 标注：App  ：轮播 Image 的结束后，监听按键，按下 a 则将 Gallery 状态置为 Top，按下 s 则将 Gallery 状态置为 Skip，按下 d 则将 Gallery 状态置为 Delete
6. 标注：App  ：标注过程中监听按键，按下 q 则退出标注，若当前 Gallery 未播放 5 张 Image，不记录当前 Gallery 的状态，退出时将已标注 Gallery 信息保存到一个文件 galleries.txt 中
7. 处理：App  ：设置 TOP
8. 处理：App  ：读取 galleries.txt，确认 Gallery 存在，不存在直接跳过，否则若 Gallery 状态为 Top，将该 Gallery 移动到 TOP 中；若 Gallery 状态为 Skip，跳过对该 Gallery 的处理；若 Gallery 状态为 Delete，将该 Gallery 删除

### 技术选型

如果用 JS 技术栈，标注部分的功能实现起来没什么难度，但是需要用 C/S 架构

不适用 JS 技术栈，得考虑一下 UI 部分怎么做

Search 了一下，全部用 Python 做好了，UI 部分用 Tkinter 实现

要用到的库大概有：

1. Tkinter  - UI 展示
2. Pillow   - 图片展示
3. PST      - Python 标准库，文件相关操作

202008301628
上面的话当我没说，GUI 用起来真的要死，还是 Web 做吧。。。

