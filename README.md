
# Ejercicio Pick and Place en ROS2 y MoveIt2 en Docker

![Ejercicio pick and place en ROS2](media/pickplace_exercise.png)

Requisitos: docker debe estar instalado en tu equipo Ubuntu (https://docs.docker.com/engine/install/ubuntu/)
- Plataforma: ROS2 Humble con MoveIt2
- Brazo robótico: UR5
- Herramienta terminal: pinza Robotiq 85
- Mundo de Gazebo Classic: JdeRobot Robotics Academy (http://jderobot.github.io/RoboticsAcademy/exercises/IndustrialRobots/pick_place)

La imagen Docker se encuentra en https://hub.docker.com/repository/docker/diegomrt/pickplace_exercise_ros2

## Pasos para la ejecución del ejercicio en host Ubuntu (con gráfica Nvidia)
### Lanzamiento del ejercicio:
1. Abre una terminal y ejecuta `xhost +` para permitir que el contenedor Docker cree ventanas en tu máquina host.
2. Crea y ejecuta el contenedor, que llamaremos "ejercicio_pickplace":
- `docker run -it --device /dev/dri --gpus all -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/.Xauthority:/root/.Xauthority -e XAUTHORITY=/root/.Xauthority --name ejercicio_pickplace diegomrt/pickplace_exercise_ros2:1.1` 
3. Dentro del contenedor iniciado, lanza el ejercicio. Si todo va bien, aparecerá una ventana con la simulación en gazebo Classic y otra ventana con Rviz2 incluyendo el plugin de MoveIt2:
- `ros2 launch ros2srrc_launch moveit2.launch.py package:=ros2srrc_ur5 config:=ur5_2`
4. Prueba a mover el robot y/o la herramienta desde el plugin de MoveIt2
 
### Ejecución de la solución
1. Abre otra terminal y conéctala al contenedor Docker lanzado
- `docker exec -i ejercicio_pickplace bash` 
2. Para que desde esta terminal se reconozcan los comandos de ROS2 y la ruta del ejercicio, ejecuta el entrypoint:
- `source ros_entrypoint.sh`
3. Despliega en Gazebo los cuatro objetos sobre la mesa con:
- `sh /root/spawn_objects_small.sh`
4. La solución del ejercicio se compone actualmente de diferentes partes, que están actualmente en un archivo por lotes (sh) en el directorio root. Par ejecutarla:
- `sh /root/demo_grasp_ros2_ur5.sh`
 
## Agradecimientos
Estos ejercicios hacen uso de los excelentes repositorios del grupo IFRA Cranfield:
- IFRA-Cranfield (2023) ROS 2 Sim-to-Real Robot Control. URL: https://github.com/IFRA-Cranfield/ros2_SimRealRobotControl. 
