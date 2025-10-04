# 1) สร้าง interfaces + msg
mkdir -p ~/interfaces/src
ros2 pkg create com_interfaces --build-type ament_cmake

# ...วาง Move.msg, แก้ package.xml/CMakeLists.txt...
cd ~/interfaces/src/com_interfaces
mkdir msg
cd msg
touch Num.msg
nano Num.msg
วาง   int64 num

colcon build --packages-select school_interfaces
source install/setup.bash
ros2 interface show school_interfaces/msg/Move

# 2) สร้างโหนด Python + launch
ros2 pkg create turtle_move --build-type ament_python --dependencies rclpy geometry_msgs school_interfaces
# ...วาง move_bridge.py, pattern_publisher.py, setup.py, launch/turtle_lab.launch.py...
colcon build --packages-select turtle_move
source install/setup.bash
ros2 launch turtle_move turtle_lab.launch.py speed:=1.2 turtle:=turtle1
