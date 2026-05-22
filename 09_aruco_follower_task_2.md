[<<](08_aruco_follower_task_1.md) | [^](README.md) | [>>](10_aruco_follower_task_3.md)

# ArUco follower ROS node

## 2. feladat: Adott marker keresése a fogadott detekciós üzenetben

A markerdetekció és a sebességparancsok számításának logikáját `timerCallback()` függvényben kell megvalósítani.

Először keressük meg a legutóbb beérkezett `aruco_opencv_msgs::msg::ArucoDetection` típusú üzenetben (`last_detection` tagváltozó) az általunk keresett markert (`marker_id_to_follow` tagváltozó)!

```C++
void ArucoFollowerNode::timerCallback()
{
    std::lock_guard<std::recursive_mutex> lock(mtx);

    // Check if we have a valid detection and if it's not too old

    if (!last_detection_valid)
    {
        publishVelocity(0.0, 0.0);
        return;
    }

    if (last_detection_valid && (get_clock()->now() - last_detection_time).seconds() > detection_timeout_sec)
    {
        // If the last detection is too old, stop the robot
        RCLCPP_INFO(get_logger(), "No markers detected in the last %g seconds: publishing zero velocity", detection_timeout_sec);
        publishVelocity(0.0, 0.0);
        last_detection_valid = false;   // Reset the flag since the detection is now considered stale
        return;
    }


    // ------------------------------------------------------------------------
    // TODO 2: Search for the specified marker ID
    // ------------------------------------------------------------------------

    marker_found = false;
    int marker_index = -1;

    // Write code to search for marker_id_to_follow in last_detection.markers

    // --- USER CODE BEGIN --- 


    // --- USER CODE END ---
    

    if (!marker_found)
    {
        // If the specified marker is not found, stop the robot
        RCLCPP_INFO(get_logger(), "Markers detected but marker ID %d not found: publishing zero velocity", marker_id_to_follow);
        publishVelocity(0.0, 0.0);
        return;
    }

    RCLCPP_INFO(get_logger(), "Following marker ID: %d", last_detection.markers[marker_index].marker_id);
    


    // Transform the marker pose to the robot's base frame (base_link)

    geometry_msgs::msg::PoseStamped target_pose;
    target_pose.header = last_detection.header;
    target_pose.pose = last_detection.markers[marker_index].pose;

    geometry_msgs::msg::PoseStamped target_pose_transformed;

    try
    {
        target_pose_transformed = tf_buffer->transform(target_pose, "base_link", tf2::durationFromSec(0.1));
    }
    catch (tf2::TransformException& ex)
    {
        RCLCPP_WARN(get_logger(), "Failed to transform marker pose: %s", ex.what());
        publishVelocity(0.0, 0.0);
        return;
    }

    geometry_msgs::msg::Point target_point;
    target_point.x = target_pose_transformed.pose.position.x;
    target_point.y = target_pose_transformed.pose.position.y;
    target_point.z = 0.0;


    // Publish visualization marker for the target direction
    std_msgs::msg::ColorRGBA color;
    color.a = 0.5; color.r = 0.0; color.g = 0.7; color.b = 0.7;
    marker_publisher->publish(createArrowMarker(target_point, "base_link", color, 0));

// [...]
}
```

### Fordítsuk le és próbáljuk ki!

```bash
# Terminal 1:
colcon build --symlink-install
ros2 launch aruco_demo aruco_follower_launch.py
```

Szükség esetén módosítsuk a keresett marker ID-t az `aruco_follower_launch.py` fájlban:

```Python
    aruco_follower_cmd = Node(
      package='aruco_demo',
      executable='aruco_follower_node',
      name='aruco_follower',
      output='screen',
      parameters=[{ 'marker_id_to_follow': 0,
                    'max_lin_speed_m_s': 0.1,
                    'max_ang_speed_rad_s': 1.0,
                    'angle_control_gain': 2.0,
                    'distance_control_gain': 0.5,
                    'control_period_sec': 0.1,
                    'detection_timeout_sec': 0.5,
                    }]
    )
```


---------------------------------------------------------------------
[<<](08_aruco_follower_task_1.md) | [^](README.md) | [>>](10_aruco_follower_task_3.md)
