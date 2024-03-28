项目采用横纵向解耦的MPC轨迹规划方法，在单向双车道场景下针对动、静态障碍物生成轨迹，直接使用c++调用casadi构建qp问题求解。<br>
预期实现：<br>
    1.参考Openpilot及Apollo框架，在车辆行驶过程中考虑自车与障碍物状态的参考线动态更新<br>
    2.参考Openpilot及Apollo框架，基于简化的车辆运动学建模的横纵向解耦MPC轨迹规划<br>
    3.基于进程通信实现车辆位姿信息的动态显示<br>

--------------------------------------------------------------    安装说明    --------------------------------------------------------------<br>
项目依赖<br>
Casadi,cmake,python及相关库<br>

项目下载：git clone https://github.com/JingyanXing/MPC_TrajectoryPlanning.git && cd MPC_TrajectoryPlanning <br>
在项目MPC_TrajectoryPlanning目录下<br>
~~执行编译指令：cd build && cmake .. && make~~(build文件夹已上传，无需重复编译)<br>
测试是否安装成功：./main<br>

项目main文件中内置两个测试：<br>
```c++
int main(){
    Test test;
    // 横纵向解耦单元测试
    test.latSolverUnitTest();
    // 纵向单元测试
    // test.lonSolverUnitTest();
    return 0;
}
```
🟢更新于2024.03.21--------------------------------------------------------------<br>
实现静态障碍物下参考线生成和轨迹规划<br>

🟢更新于2024.03.26--------------------------------------------------------------<br>
在Test.run方法中初步实现给定静态障碍物环境下车辆参考线的动态更新，规划轨迹的生成<br>
基于socket进行进程间通信实现车辆形心位置动态图像绘制<br>
可视化启用方法：令起终端cd进入visual目录下， 执行 python visualserver.py。可视化服务端唤起，随后在原终端执行./main<br>

TODO:包含车辆轮廓的动态轨迹绘制，车辆速度，加速度，航向角，轮胎转角动态曲线绘制
TODO:动态障碍物跟驰及超车<br>
