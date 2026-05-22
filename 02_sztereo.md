# Hogyan lehet 2D képből 3D információt kinyerni?

## Sztereo kamera

<p align="center"><img src="https://www.researchgate.net/profile/Koh-Hosoda/publication/237740604/figure/fig4/AS:667857088180236@1536240946625/Model-of-parallel-stereo-camera.png"/></p>

(Forrás: https://www.researchgate.net/publication/237740604_Visual_Tracking_of_Unknown_Moving_Object)


## Példa: Intel Realsense

![](https://www.realsenseai.com/wp-content/uploads/2025/07/D435i.png)

Próbáljuk ki!

1. Csatlakoztassuk a RealSense kamerát a számítógéphez!
2. Indítsuk el a következő launch fájlt:

    ```
    ros2 launch aruco_demo realsense_demo_launch.py
    ```

---------------------------------------------------------------------
[<<<](01_kamera_modell.md) | [^^^](README.md) | [>>>](03_ismert_meret.md)