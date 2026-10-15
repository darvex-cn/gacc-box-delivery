<h1 align="center">GACC Box Delivery</h1>

<hr>

<p align="center">
  基于 ROS 2 与 FoundationPose 的机器人箱体搬运工程<br>
  规划集成箱体位姿估计、机械臂抓取、移动导航与仿真验证<br>
  面向堆叠箱子的目标选择、抓取与搬运流程
</p>

<p align="center">
  <a href="#下载与初始化">下载与初始化</a> ·
  <a href="#工程目录">工程目录</a> ·
  <a href="#开发与使用">开发与使用</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/ROS-2-22314E?logo=ros&amp;logoColor=white" alt="ROS 2">
  <img src="https://img.shields.io/badge/FoundationPose-待接入-76B900" alt="FoundationPose 待接入">
  <img src="https://img.shields.io/badge/status-目录骨架-orange" alt="当前状态：目录骨架">
  <a href="https://github.com/darvex-cn/gacc-box-delivery/stargazers"><img src="https://img.shields.io/github/stars/darvex-cn/gacc-box-delivery?style=flat" alt="GitHub stars"></a>
</p>

规划的搬运流程为：相机提供 RGB-D 数据，视觉模块识别候选箱子并估计位姿；任务模块选择搬运目标，协调机械臂抓取、移动导航与放置，完成后重新观察并处理下一个箱子。

当前仓库仅包含目录骨架和说明文档。各 ROS 2 模块尚未初始化构建文件，FoundationPose、模型权重及硬件接口尚未接入，目前没有可执行节点或启动入口。

## 下载与初始化

```bash
git clone https://github.com/darvex-cn/gacc-box-delivery.git
cd gacc-box-delivery
```

仓库已预留 `.gitmodules`，当前尚未配置第三方子模块。后续接入后，可通过以下命令初始化或更新：

```bash
git submodule update --init --recursive
```

## 工程目录

```text
gacc-box-delivery/
├── ros_ws/src/
│   ├── box_interfaces/              # 自定义消息、服务与动作
│   ├── box_perception/              # 视觉感知与箱体位姿估计
│   ├── box_manipulation/            # 抓取规划与机械臂运动
│   ├── box_navigation/              # 移动导航与停靠
│   ├── box_tasks/                   # 搬运任务调度与失败恢复
│   ├── box_description/             # 机器人模型与坐标系
│   ├── box_simulation/              # 仿真场景与配置
│   └── box_bringup/                 # 整机启动与组合配置
├── python_libs/foundationpose_adapter/
├── third_party/
├── assets/objects/
├── calibration/
├── models/foundationpose/
├── data/
│   ├── datasets/
│   └── results/
├── scripts/
├── docker/
├── tests/integration/
└── docs/
```

| 目录 | 用途 |
| --- | --- |
| `ros_ws/src/` | ROS 2 模块：接口、视觉、运控、导航、任务、机器人描述、仿真与整机启动 |
| `python_libs/foundationpose_adapter/` | 与 ROS 解耦的 FoundationPose 适配层 |
| `third_party/` | 固定版本的第三方源码 |
| `assets/objects/` | 箱体等物体的网格、纹理与尺寸元数据 |
| `calibration/` | 按机器人或设备管理的标定结果 |
| `models/` | 本地模型权重及来源说明 |
| `scripts/` | 环境、下载和运行辅助脚本 |
| `docker/` | 容器构建与部署配置 |
| `tests/integration/` | 跨模块与完整流程测试 |
| `data/` | 本地数据集及推理、调试与评估结果 |
| `docs/` | 架构、接口、标定和部署文档 |

空目录通过 `.gitkeep` 保留；`data/` 和 `models/` 保留二级目录占位文件及根目录说明，内部数据与权重默认不提交 Git。构建产物也不提交。
各模块配置放在自身 `config/`，整机启动组合放在 `box_bringup/`。

## 开发与使用

ROS 2 发行版、Python/CUDA 版本、机器人型号与仿真平台尚待确定，当前不能直接通过 `colcon` 构建或启动。后续开发按以下顺序推进：

1. 确定软硬件版本，初始化实际需要的 ROS 2 包。
2. 接入 FoundationPose，使用离线 RGB-D 数据验证箱体位姿估计。
3. 完成相机与手眼标定，打通“相机 → 箱体位姿 → 抓取”流程。
4. 接入导航与任务调度，逐步验证完整搬运流程及仿真运行。

相关设计与接入说明：

- [系统架构](docs/architecture.md)
- [接口约定](docs/interfaces.md)
- [环境与部署](docs/deployment.md)
- [标定约定](docs/calibration.md)
