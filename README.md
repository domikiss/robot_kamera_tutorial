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
    - aruco_follower node átnézése
    - cmd_vel publikálás
    - Adott marker keresése
    - szögsebesség-parancs számítása
    - sebességparancs számítása
    - Tesztelés lokális gépen
    - Csatlakozás a GoPiGo3-hoz (SSH)
    - ROS_DOMAIN_ID beállítása a roboton
    - gopigo3_bringup
    - Tesztelés a gopigo-n


---------------------------------------------------------------------
_Megjegyzés:_

A mérésen a ROS2 keretrendszer a Zenoh RMW-t (ROS Middleware) használja a kommunikációhoz. Ezért mindig futnia kell egy ún. Zenoh router-nek a háttérben, különben nem fognak működni a ROS2 funkciók.

```bash
ros2 run rmw_zenoh_cpp rmw_zenohd
```
