# 地狱狂奔 — 马浩然无尽跑酷

小米手环 9 / Vela 系统 · 恐怖风格跑酷小游戏

## 设备规格
- 型号: 小米手环 9 / Xiaomi Band 9
- 系统: Vela（实时操作系统）
- 屏幕: 192 × 490 像素（超狭长竖屏）
- 交互: 触摸屏（点击 = 跳跃 / 开始 / 重新开始）

## 项目结构
```
hell-runner-vela/
├── manifest.json          # 应用清单（Vela 必需）
├── app.json               # 应用配置（项目信息）
└── pages/
    └── index/
        └── index.ux       # 主页面（含 template + script + style）
```

## 游戏玩法
- **点击屏幕**: 跳跃（支持二段跳）
- **撞到障碍**: 游戏结束，再点击重开
- **障碍类型**:
  - 🔺 尖刺石柱
  - 🌵 血色变异仙人掌
  - 👻 漂浮幽灵
  - 🦇 低空恶魔飞鸟
- **分数触发惊悚文字**: 5 / 15 / 30 / 50 / 80 / 120 / 150 / 200 分

## 编译/打包方式

### 方法 1：VelaGen 工具
将整个 `hell-runner-vela/` 目录作为输入：

```
velagen build ./hell-runner-vela/ -o 地狱狂奔.rpk
```

### 方法 2：Vela 官方开发工具
使用小米手环官方开发者工具（Mi Watch Developer Tool）：
- 选择设备：小米手环 9
- 分辨率：192 × 490
- 导入整个项目文件夹

### 方法 3：打包为 .zip
VelaGen 也接受 .zip 文件：
```bash
cd hell-runner-vela
zip -r ../hell-runner.zip manifest.json app.json pages/
```

## 核心设计考虑
1. **极小屏幕 (192×490)**: 所有图形都以像素风绘制，仅用 2-3 层颜色叠加营造恐怖感
2. **手环性能限制**: 纯 Canvas 绘制，没有图像资源，启动即运行；固定 30 FPS
3. **本地存储**: 最高分保存到 `$localStorage`
4. **单交互点**: 只需点击，手环体验流畅

## 技术实现
- 游戏主循环：`setInterval(33ms)`，约 30 FPS
- 玩家物理：重力 + 跳跃力 + 二段跳
- 障碍生成：按分数动态提升难度
- 图像绘制：Canvas 2D Context，纯代码像素画（零图片资源）

## 文件大小
- manifest.json: ~1 KB
- index.ux: ~17 KB（全部游戏逻辑 + Canvas 绘制）
- 合计: ~18 KB 原始代码

## 画面风格说明
- 主角: 马浩然 - 绿色病态皮肤 / 紧闭双眼 / 超长血红舌头 / 黑色短发
- 场景: 暗红地面 + 裂隙血光
- 整体氛围: 阴森 / 压抑 / 惊悚
