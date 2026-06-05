# AstrBot 数学函数绘图插件

将数学公式、函数表达式绘制为高质量图像，AI 辅导/教学时自动调用。支持 2D、3D、极坐标、参数方程、矢量场等多种绘图模式。

---

## AI 生成声明

> **本插件 100% 由 AI（大型语言模型）生成代码**，包括插件主体、工具定义、配置逻辑和文档。未经过专业安全审计或人工代码审查。

## 免责声明

1. **不提供任何保证**：本插件按"原样"提供，不附带任何明示或暗示的担保，包括但不限于适销性、特定用途适用性和非侵权性保证。
2. **使用风险自负**：使用者应自行承担使用本插件所带来的所有风险和责任。作者/AI 不对因使用或无法使用本插件而导致的任何直接、间接、附带、特殊或后果性损害承担责任。
3. **API 费用**：AI API 调用可能产生费用，使用者应自行了解和承担相关费用。

---

## 安装

1. 将插件目录放入 AstrBot 的 `data/plugins/` 下
2. 安装依赖：
   ```bash
   pip install -r requirements.txt
   ```
3. 重启 AstrBot

## 支持的绘图模式

### 2D 绘图

| 命令 | 说明 | 示例 |
|------|------|------|
| `/plot <expr>` | 一元函数 y=f(x) | `/plot sin(x)` |
| `/plot <e1>,<e2>` | 多函数对比 | `/plot sin(x),cos(x),x**2` |
| `/polar <expr>` | 极坐标 r=f(θ) | `/polar sin(3*theta)` |
| `/parametric <x>,<y>` | 参数方程 (x(t), y(t)) | `/parametric cos(t),sin(t)` |
| `/vector2d <Fx>,<Fy>` | 二维矢量场 | `/vector2d -x,-y` |

### 3D 绘图 (plotly 引擎)

| 命令 | 说明 | 示例 |
|------|------|------|
| `/plot3d <expr>` | 三维曲面 z=f(x,y) | `/plot3d sin(sqrt(x**2+y**2))` |
| `/plot3dm <e1>,<e2>,...` | 多曲面叠加 | `/plot3dm x**2+y**2,sqrt(x**2+y**2)` |
| `/spherical <expr>` | 球坐标曲面 r=f(θ,φ) | `/spherical cos(theta)` |
| `/parametric3d <x>,<y>,<z>` | 三维参数曲线 | `/parametric3d cos(t),sin(t),t/5` |
| `/implicit3d <eq>` | 隐式3D曲面 F(x,y,z)=0 | `/implicit3d x**2+y**2+z**2-1` |

### 隐式方程

| 命令 | 说明 | 示例 |
|------|------|------|
| `/plot <eq>` | 隐式方程 F(x,y)=0 | `/plot x**2+y**2-1` (圆) |

### 效果展示
<img width="1213" height="733" alt="1297b393547e0392260b0066bed58521" src="https://github.com/user-attachments/assets/e5028793-eb9c-4965-b2d1-d47932e1c60c" />
一元函数

<img width="1012" height="654" alt="4a7c58a702bb717f42707c87d093e86f" src="https://github.com/user-attachments/assets/88b26bee-7adb-4667-a74f-01da0b390763" />
多函数对比

<img width="1200" height="1200" alt="891915fd3185a81b0eabcb056958048b" src="https://github.com/user-attachments/assets/2742fb17-0e32-4f38-a9e0-139f757ca87f" />
极坐标

<img width="1213" height="733" alt="5b8efffef922c30d5fdd7d8ac9b954a7" src="https://github.com/user-attachments/assets/74179a60-af30-474e-b768-a9031da342a1" />
参数方程

<img width="952" height="654" alt="ada15501d8daaceb181017b2046574db" src="https://github.com/user-attachments/assets/7952d3a3-ccfa-44b6-829d-b07dc173617c" />
二维矢量场

<img width="1440" height="1080" alt="059de18487ffd813a3e73de9727ef967" src="https://github.com/user-attachments/assets/c7569a2c-d2d2-44c3-9361-f6e2bf31d271" />
三维曲面

<img width="1440" height="1080" alt="c0b1b82988c9035c0ffa33fe4cd232cc" src="https://github.com/user-attachments/assets/2edb0813-5721-4278-bc64-d903429b4fa3" />
多曲面叠加

<img width="1440" height="1080" alt="b69399ea266fcd26aea58c1ffbdc132c" src="https://github.com/user-attachments/assets/52385385-89c1-46ce-bd0a-b3c937b9236c" />
球坐标曲面

<img width="1440" height="1080" alt="df003cb8ec8d78be443481eb6e2245a6" src="https://github.com/user-attachments/assets/dabe19bd-7cad-4a99-8c60-f1dd36ccd160" />
三维参数曲线

<img width="1440" height="1080" alt="0b7ee812123473c3e08b87663bd52c7e" src="https://github.com/user-attachments/assets/14f33675-228f-458e-9936-e4cb0520ff89" />
隐式3D曲面

<img width="1440" height="1080" alt="a6a2ffec00b07e691d521e23a04b8f5f" src="https://github.com/user-attachments/assets/cba6e471-5cc8-481c-8bc6-9e65f08ac2a8" />
隐式方程

## 支持的数学函数与常量

`sin`, `cos`, `tan`, `exp`, `log`, `sqrt`, `abs`, `max`, `min`, `Heaviside`, `sign`, `Piecewise`, `pi`, `E`, `e`, `Max`, `Min`

支持 `^` 幂运算符（自动转为 `**`）。

## 坐标轴标签

所有绘图工具支持可选参数 `xlabel`、`ylabel`、`zlabel`（3D 工具），在 AI 调用时传入：
```
plot_function(expression="sin(x)", xlabel="时间 (s)", ylabel="振幅")
```

## 助手命令

| 命令 | 说明 |
|------|------|
| `/plot_status` | 查看插件状态（缓存图像数、DPI等） |

## LLM 工具列表

AI 可自动调用以下工具（通过 `@filter.llm_tool` 注册）：

| 工具名 | 用途 |
|--------|------|
| `plot_function` | 一元函数图像 |
| `plot_multiple` | 多函数对比图像 |
| `plot_implicit` | 隐式方程图像 |
| `plot_3d_function` | 三维曲面 |
| `plot_polar` | 极坐标图像 |
| `plot_parametric` | 参数方程图像 |
| `plot_3d_spherical` | 球坐标曲面 |
| `plot_vector_field_2d` | 二维矢量场 |
| `plot_3d_multiple` | 多3D曲面叠加 |
| `plot_implicit_3d` | 隐式三维曲面 |
| `plot_3d_parametric` | 三维参数曲线 |

## 配置项

在 AstrBot 插件配置中可调整：

| 配置键 | 默认值 | 说明 |
|--------|--------|------|
| `plot_dpi` | 120 | 图像分辨率 |
| `default_x_range` | `-10,10` | 默认 x 轴范围 |
| `line_width` | 2.0 | 曲线线宽 |
| `grid_alpha` | 0.3 | 网格透明度 |
| `plot_3d_grid_density` | 200 | 3D 曲面采样密度 |
| `plot_3d_cmap` | `viridis` | 3D 曲面配色方案 |
| `plot_3d_alpha` | 0.88 | 3D 曲面透明度 |
| `plot_3d_elev` | 25 | 3D 仰角（度） |
| `plot_3d_azim` | -60 | 3D 方位角（度） |

## 依赖

- matplotlib ≥ 3.7.0
- numpy ≥ 1.24.0
- sympy ≥ 1.11.0
- plotly ≥ 6.0
- kaleido ≥ 1.0 (plotly 静态图片导出)

## 许可

MIT
