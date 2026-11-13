# SAN_New_Angel
A 2D Action RPG Devlog for CUC Portfolio
### 2026-11-01 (Day 2 补记：Emoji 素材与坐标大坑)
- **素材踩坑**：
  - 费劲千辛万苦终于找到可用的 Emoji 素材。自带的输入法输出不符合要求，网搜的各种奇奇怪怪，最终在 Emoji 百科找到了想要的谷歌版：😂😡🤓🤣😅🐖。
  - 遇到了素材问题：部分 Emoji 大小不一致，部分带有莫名其妙的白色背景。
- **技术验证（意外成功）**：
  - 试探性地直接把文件拖入 Godot 左下角文件夹（res://），成功导入！
- **遗留 Bug（待解决）**：
  - 发射出去的 Emoji，主角本体会一直卡在屏幕左上角，无法正常出现在中间。
  - 因时间有限，决定明日集中精力进行坐标偏移（Offset）与贴图居中的排查。
<img width="1440" height="1920" alt="1c47bdb725bfb1fcacddf636ebbb9b09" src="https://github.com/user-attachments/assets/854b7019-c337-430e-a029-2754346bad33" />
<img width="1440" height="1920" alt="755b1cc7db3bf37c1f78ad710ec33815" src="https://github.com/user-attachments/assets/be0a968f-11e4-47c3-bd2b-2073c9fc3633" />
<img width="1440" height="1920" alt="1c47bdb725bfb1fcacddf636ebbb9b09" src="https://github.com/user-attachments/assets/c053709d-dbff-4f35-9faa-d88b3494294e" />

DAY2∽DAY7（11.2∽11.7）的开发日记（因为网络连接抽风，导致这几天本人没有上传日记 所以未来游戏开发，上传日记不太可能太频繁）

**痛定思痛的反思**

在我自从11.1日开启游戏开发（我本人的开发日记，是在当天之后第二天甚至更多天后发的），我发现，我的编程效率堪忧，本质是人形AI代码粘贴器，于是在我反思之后，就暂时性的先停了实战堪忧的开发。在11.4日正式开始了编程学习，在B站寻找视频进行学习，并且根据视频进行实战以及摘录笔记

**美术学习的探索**
在我痛定思痛决定开始学编程之后，我也差不多同时开始了像素美术学习，用PIXEL STUDIO进行绘画，目前学习效果尚可。（这几天的绘画进步）

<img width="1440" height="1920" alt="d636991573ebca9f95d24f35e4fe65c2" src="https://github.com/user-attachments/assets/a6e9dd74-b684-4431-bd58-f307648b5b4b" />
<img width="1440" height="1920" alt="fbf5f1d54815e022b3005faaf9d55e78" src="https://github.com/user-attachments/assets/4186e861-6c15-4ad2-87fc-8292cdf1d65c" />
<img width="1920" height="1440" alt="088085b77c99b91cb36b8566bd7facd4" src="https://github.com/user-attachments/assets/e0060455-7af8-4bb4-b235-7cd4c1a55fa4" />

<img width="873" height="1920" alt="c0e2b7a9013a496a06152415b1716bde" src="https://github.com/user-attachments/assets/9672a07c-cc58-4062-ab0e-edfe590bd2ca" />

<img width="873" height="1920" alt="543f4a914d0bf8bba5ae8695f98aa391" src="https://github.com/user-attachments/assets/cb014f9d-1785-4709-ac15-66479d5b55ce" />

<img width="873" height="1920" alt="95a6a5bfe6a4c8e8c22b7512155d75ed" src="https://github.com/user-attachments/assets/8046303e-0db7-474c-a2d9-34c9e54dd528" />

<img width="873" height="1920" alt="f4c66ff1e7821b4cdfb2f907fb3a0f1e" src="https://github.com/user-attachments/assets/a1623b53-fc8d-42a1-b157-cc5aeef977ca" />

# SAN NEW ANGEL - Devlog

## 🗓️ 2026-11-08 (Day 8：底层逻辑重构与核心控制流)

### 🧠 编程理论大突破
今天继续进行底层逻辑的深入学习，并整理了硬核手写笔记：
- **布尔值（Boolean）与逻辑判断**：
  - 深入理解了 `True` 和 `False` 的本质。
  - 掌握了 `and`（必须全真）与 `or`（一真即真）的区别，并理解了逻辑判断中的“短路效应”。
- **选择结构（if / elif / else）**：
  - 明确了 `elif` 作为“插队/分支”的概念，用于处理多条件判断。
  - **核心机制**：一旦某个条件满足（如 `if` 或某个 `elif` 通过），程序将立刻跳出当前判断块，绝对不再执行下方其他分支。
- **循环结构（while）**：
  - `while` 是“当条件成立时一直执行”。
  - 极其凶险！如果忘记在内部改变条件（如 `count += 1`），会触发“死循环（Deadlock）”，导致程序卡死、控制台疯狂刷屏。

### 💻 引擎实战与惨痛踩坑
- **生命周期与返回值**：再次巩固了 `_ready()`（单次触发）和 `_process()`（循环触发）的区别；彻底搞懂了 `-> void`（只执行不返回）的含义，理清了 `void`（类型）与 `_ready`（函数名）毫无捆绑关系。
- **实战测试**：在测试 `if 4 == 4 or 10 > 11:` 时遇到“无输出”现象，排查后发现是场景树主节点（Node2D）与脚本挂载不匹配导致。
- **💥 玄学卡顿（血的教训）**：在测试布尔值时，因手滑误触了某些未知操作，导致 Godot 引擎当场“发癫”，陷入极其严重的疯狂卡顿（未响应状态）。最终只能无奈呼出任务管理器强杀进程才得以脱险。**总结教训：严格区分 F5（运行整个项目主场景）与 F6（单独运行当前场景），千万别在深夜乱点未知面板！**

### 🎨 美术进展
- **像素画练习**：在手机端 `Pixel Studio` 进行了长时间临摹练习，成功绘制出一个具备光影细节的“深色玻璃药剂瓶”。
- **数据记录**：累计绘画时长突破 4 小时，总点击量逼近 2 万次，控笔精细度显著提升。

---
*Stay hungry, stay foolish. 明天继续攻克节点绑定与实例化。*
<img width="1280" height="960" alt="06071b01a9b91744fad3be702710ab65_720" src="https://github.com/user-attachments/assets/06a8b5fe-4079-45ec-b3ab-934df092a03f" />
<img width="1280" height="960" alt="281169777a171b96c245ce11617ba641_720" src="https://github.com/user-attachments/assets/2e611562-f749-47d6-b707-4e4c987cad7d" />
<img width="1280" height="582" alt="79fe0a69459968f75afafdf32214007e_720" src="https://github.com/user-attachments/assets/e7fc6896-5fe7-49b4-b098-f7de401021b7" />
<img width="1280" height="960" alt="2fbcb53dd11529fd719b6e0a46713fa0_720" src="https://github.com/user-attachments/assets/d22a8e04-84a6-447f-8188-6784a4d3674d" />
<img width="1280" height="960" alt="5ca5a865b611615d708a9cc9db9b5107_720" src="https://github.com/user-attachments/assets/be3d1a05-6fd8-4c15-b127-1ea0692e59de" />

<img width="873" height="1920" alt="aacdbfaf3e765363a7bae2b3a06d2b79_720" src="https://github.com/user-attachments/assets/ca45ed32-a588-43e7-ad35-6d5ee8910efc" />

# SAN NEW ANGEL - Devlog

## 🗓️ 2026-11-09 (Day 9：底层控制流与像素武器设计)

今日受外部行程（跨区聚餐）影响，大块代码实战时间被压缩，但在碎片时间依然保持了底层理论的学习与美术资产的产出。

### 🧠 编程理论大突破（控制流与核心语法）
通过系统整理手写笔记，开始深入理解以下几个核心概念：
- **`+=` 累加机制**：理解了其本质为 `自身 = 自身 + 新增值`。常用于血量恢复（`hp += 20`）或持续位移。
- **坐标轴与正负方向**：明确了 `direction = 1`（向右）与 `direction = -1`（向左）的物理意义。
- **`var` 与 `func` 的本质区别**：
  - `var`（变量）：定义“名词”。用于存放数据（如 HP、速度），状态是静态的，等待被赋值。
  - `func`（函数）：定义“动词”。用于封装动作（如攻击、移动），只有被调用时才会执行。
- **`pass` 关键字**：明确其为“占位符”。在语法要求必须有缩进但暂未想好逻辑时使用，本身不产生实际效果，但可避免程序报错。

### 💻 引擎实战与疑惑
- **节点路径获取**：学习了使用 `$` 符号（如 `$Icon`）快速获取当前场景下的子节点。
- **一个小疑惑**：在测试 `_process` 让图标移动时，遭遇 `Node not found: "Icon"`。重新创建节点并严格统一命名后，依然没有看到预期中的移动效果。虽然检查了代码逻辑没问题，但最终还是因为时间太晚没排查出来。留待明天重新梳理场景树结构再战。

### 🎨 美术进度（Pixel Studio）
- **素材产出**：完成了多张像素素材练习（深色药剂瓶、透明水杯等）。
- **核心设计**：构思并绘制了一把“紫（暗影）、蓝（冰）、红（火）”配色的元素剑。初步定位于B地区变异小怪的专属武器。
- **美术数据**：累计绘画时长突破 5 小时，点击量逼近 2.6 万次。

---
*Stay hungry, stay foolish. 承认疑惑，也是解决 Bug 的第一步。*

<img width="1280" height="960" alt="c91f8b8ed26bf13f9520d4e3c7f36712_720" src="https://github.com/user-attachments/assets/bfcb1cb1-508b-4335-af2b-03a3a68d4af5" />

<img width="1280" height="960" alt="d3b9bde8ce5aa7be1b9b2c9de75fd5d6_720" src="https://github.com/user-attachments/assets/8b9609d9-a522-4216-87d0-d01a8a0f161e" />

<img width="873" height="1920" alt="f1cc224945278c89eaa21a5af8807043" src="https://github.com/user-attachments/assets/800d0ed7-b9b3-4721-8151-a4062a05dfb4" />

<img width="873" height="1920" alt="63243d68a6c4e44c4990db6456bd1920_720" src="https://github.com/user-attachments/assets/7032e600-73fd-4eb8-b501-957f51054f3a" />

<img width="1280" height="582" alt="a312a0ab3b86528d7b7ee3ccf33b051b_720" src="https://github.com/user-attachments/assets/8dbb40e5-7633-405e-83a9-49666412d41b" />

# SAN NEW ANGEL - Devlog

## 🗓️ 2026-11-10 (Day 10：环境排雷与美术场景初探)

今日经历了较为强烈的“开发阵痛期”，连续经历两次踩雷，影响了部分进度，但也完成了美术上的新尝试。

### 💻 引擎实战与排坑
- **第一次踩雷（脚本挂载死胡同）**：在跟随教程尝试为节点附加脚本时，多次遭遇“附加失败”与空脚本报错。经过复盘，意识到是 Godot 的默认路径与节点继承关系发生了冲突，决定明日新建纯净工程重新测试。
- **第二次踩雷（社区交流与学习）**：在技术群交流时，被群员安利了 GDS 基础视频教程。由于当天时间太晚，未能一口气看完，决定明日继续学习。

### 🧠 编程理论
- 重新看了精简版 GDS 视频教程，巩固了核心基础语法。

### 🎨 美术进度（Pixel Studio）
- **场景绘制尝试**：尝试给地图绘制部分场景，但在模仿学习的过程中未能达到预期效果，产出了半成品。
- **素材产出**：绘制了一枚具有通透质感的蓝色冰系圆球。虽然中途手滑，冰球疑似被画成了保龄球，但光影效果尚可。初步设定为具有冰冻/物理砸击属性的道具。

---
*Stay hungry, stay foolish. 允许自己偶尔卡壳，因为这是解决 Bug 的必经之路。*
<img width="1280" height="960" alt="94c0f19630968410b15433da847f25dd_720" src="https://github.com/user-attachments/assets/8514a105-f477-4188-9688-76c20bbcc553" />
<img width="1200" height="11527" alt="aca5550b6e635c27efc8e13aac53d20b_720" src="https://github.com/user-attachments/assets/2d2298da-e85e-4d5f-b70e-f7bff96676ed" />
<img width="1280" height="960" alt="7c865d2e1296720ae2e35f2fceff30d9_720" src="https://github.com/user-attachments/assets/323f9a05-8141-4eca-8b9c-d87c56246f33" />
<img width="1280" height="960" alt="3d3cc31cc1570fb66f767993d31c71df_720" src="https://github.com/user-attachments/assets/24355082-aacc-4c76-8e2f-87ae2e9b5667" />
<img width="873" height="1920" alt="91291a1cd4d7d2198c60940768a94e51_720" src="https://github.com/user-attachments/assets/2b7ea670-185f-4113-bb10-82e880946150" />

# SAN NEW ANGEL - Devlog

## 🗓️ 2026-11-11 (Day 11：修整与蓄力)

今日因学校突发的普通话水平测试及晚间课程，极大地压缩了开发时间。同时，经历了前八天高强度的编程底层学习与像素美术练习，大脑和身体均发出了需要休息的信号。

### 💡 开发者心语
今天没有写代码，也没有画像素。我选择在这一天放下键盘，去体验其他人的游戏世界（Minecraft 暮色森林开荒），并为喜爱的角色庆生。

今天也是我推 **爱莉希雅（二游高热度角色）** 的生日。作为一个未来想做游戏的人，去感受顶级二次元IP的角色魅力与社区氛围，观察玩家们为何对她如此狂热，本身也是一种不可或缺的“市场调研”与情感积累。

**“深蹲是为了更好的跳跃，今天的休息，是为了未来更好的前进。”**

---
*Stay hungry, stay foolish. 允许自己慢下来，也是一种修行。*
# SAN NEW ANGEL - Devlog

## 🗓️ 2026-11-12 (Day 12：破而后立与代码运行的罗生门)

今日是充满波折与顿悟的一天。在经历了项目环境崩溃、群友的技术指导以及漫长的排查后，终于完成了核心逻辑的初步跑通。

### 🎨 美术进度
- 完成了新的像素素材绘制，进一步丰富了游戏的美术资产库。

### 💻 引擎实战与排错记录
因旧项目遗留的无数报错与节点冲突，今晚痛定思痛，**彻底删除了旧工程，从零新建了纯净项目。**

但在测试基础的节点移动逻辑时，遭遇了极其经典的“新手罗生门”：
1. **求助社区**：咨询了其他社区开发者后，有一位大佬看了代码，觉得逻辑本身没有任何问题。
2. **玄学卡壳**：但问题是，程序就是死活跑不起来，画面毫无反应。
3. **我的推断**：我目前的推断是，因为我是跟着 UP 主的视频教程敲代码，但由于我们双方的软件操作（如节点树层级、脚本挂载对象等）存在细微区别，导致我新填入的代码运行失败了。
4. **最终破局**：经过反复对照排查，修正了脚本挂载的位置与运行逻辑，最终成功让节点在屏幕上动了起来。

### 💡 开发者心语
今天深刻体会到了独立开发中“环境清理”与“有效求助”的重要性。从无数次“死活动不了”的自我怀疑，到最后亲眼看着程序跑通，踩过的坑都是宝贵的经验。代码是不会骗人的，跑不通只是因为哪里没对齐。

---
*Stay hungry, stay foolish. 踩过的坑，终将变成塑造世界的地基。*
<img width="1200" height="11486" alt="2e3f7dddb3ead1cceaa2a3017a24b436_720" src="https://github.com/user-attachments/assets/2c9b2727-0e6e-4a46-a8d1-83e5b46e2fb7" />
<img width="1200" height="11591" alt="ab8652717dde33293e3070293d596361_720" src="https://github.com/user-attachments/assets/8ddbd445-fedf-43ce-9aad-5c849a4d4384" />
<img width="1200" height="11444" alt="4e575129270952106f544e3026ff9379_720" src="https://github.com/user-attachments/assets/60c6249f-1c0e-4778-9e49-5f7ed47bb7fe" />
<img width="1200" height="11700" alt="e7c4811008969fb4f59831ee9f415299_720" src="https://github.com/user-attachments/assets/cd810471-9e3f-45b2-ac3f-b2c8d7a653bf" />
<img width="1200" height="11527" alt="693b0ec58d6c05232d18d248948785a6_720" src="https://github.com/user-attachments/assets/8d8ea555-c85c-4fdb-99f6-2e86ca47e216" />
<img width="1200" height="11509" alt="4aaf78b1c920b655b6959161b8a02c56_720" src="https://github.com/user-attachments/assets/342538a8-7c88-4b4e-9d22-aae1536016ea" />
<img width="1200" height="11609" alt="1eaa7d99b985715c17756feea1aada78_720" src="https://github.com/user-attachments/assets/b5fe85d1-204a-47bc-98e0-36fff6835997" />
<img width="873" height="1920" alt="652b2e1c25b9a8d93953136048457d35_720" src="https://github.com/user-attachments/assets/8fe65945-8694-454a-bd31-773787ac100c" />

<img width="1280" height="960" alt="5b30134ca153dc774245eb964be1251f_720" src="https://github.com/user-attachments/assets/742d9974-e360-438c-880d-84d0a4019d30" />

<img width="1280" height="1707" alt="8ab61c1105d29677a1a93d8f6daffe6e_720" src="https://github.com/user-attachments/assets/fe2adf4f-32ba-4cdf-8785-9e9e9f5e935e" />

<img width="1280" height="1707" alt="9c4ae10b5c40e7c3145f5c212c7af53b_720" src="https://github.com/user-attachments/assets/f1c8ca66-9270-4a6e-bca8-b38d25e5fe45" />
<img width="1280" height="960" alt="4084fdf71bae22c0aa81722a5b09dd54_720" src="https://github.com/user-attachments/assets/7f95ca8b-0ef4-475c-ab0c-5508a0ccf791" />
<img width="1280" height="960" alt="13ac32415e0e73d2cf8559f5bfc58822_720" src="https://github.com/user-attachments/assets/54a2a95b-d32a-477a-9433-30238115fa9e" />

<img width="873" height="1920" alt="424f2834969c9c66fe1ca68ae87e2e77_720" src="https://github.com/user-attachments/assets/01872467-5719-4ac2-8bf0-e40b34132763" />

<img width="873" height="1920" alt="42ac9d379938398fd3e0c8551ab4355c" src="https://github.com/user-attachments/assets/c7f19993-7898-4e93-8762-c8f885814e1e" />

<img width="1280" height="960" alt="2393918eaf2e3333b6cc6285b3bd257c_720" src="https://github.com/user-attachments/assets/7b8fac10-cf67-42c8-bcc3-ea4c14645c42" />

# SAN NEW ANGEL - Devlog

## 🗓️ 2026-11-13 (Day 13：环境排雷与基础逻辑初探)

今日整体开发进度较小。白天及傍晚因处理部分个人事务，以及遭遇电脑系统级弹窗报错等突发情况，导致原定的开发时间被大幅压缩。

### 🎨 美术进度
- 对前期绘制的部分像素资产进行了细节优化，增加描边与高光，提升了整体的立体感与视觉质感。

### 💻 引擎实战与逻辑突破
1. **坐标与基础移动**：深入理解了二维坐标轴的概念，并成功通过代码让精灵节点在 X 轴与 Y 轴上同时进行移动，实现了斜向位移。
2. **条件判断（if）初探**：开始尝试在 `_process` 中加入 `if` 条件判断语句（如判断 X 坐标是否大于等于屏幕宽度），试图实现边界检测与坐标重置的循环逻辑。

### 🚑 踩坑复盘
在编写条件判断代码时，再次遭遇了经典的报错组合拳：
- 标点符号错误：误使用了中文全角冒号，导致语法解析失败。
- 层级缩进错误：`if` 语句下方的执行代码没有正确缩进，导致引擎报错 `Expected indented block`。最终通过严格排查缩进层级，修回了代码。

### 💡 开发者心语
现实环境中的杂事是开发路上极大的阻力。虽然今日代码推进幅度有限，但夯实了 `if` 判断和缩进层级的基础逻辑。每天进步一点点，保持手感。

---
*Stay hungry, stay foolish. 踩过的坑，终将变成塑造世界的地基。*
<img width="1280" height="960" alt="f5b1cb8e02e8fd301efe85e82da557ff_720" src="https://github.com/user-attachments/assets/40875ff9-92b6-4a00-adf9-9054baa7397e" />

<img width="1280" height="960" alt="4de151113ae6df4f0a81bfe10ef47627_720" src="https://github.com/user-attachments/assets/2dc5d415-6d71-49f9-9b76-25b7efcfd9f7" />


<img width="1280" height="1707" alt="f2d7315027e3b4fe7cd91b501dc7a9c3_720" src="https://github.com/user-attachments/assets/cdf8d379-c1ae-4817-88a2-a0f9e9cf7665" />

<img width="1280" height="1707" alt="b9606ef82773b7c926da4f57e9808f96_720" src="https://github.com/user-attachments/assets/69bcfc86-6e9b-4fcb-8657-f135519b686e" />


<img width="1280" height="1707" alt="8428e693af07e2444fe5094a4c2695ac_720" src="https://github.com/user-attachments/assets/5aa07686-2ef3-498f-aaf5-5c5588d07ac0" />

<img width="873" height="1920" alt="c43fd12d9564f0cf9f6b13ba7d12eb04_720" src="https://github.com/user-attachments/assets/2daa685f-3df9-4c35-befa-ef2eb12fcef8" />

<img width="873" height="1920" alt="62cb255a27cf8c3ce928f31471da68f9_720" src="https://github.com/user-attachments/assets/56bafa8b-a4a6-4d2d-a848-b18d0850b574" />

<img width="1920" height="1920" alt="3bcc733dfbd9a5d9ba804f10d0157bde" src="https://github.com/user-attachments/assets/dac56cb8-e775-43b0-b201-d5a93e6b694f" />




