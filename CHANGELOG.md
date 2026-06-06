# 更新日志

本文件记录 AstrBot 数学函数绘图插件的所有重要变更。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，版本号遵循语义化版本。

---

## [v1.1.1] - 2026-06-06

### 修复

- 补充 `requirements.txt` 缺失的 `plotly` 和 `kaleido` 依赖（感谢 @A-kirami 的 PR [#1](https://github.com/D1ff1culTT/astrbot_plugin_math_plotter/pull/1)）

### 新增

- `CHANGELOG.md` 更新日志文件

---

## [v1.1.0] - 2026-06-06

### 新增

- **二维向量示意图**：LLM 工具 `plot_vector_2d` + 指令 `/vector`
  - 带实心三角箭头的线段，箭头在终点位置
  - 支持任意起点→终点（不限于原点出发）
  - 每个向量可自定义颜色和文字标签
  - 标签自动放在终点附近，避免与箭头重叠
- **三维向量示意图**：LLM 工具 `plot_vector_3d` + 指令 `/vector3d`
  - plotly 渲染，线段末端配锥体箭头
- **向量加法演示**：LLM 工具 `plot_vector_addition` + 指令 `/vector_add`
  - 平行四边形法则可视化，虚线辅助线 + 结果向量（绿色）
- **向量数乘演示**：LLM 工具 `plot_vector_scaling` + 指令 `/vector_scale`
  - 原向量（灰色）与缩放向量（彩色）对比，支持负数反向
- **基变换演示**：LLM 工具 `plot_basis_transform` + 指令 `/basis`
  - 标准基 e1, e2 与新基 b1, b2 同框对比
- **文本清洗机制**：`_sanitize_math_text()` 将 Unicode 上下标（₁ ₂ ³ 等）自动转为 ASCII，防止 matplotlib 渲染方框
- README 新增「向量绘图」章节

### 修复

- 修复 `vector_add`、`vector_scale`、`basis` 中负值向量坐标轴只显示第一象限的问题（轴范围计算改用 min/max 动态推算）
- 修复 LLM 传入的 Unicode 下标（如 `title='...e₁,e₂...'`）在标题中显示方框
- 修复向量定义中标签名含 Unicode 下标（如 `vectors='3,4:red:v₁'`）在图中显示方框

### 变更

- 所有 15 条指令均添加 `desc` 描述，适配 AstrBot 插件面板展示
- 向量标签/标题全部改用纯文本表示（`v1`, `v2`, `e1`, `e2` 等），不再依赖 mathtext 数学渲染引擎

---

## [v1.0.0] - 2026-06-06

### 新增

- 首个正式版本，支持 11 种坐标系/绘图模式

#### 2D 绘图
- `plot_function` / `/plot` — 一元函数 y=f(x)，支持隐式方程 F(x,y)=0 和多函数对比
- `plot_multiple` — 多函数同框对比（最多 6 条）
- `plot_implicit` — 隐式方程图像
- `plot_polar` / `/polar` — 极坐标 r=f(θ)
- `plot_parametric` / `/parametric` — 参数方程 (x(t), y(t))
- `plot_vector_field_2d` / `/vector2d` — 二维矢量场

#### 3D 绘图 (plotly 引擎)
- `plot_3d_function` / `/plot3d` — 三维曲面 z=f(x,y)
- `plot_3d_multiple` / `/plot3dm` — 多三维曲面叠加
- `plot_3d_spherical` / `/spherical` — 球坐标曲面 r=f(θ,φ)
- `plot_implicit_3d` / `/implicit3d` — 隐式三维曲面 F(x,y,z)=0
- `plot_3d_parametric` / `/parametric3d` — 三维参数曲线
- `plot_status` / `/plot_status` — 插件状态查看

#### 其他
- 支持坐标轴标签自定义（`xlabel`, `ylabel`, `zlabel`）
- 支持 `^` 幂运算符自动转换
- 支持 `max`/`min` 函数自动映射为 SymPy Max/Min
- 可配置 DPI、线宽、网格透明度、3D 渲染参数等

[Unreleased]: https://github.com/D1ff1culTT/astrbot_plugin_math_plotter/compare/v1.1.0...HEAD
[v1.1.0]: https://github.com/D1ff1culTT/astrbot_plugin_math_plotter/compare/v1.0.0...v1.1.0
[v1.0.0]: https://github.com/D1ff1culTT/astrbot_plugin_math_plotter/releases/tag/v1.0.0
