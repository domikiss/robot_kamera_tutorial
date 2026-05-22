[<<](03_ismert_meret.md) | [^](README.md) | [>>](05_kalibracio.md)

# Hogyan lehet 2D képből 3D információt kinyerni?

## ArUco markerek

- ArUco: Augmented Reality University of Cordoba
- Könnyen detektálható 2D szimbólumok

<p align="center"><img src="pic/aruco_marker_intro.gif" width="1280"/></p>

*(Forrás: https://towardsdev.com/aruco-marker-generation-and-detection-with-opencv-python-with-newer-updated-version-f801d7dcf211)*



**Próbáljuk ki!**

1. Csatlakoztassuk a Logitech webkamerát a számítógéphez
2. Indítsuk el a launch fájlt, és értelmezzük, hogy mit látunk!

```bash
# Terminal 1:
ros2 launch aruco_demo aruco_demo_launch.py

# Terminal 2:
ros2 topic list
ros2 topic echo /aruco_detections
```

---------------------------------------------------------------------
[<<](03_ismert_meret.md) | [^](README.md) | [>>](05_kalibracio.md)
