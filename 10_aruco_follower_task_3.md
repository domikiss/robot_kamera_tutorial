[<<](09_aruco_follower_task_2.md) | [^](README.md) | [>>](11_aruco_follower_task_4.md)

# ArUco follower ROS node

## 3. feladat: Orientációszabályozás (szögsebesség számítása)

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

### Próbáljuk ki a roboton is!

Csatlakozás a GoPiGo3 robothoz SSH-n (használjuk az adott robothoz tartozó IP címet):

```bash
ssh ubuntu@192.168.100.xx    # xx: 19 vagy 25  (rá van írva a robotra)
```

ROS_DOMAIN_ID lekérdezése: 

```bash
# Host PC terminal:
printenv | grep ROS
```

Olvassuk le a ROS_DOMAIN_ID értékét, majd állítsuk be a GoPiGo3 termináljában (XXX az ID értéke):

```bash
# GoPiGo3 robot terminal (SSH):
export ROS_DOMAIN_ID=XXX
```

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
[<<](09_aruco_follower_task_2.md) | [^](README.md) | [>>](11_aruco_follower_task_4.md)
