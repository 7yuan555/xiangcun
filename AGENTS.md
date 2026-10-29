# AGENTS.md

- Working directory: `E:\opencode` (fresh workspace; no repo files present yet).
- Add repo-specific commands, structure, and constraints here as the project takes shape.

# 项目 AI 助手配置文档
## 1. 角色设定
你是一位精通现代前端开发与 H5 小游戏开发的专家。
- **技术栈**：纯 HTML5 + CSS3 + 原生 JavaScript（不依赖任何第三方框架或库，保证单文件即可运行）。
- **核心原则**：代码简洁、性能优先、**移动端优先**、**零 Bug**。

## 2. 项目上下文
- **项目主题**：名为《指尖上的振兴》的叙事类交互 H5 小游戏，围绕“乡村振兴”与“传统手艺传承”。
- **文件结构**：所有代码（HTML/CSS/JS）请全部写在一个 `index.html` 文件中，方便直接部署和分享。

## 3. 编码规范
- **响应式**：必须适配手机竖屏，使用 `100vh` 和 `100vw` 作为基础尺寸。
- **交互原则（极为重要）**：**绝对禁止使用复杂的拖拽（Drag）功能**。所有交互只能使用“点击（Click）”、“长按（Long Press）”或“滑块（Input Range）”来实现。
- **视觉**：国风轻水彩风格。前期灰冷色调（表现贫困），后期暖色调（表现振兴）。
- **图片**：所有需要图片的地方，先用带有文字说明的占位色块（如 `<div style="...">【这里放：场景1背景图】</div>`）代替，方便我后续替换。

## 4. 场景与交互逻辑
- **场景1（序章）**：点击屏幕翻页，播放3段背景文字。
- **场景2（转机）**：点击屏幕触发打字机对话，村支书出现并解读政策。
- **场景3（手艺体验）**：使用 `<input type="range">` 滑块，玩家向右滑动滑块完成“刺绣/纺线”进度，获得道具。
- **场景4（致富快进）**：点击按钮，触发“时光飞逝”动画（日历翻页、金币掉落），背景渐变为明亮色调。
- **场景5（情感升华）**：长按屏幕3秒点亮光点，致敬扶贫干部，展示真实故事。

# 核心技术要求：必须完美适配 PC 端与移动端（双端适配）

1. **页面布局与缩放（Viewport）**
   - 必须在 HTML `<head>` 中加入：`<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">`。
   - 全局 CSS 必须设置 `overflow: hidden;` 和 `touch-action: none;`，禁止页面上下滑动和双指缩放，保持 100vh 和 100vw 占满全屏。

2. **PC端居中显示（重点）**
   - 因为手机是竖屏，PC 是横屏，为了防止在电脑上打开时画面被拉伸变形，请将整个游戏的主容器设置：`max-width: 480px; margin: 0 auto; box-shadow: 0 0 20px rgba(0,0,0,0.5);`。这样在电脑上打开，游戏会像手机模拟器一样居中显示，手机端则自动铺满全屏。

3. **交互事件兼容（极其重要）**
   - 请写一个通用的事件监听函数，同时兼容鼠标（PC）和触摸（Mobile）。
   - **点击事件**：PC端用 `onclick`，移动端用 `touchstart`（并加上 `e.preventDefault()` 防止点击穿透和延迟）。
   - **长按事件**：请统一封装 `mousedown`/`touchstart`（开始计时）与 `mouseup`/`touchend`/`touchcancel`（取消计时）的逻辑，确保鼠标长按和手指长按都能正常触发 3 秒倒计时。
   - **防误触**：在 CSS 中加入 `-webkit-user-select: none; user-select: none;` 防止长按时选中文字或弹出手机端的复制/保存图片菜单。

4. **滑块（Input Range）兼容**
   - 第3幕的滑块，请使用原生的 `<input type="range">`，并编写 CSS 隐藏默认样式，自定义一个圆润的滑块按钮，确保鼠标点击拖动和手指滑动都能精准响应。

5. **视觉与动画**
   - 动画优先使用 CSS3 的 `@keyframes` 和 `transition`，以确保在低端手机和电脑浏览器上都能达到 60 帧的流畅度。
