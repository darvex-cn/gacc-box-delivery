# 环境与部署

当前仓库仅含目录骨架，不能直接通过 colcon 构建或启动。

后续接入顺序：

1. 确定 ROS 2、Python、CUDA 与算法环境版本。
2. 初始化 ROS 包的 package.xml 与构建配置。
3. 固定第三方仓库版本并获取模型权重。
4. 配置设备与标定结果。
5. 跑通离线位姿估计，再验证实机或仿真搬运链路。

在仓库根目录使用 `colcon build --base-paths ros_ws/src --build-base ros_ws/build --install-base ros_ws/install` 前，需先完成包初始化。
