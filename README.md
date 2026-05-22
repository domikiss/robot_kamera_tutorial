# Gépi látás a robotikában

__Tartalom__

1. [A pinhole kamera modell](01_kamera_modell.md)
2. Hogyan lehet 2D képből 3D információt kinyerni?
    - [Sztereo kamera](02_sztereo.md)
    - [Ismert méretű objektumok detekciója](03_ismert_meret.md)
    - [ArUco markerek](04_aruco.md)
    - [Kamerakalibráció](05_kalibracio.md)
    - [ArUco demo](06_aruco_demo.md)
3. Mobil robot irányítása gépi látás alapján
    - [ArUco follower ROS node](07_aruco_follower.md)
    - [1. feladat: Sebességparancs publikálása](08_aruco_follower_task_1.md)
    - [2. feladat: Adott marker keresése a fogadott detekciós üzenetben](09_aruco_follower_task_2.md)
    - [3. feladat: Orientációszabályozás (szögsebesség számítása)](10_aruco_follower_task_3.md)
    - [4. feladat: Távolságszabályozás (sebesség számítása)](11_aruco_follower_task_4.md)


---------------------------------------------------------------------
_Megjegyzés:_

A mérésen a ROS2 keretrendszer a Zenoh RMW-t (ROS Middleware) használja a kommunikációhoz. Ezért mindig futnia kell egy ún. Zenoh router-nek a háttérben, különben nem fognak működni a ROS2 funkciók.

```bash
ros2 run rmw_zenoh_cpp rmw_zenohd
```

---------------------------------------------------------------------
[>>](01_kamera_modell.md)