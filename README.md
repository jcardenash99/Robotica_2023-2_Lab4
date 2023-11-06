# Robotica_2023-2_Lab4
## Integrantes

- Wilfer Armando Fiquitiva Mendez.
- Johan Leonardo Castellanos Ruiz.
- Juan Pablo Cardenas Higuera.

## Cinemática 
Inicialmente se define la cinemática directa del robot Pincher teniendo haciendo la representación gráfica de las articulaciones y los eslabones dando una posición inicial que denominaremos HOME.

![](https://github.com/jcardenash99/Robotica_2023-2_Lab4/blob/main/Cinematica%20directa%20pincher.png)

### Figura 1 Cinematica directa robot pincher.

![](https://github.com/jcardenash99/Robotica_2023-2_Lab4/blob/main/Tabla%20D_H%20Pincher.png)

### Tabla 1 parametros D_H robot pincher.
## ROS
´´´
from cmath import pi
import numpy as np
import rospy
import time
from std_msgs.msg import String
from sensor_msgs.msg import JointState
from dynamixel_workbench_msgs.srv import DynamixelCommand
from trajectory_msgs.msg import JointTrajectory, JointTrajectoryPoint

def joint_publisher():
    pub = rospy.Publisher('/joint_trajectory', JointTrajectory, queue_size=0)
    rospy.init_node('joint_publisher', anonymous=False)
    

Home=[0, 0, 0, 0, 0]
Pos1=[25, 25, 20, -20, 0]
Pos2=[-35,35, -30, 30, 0]
Pos3=[85, -20, 55, 25, 0]
Pos4=[80, -35, 55, -45, 0]

def go_trajectory(pos):
    state = JointTrajectory()
    state.header.stamp = rospy.Time.now()
    state.joint_names = ["joint_1", "joint_2", "joint_3", "joint_4", "joint_5"]
    point = JointTrajectoryPoint()
    point.positions = pos 
    point.time_from_start = rospy.Duration(1)
    state.points.append(point)
    pub.publish(state)
    print('Posicion enviada')
    print(pos)
    rospy.sleep(5)

while not rospy.is_shutdown():
    go_trajectory(Home)
    go_trajectory(Pos1)
    go_trajectory(Pos2)
    go_trajectory(Pos3)
    go_trajectory(Pos4)

if __name__ == '__main__':
    try:
        joint_publisher()
    except rospy.ROSInterruptException:
        pass
´´´
## Toolbox
## Matlab + ROS + Toolbox:
Se buscan las poses mediante MATLAB de la siguiente tabla
 |    q1   |   q2   |   q3   |   q4   |   q5   |
| ------- | ------ | ------ | ------ | ------ |
|   1    |    0   |    0   |    0   |    0   |
|   2    |   25   |   25   |   20   |  -20   |
|   3    |  -35   |   35   |  -30   |   30   |
|   4    |   85   |  -20   |   55   |   25   |
|   5    |   80   |  -35   |   55   |  -45   |

