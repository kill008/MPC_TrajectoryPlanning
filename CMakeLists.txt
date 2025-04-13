cmake_minimum_required(VERSION 3.10)
project(MPC_trajectory)
# 在 project() 之后添加
# set(CMAKE_BUILD_TYPE Debug)  # 生成调试信息
# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 17)

# 添加 CasADi 头文件路径（关键修改）
include_directories(
  ${PROJECT_SOURCE_DIR}/map
  ${PROJECT_SOURCE_DIR}/solver
  ${PROJECT_SOURCE_DIR}/vehicle
  ${PROJECT_SOURCE_DIR}/data
  ${PROJECT_SOURCE_DIR}/test
  ${catkin_INCLUDE_DIRS}
  /opt/anaconda3/include  # 添加 Conda 的 include 路径
)

# 添加 CasADi 库路径（如果需要链接）
link_directories(/opt/anaconda3/lib)  # 添加 Conda 的 lib 路径

# 查找当前目录下的所有源文件
aux_source_directory(. DIR_SRCS)

# 添加子目录
add_subdirectory(map)
add_subdirectory(solver)
add_subdirectory(vehicle)
add_subdirectory(data)
add_subdirectory(test)

# 指定生成目标
add_executable(main main.cc)

# 添加链接库（确保链接 casadi）
target_link_libraries(main 
  map 
  solver 
  vehicle 
  data 
  test 
  ${catkin_LIBRARIES}
  casadi  # 链接 CasADi 库
)