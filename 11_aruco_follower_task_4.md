[<<](10_aruco_follower_task_3.md) | [^](README.md)

# ArUco follower ROS node

## 4. feladat: Távolságszabályozás (sebesség számítása)

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

### Próbáljuk ki a roboton is!

"Élesszük fel" a robotot:

```bash
# GoPiGo3 robot terminal (SSH):
ros2 launch gopigo3_bringup gopigo3_bringup_launch.py
```

Indítsuk el az alkalmazást a host gépen:

```bash
# Host PC terminal:
ros2 launch aruco_demo aruco_follower_launch.py use_real_robot:=True
```

---------------------------------------------------------------------
[<<](10_aruco_follower_task_3.md) | [^](README.md)
