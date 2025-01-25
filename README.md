
# Ejercicio Pick and Place de JdeRobot en ROS2 y MoveIt2
ROS2 Humble con MoveIt2

- Brazo robótico: UR5
- Herramienta terminal: pinza Robotiq 5
- Docker debe estar instalado en tu equipo (https://docs.docker.com/engine/install/ubuntu/)

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
3. La solución está actualmente en un archivo por lotes (sh) en el directorio root. Par ejecutarla:
  

