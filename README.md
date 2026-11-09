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
因你而存在的致爱♪: 11-09 22:42:03
<img src="file://C:\Users\孟乐\Documents\Tencent Files\3983349379\nt_qq\nt_data\Pic\2026-11\Ori\f1cc224945278c89eaa21a5af8807043.jpg" />

因你而存在的致爱♪: 11-09 22:42:03
<img src="file://C:\Users\孟乐\Documents\Tencent Files\3983349379\nt_qq\nt_data\Pic\2026-11\Thumb\c91f8b8ed26bf13f9520d4e3c7f36712_720.jpg" />

因你而存在的致爱♪: 11-09 22:42:04
<img src="file://C:\Users\孟乐\Documents\Tencent Files\3983349379\nt_qq\nt_data\Pic\2026-11\Thumb\d3b9bde8ce5aa7be1b9b2c9de75fd5d6_720.jpg" />

因你而存在的致爱♪: 11-09 22:42:04
<img src="file://C:\Users\孟乐\Documents\Tencent Files\3983349379\nt_qq\nt_data\Pic\2026-11\Thumb\defe07fbbc91f1a0d154c75de89425ce_720.jpg" />

因你而存在的致爱♪: 11-09 22:42:05
<img src="file://C:\Users\孟乐\Documents\Tencent Files\3983349379\nt_qq\nt_data\Pic\2026-11\Thumb\63243d68a6c4e44c4990db6456bd1920_720.jpg" />

因你而存在的致爱♪: 11-09 22:42:05
<img src="file://C:\Users\孟乐\Documents\Tencent Files\3983349379\nt_qq\nt_data\Pic\2026-11\Thumb\a312a0ab3b86528d7b7ee3ccf33b051b_720.jpg" />
