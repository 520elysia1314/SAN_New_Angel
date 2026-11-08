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


