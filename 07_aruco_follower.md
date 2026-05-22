[<<](06_aruco_demo.md) | [^](README.md) | [>>](08_aruco_follower_task_1.md)

# ArUco follower ROS node

Nyissuk meg a következő fájlokat az editorban:
- `aruco_demo/src/aruco_follower_main.cpp`
- `aruco_demo/include/aruco_demo/aruco_follower_node.hpp`
- `aruco_demo/src/aruco_follower_node.cpp`

Mit látunk?

## main() függvény

`aruco_follower_main.cpp` :

```C++
#include "rclcpp/rclcpp.hpp"
#include "aruco_demo/aruco_follower_node.hpp"

using namespace aruco_follower;

int main(int argc, char const* argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<ArucoFollowerNode>());
  rclcpp::shutdown();
  return 0;
}

```

## ArucoFollowerNode osztály

`aruco_follower_node.hpp` :

```C++
namespace aruco_follower
{
class ArucoFollowerNode : public rclcpp::Node
{

public:
    ArucoFollowerNode();
    ~ArucoFollowerNode();


// [...]
```

Privát metódusok:

```C++
private:

    void initParams();

    void publishVelocity(double lin_speed, double ang_speed);

    void arucoDetectionCallback(const aruco_opencv_msgs::msg::ArucoDetection& msg);
    void timerCallback();

// [...]
```
Subscriber, publisher objektumok (privát tagváltozók):

```C++
    rclcpp::Subscription<aruco_opencv_msgs::msg::ArucoDetection>::SharedPtr aruco_detection_subscriber;
    rclcpp::Publisher<geometry_msgs::msg::Twist>::SharedPtr velocity_publisher;
    rclcpp::Publisher<visualization_msgs::msg::Marker>::SharedPtr marker_publisher;

// [...]
```

További privát tagváltozók:

```C++
    std::shared_ptr<tf2_ros::TransformListener> tf_listener;
    std::unique_ptr<tf2_ros::Buffer> tf_buffer;

    rclcpp::TimerBase::SharedPtr timer;
    std::recursive_mutex mtx;

    int marker_id_to_follow;
    double max_lin_speed, max_ang_speed;

    double detection_timeout_sec;
    aruco_opencv_msgs::msg::ArucoDetection last_detection;
    bool last_detection_valid = false;
    rclcpp::Time last_detection_time;
    bool marker_found = false;
    rclcpp::Time last_marker_found_time;

};
}  // namespace aruco_follower
```



### Nézzük meg az implementációt!

`aruco_follower_node.cpp` :

Konstruktor:

```C++
ArucoFollowerNode::ArucoFollowerNode() : Node("aruco_follower_node")
{
    initParams();

    aruco_detection_subscriber = create_subscription<aruco_opencv_msgs::msg::ArucoDetection>(
        get_parameter("aruco_detection_topic_name").as_string(), 10,
        std::bind(&ArucoFollowerNode::arucoDetectionCallback, this, _1));

    velocity_publisher = create_publisher<geometry_msgs::msg::Twist>(get_parameter("velocity_cmd_topic_name").as_string(), 10);

    marker_publisher = create_publisher<visualization_msgs::msg::Marker>("target_dir_marker", 10);

    tf_buffer = std::make_unique<tf2_ros::Buffer>(get_clock());
    tf_listener = std::make_shared<tf2_ros::TransformListener>(*tf_buffer);

    max_lin_speed = get_parameter("max_lin_speed_m_s").as_double();
    max_ang_speed = get_parameter("max_ang_speed_rad_s").as_double();
    detection_timeout_sec = get_parameter("detection_timeout_sec").as_double();
    marker_id_to_follow = get_parameter("marker_id_to_follow").as_int();

    timer = create_wall_timer(get_parameter("control_period_sec").as_double() * 1s,
                              std::bind(&ArucoFollowerNode::timerCallback, this));
}
```

ROS node paraméterek deklarálása és alapértelmezett értékek beállítása:

```C++
void ArucoFollowerNode::initParams()
{
    declare_parameter("aruco_detection_topic_name", "/aruco_detections");
    declare_parameter("velocity_cmd_topic_name", "/cmd_vel");

    declare_parameter("control_period_sec", 0.1);
    declare_parameter("detection_timeout_sec", 1.0);

    declare_parameter("angle_control_gain", 2.0);
    declare_parameter("distance_control_gain", 0.5);

    declare_parameter("max_lin_speed_m_s", 0.2);
    declare_parameter("max_ang_speed_rad_s", 1.0);

    declare_parameter("marker_id_to_follow", 0);

    declare_parameter("debug_mode", false);
}
```

Callback függvény az ArUco detekciók feldolgozására:

```C++
void ArucoFollowerNode::arucoDetectionCallback(const aruco_opencv_msgs::msg::ArucoDetection& msg)
{
    std::lock_guard<std::recursive_mutex> lock(mtx);

    if (!msg.markers.empty())
    {
        if (get_parameter("debug_mode").as_bool()) {
            RCLCPP_INFO(get_logger(), "Detected %zu markers", msg.markers.size());
        }
        last_detection_time = get_clock()->now();
        last_detection = msg;
        last_detection_valid = true;     // Set the flag to indicate that a marker has been detected at least once
    }
}

```

---------------------------------------------------------------------
[<<](06_aruco_demo.md) | [^](README.md) | [>>](08_aruco_follower_task_1.md)
