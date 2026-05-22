[<<](07_aruco_follower.md) | [^](README.md) | [>>](09_aruco_follower_task_2.md)

# ArUco follower ROS node

## 1. feladat: Sebességparancs publikálása

```C++
void ArucoFollowerNode::publishVelocity(double lin_speed, double ang_speed)
{
    // ------------------------------------------------------------------------
    // TODO 1: Create and publish a geometry_msgs::msg::Twist message with the 
    //         specified linear and angular speeds
    // ------------------------------------------------------------------------

    // --- USER CODE BEGIN --- 

    // --- USER CODE END ---
}

```

### Fordítsuk le és próbáljuk ki!

```bash
# Terminal 1:
colcon build --symlink-install
ros2 launch aruco_demo aruco_follower_launch.py

# Terminal 2:
ros2 topic echo /cmd_vel
```

---------------------------------------------------------------------
[<<](07_aruco_follower.md) | [^](README.md) | [>>](09_aruco_follower_task_2.md)
