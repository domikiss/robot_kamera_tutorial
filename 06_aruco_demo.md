# 3D detekció ArUco markerek segítségével


Indítsuk el újra a launch fájlt, és értelmezzük, hogy mit látunk!

```bash
# Terminal 1:
ros2 launch aruco_demo aruco_demo_launch.py

# Terminal 2:
ros2 topic echo /aruco_detections
```

Hihetőek a koordináták? Ha nem, mi lehet a probléma?

Nézzük meg a RealSense kamerával is!

```bash
ros2 launch aruco_demo realsense_demo_launch.py
```

Végezzük el a szükséges módosítást mindkét launch fájlban!


---------------------------------------------------------------------
[<<<](05_kalibracio.md) | [^^^](README.md) | [>>>](07_aruco_follower.md)
