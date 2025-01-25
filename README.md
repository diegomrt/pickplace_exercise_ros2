
# Ejercicio Pick and Place en ROS2 y MoveIt2 en Docker
Requisitos: docker debe estar instalado en tu equipo Ubuntu (https://docs.docker.com/engine/install/ubuntu/)
- Plataforma: ROS2 Humble con MoveIt2
- Brazo robótico: UR5
- Herramienta terminal: pinza Robotiq 85
- Mundo de Gazebo Classic: JdeRobot Robotics Academy (http://jderobot.github.io/RoboticsAcademy/exercises/IndustrialRobots/pick_place)

![](media/video_pickplace_final_13.01.25_v1.1.webm)

## Pasos para la ejecución del ejercicio en host Ubuntu (con gráfica Nvidia)
### Lanzamiento del ejercicio:
1. Abre una terminal y ejecuta `xhost +` para permitir que el contenedor Docker cree ventanas en tu máquina host.
2. Crea y ejecuta el contenedor, que llamaremos "ejercicio_pickplace":
- `docker run -it --device /dev/dri --gpus all -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/.Xauthority:/root/.Xauthority -e XAUTHORITY=/root/.Xauthority --name ejercicio_pickplace diegomrt/pickplace_exercise_ros2:1.0` 
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

## EJEMPLO ADICIONAL: robot UR5 sobre eje lineal de 2m
### Lanzamiento del ejemplo:
1. Abre una terminal y ejecuta `xhost +` para permitir que el contenedor Docker cree ventanas en tu máquina host.
2. Crea y ejecuta el contenedor, que llamaremos "eje_lineal":
- `docker run -it --device /dev/dri --gpus all -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/.Xauthority:/root/.Xauthority -e XAUTHORITY=/root/.Xauthority --name eje_lineal diegomrt/pickplace_exercise_ros2:1.0` 
3. Dentro del contenedor iniciado, lanza el ejercicio. Si todo va bien, aparecerá una ventana con la simulación en gazebo Classic y otra ventana con Rviz2 incluyendo el plugin de MoveIt2:
- `ros2 launch ros2srrc_launch moveit2.launch.py package:=ros2srrc_ur5 config:=ur5_4`
 
### Ejecución de la solución
1. Abre otra terminal y conéctala al contenedor Docker lanzado:
- `docker exec -i eje_lineal bash` 
2. Para que desde esta terminal se reconozcan los comandos de ROS2 y la ruta del ejercicio, ejecuta el entrypoint:
- `source ros_entrypoint.sh`
3. Despliega en Gazebo un objeto amarillo con:
- `sh /root/spawn_yamaha_yellowbox.sh`
4. La solución del ejercicio se compone actualmente de diferentes partes, que están actualmente en un archivo por lotes (sh) en el directorio root. Par ejecutarla:
- `sh /root/demo_yamaha_ros2_ur5.sh`
_Nota: pendiente reconstrucción del mundo (se cargan por defecto los objetos del ejercicio de pick and place, que se pueden eliminar uno por uno en Gazebo)_
  
## Agradecimientos
Estos ejercicios hacen uso de los excelentes repositorios del grupo IFRA Cranfield:
- IFRA-Cranfield (2023) ROS 2 Sim-to-Real Robot Control. URL: https://github.com/IFRA-Cranfield/ros2_SimRealRobotControl. 
