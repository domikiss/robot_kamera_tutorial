[<<](10_aruco_follower_task_3.md) | [^](README.md)

# ArUco follower ROS node

## 4. feladat: Próbáljuk ki a roboton is!

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
[<<](10_aruco_follower_task_3.md) | [^](README.md)
