[<<](04_aruco.md) | [^](README.md) | [>>](06_aruco_demo.md)

# Kamerakalibráció

Indítsuk el az alábbi ROS node-okat:

```bash
# Terminal 1:
ros2 run usb_cam usb_cam_node_exe

# Terminal 2:
ros2 run camera_calibration cameracalibrator --size 4x6 --square 0.04 --ros-args -r image:=/image_raw
```

Vegyük elő a sakktáblát, és mozgassuk különböző pozíciókba. Ügyeljünk a  következőkre:

- A sakktábla legyen mindig sík felületű (ne hajoljon, ne legyen hullámos)
- Legyenek változatos képek:
    - Vízszintes pozíció
    - Függőleges pozíció
    - Méret
    - Függőleges/vízszintes tengely körüli elforgatás (skew)

Ha elég kép készült, akkor "CALIBRATE", majd "SAVE" gombokat nyomjuk meg.

Az elkészült `ost.yaml` fájlt másoljuk az `src/aruco_demo/config` mappába!



---------------------------------------------------------------------
[<<](04_aruco.md) | [^](README.md) | [>>](06_aruco_demo.md)
