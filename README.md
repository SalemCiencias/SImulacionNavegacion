# Simulación Navegación
## Organización del repositorio
Este respositorio contiene 3 carpetas: 
- Blender Salon: Contiene los modelos de blender que fueron usados para crear el salon.
- modelos_gazebo: Contiene las formas .dae y .stl del salon, estas son usadas por gazebo como geometria y como collision respctivamente, para crear el salon. 
- Texturas: Contiene imagenes que fueron usadas como texturas para el salon, estas unicamente se llaman desde blender. 
## Instrucciones para correr el proyecto
Para poder correr el proyecto es necesario iniciar 
el mundo de gazebo, con la instrucción: 
```
ign gazebo Robotica.sdf
```
Y ádemas correr los puentes que convierten los topicos 
de ignition a topicos de ROS2, primero el comando para 
enviarle mensajes de movimiento a la Kobuki: 
```
ros2 run ros_gz_bridge parameter_bridge /commands/velocity@geometry_msgs/msg/Twist@ignition.msgs.Twist
```
Y tambiene el que convierte las lecturas del odometro: 
```
ros2 run ros_gz_bridge parameter_bridge /odom@nav_msgs/msg/Odometry@ignition.msgs.Odometry

```
## Breve explicación del sdf
Basicamente la simulación solo se compone de 3 modelos, el modelo del salon, en donde unicamente importamos los modelos generados con ayuda de Blender, exportados 
en .stl y en .dae
```
<model name="salon">
            <static>true</static>
            <link name="link">
                <collision name="collision">
                <geometry>
                    <mesh>
                        <uri>file://modelos_gazebo/salon.stl</uri>
                        <scale> 1 1 1 </scale>
                    </mesh>
                </geometry>
                </collision>
                 <visual name="visual">
                    <geometry>
                    <mesh>
                        <uri>file://modelos_gazebo/salon.dae</uri>
                        <scale> 1 1 1</scale>
                    </mesh>
                    </geometry>
                </visual>
            </link>
        </model>
...
</model>
```
El modelo del piso, para que tener una referencia sobre la altura en Z, a la que colocamos el piso del salon. 
```
<model name="ground_plane">
...
</model>
```
Y finalmente el modelo de la kobuki, si se quisiera usar la kobuki en otro entorno, unicamente habria que copiarla y pegarla en otro archivo cuidando que se tengan las carpetas de referencia que estan en modelos_gazebo. 
```
<model name="kobuki_standalone" canonical_link='base_link'>
...
</model>
```
