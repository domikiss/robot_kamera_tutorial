[<<](09_aruco_follower_task_2.md) | [^](README.md) | [>>](11_aruco_follower_task_4.md)

# ArUco follower ROS node

## 3/1. feladat: Orientációszabályozás (szögsebesség számítása)

```C++
void ArucoFollowerNode::timerCallback()
{
// [...]

    geometry_msgs::msg::Point target_point;
    target_point.x = target_pose_transformed.pose.position.x;
    target_point.y = target_pose_transformed.pose.position.y;
    target_point.z = 0.0;

// [...]

    // ----------------------------------------------------------------------------------------------------
    // TODO 3: Calculate angular velocity command based on the target point direction in the robot's frame
    // ----------------------------------------------------------------------------------------------------

    double lin_speed = 0.0;
    double ang_speed = 0.0;

    // --- USER CODE BEGIN --- 


    // --- USER CODE END ---

// [...]
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

## 3/2. feladat: Távolságszabályozás (sebesség számítása)

```C++
void ArucoFollowerNode::timerCallback()
{
// [...]

    geometry_msgs::msg::Point target_point;
    target_point.x = target_pose_transformed.pose.position.x;
    target_point.y = target_pose_transformed.pose.position.y;
    target_point.z = 0.0;
    
// [...]


    // ------------------------------------------------------------------------------------
    // TODO 4: Calculate linear velocity command based on the distance to the target point
    // ------------------------------------------------------------------------------------

    // --- USER CODE BEGIN ---

  
    // --- USER CODE END ---


// [...]
}
```

### Fordítsuk le és próbáljuk ki!

```bash
# Host PC terminal 1:
colcon build --symlink-install
ros2 launch aruco_demo aruco_follower_launch.py

# Host PC terminal 2:
ros2 topic echo /cmd_vel
```



---------------------------------------------------------------------
[<<](09_aruco_follower_task_2.md) | [^](README.md) | [>>](11_aruco_follower_task_4.md)
