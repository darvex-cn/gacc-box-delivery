# 系统架构

任务模块协调视觉、运控和导航，仿真或硬件提供执行环境。

```text
box_tasks
  ├── box_perception → foundationpose_adapter → FoundationPose
  ├── box_manipulation
  └── box_navigation
                 ↓
       硬件驱动 / 仿真接口
```

- `interfaces` 定义跨模块通信契约。
- `description` 维护机器人模型和坐标系。
- `bringup` 组合整机启动与配置。
- 业务模块通过 ROS 接口协作，避免相互导入内部实现。
- 实机与仿真尽量复用任务逻辑，通过启动参数切换后端。

待确定：ROS 2 发行版、机器人型号、相机、仿真平台、进程边界和运行环境。
