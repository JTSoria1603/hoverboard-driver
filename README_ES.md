
# Hoverboard Driver

Este archivo describe las funciones principales, configuraciones y elementos añadidos al paquete `hoverboard-driver`.

---

## **1. Archivos de Lanzamiento (`launch`)**

Se han añadido los siguientes archivos de lanzamiento:

### **`map.launch`**
Este archivo ejecuta el nodo de Hector Mapping para generar mapas en tiempo real utilizando datos del LiDAR y la odometría del robot. También incluye la configuración para abrir automáticamente RViz con los temas relevantes.

- **Componentes que lanza:**
  - **Hector Mapping:** Nodo de SLAM para generar mapas.
  - **RViz:** Herramienta de visualización para ver el mapa y los datos del LiDAR.
  - **Transformaciones:** Publicadores estáticos para conectar `base_link` con el LiDAR.

- **Instrucciones de Uso:**
  Ejecuta el archivo con el siguiente comando:
  ```bash
  roslaunch hoverboard_driver map.launch
  ```

  Esto abrirá Hector Mapping y RViz automáticamente.

---

## **2. Librerías necesarias**

Para utilizar este paquete, asegúrate de que las siguientes librerías y dependencias estén instaladas:

### **Dependencias de ROS**
- `hector_mapping`: Instalación:
  ```bash
  sudo apt-get install ros-noetic-hector-mapping
  ```
- `rviz`: Instalación:
  ```bash
  sudo apt-get install ros-noetic-rviz
  ```
- `joint_state_controller`: Instalación:
  ```bash
  sudo apt-get install ros-noetic-joint-state-controller
  ```
- `diff_drive_controller`: Instalación:
  ```bash
  sudo apt-get install ros-noetic-diff-drive-controller
  ```
- `robot_state_publisher`: Instalación:
  ```bash
  sudo apt-get install ros-noetic-robot-state-publisher
  ```

### **Dependencias adicionales**
- `xacro`: Instalación:
  ```bash
  sudo apt-get install ros-noetic-xacro
  ```

---

## **3. Modelo Xacro**

El modelo Xacro define la estructura física del robot, incluyendo:
- Chasis.
- Ruedas motrices (`left_wheel` y `right_wheel`).
- LiDAR (`laser`).

![Modelo Xacro](modelo_xacro.jpg)


### **Ubicación del archivo:**
El archivo del modelo Xacro se encuentra en:
```bash
hoverboard_driver/xacro/robot.urdf.xacro
```

### **Secciones principales del modelo:**

1. **Chasis (`base_link`):**
   - Define la base principal del robot.
   - Incluye las dimensiones y el material visual.

2. **Ruedas motrices (`left_wheel` y `right_wheel`):**
   - Son esenciales para la odometría y el control diferencial.
   - Configuradas como joints tipo `continuous` para movimiento rotacional continuo.

3. **LiDAR (`laser`):**
   - Se ubica en el marco `base_link` mediante un joint fijo.
   - Publica datos en el topic `/scan`.

### **Visualización en RViz:**
Puedes visualizar el modelo físico utilizando RViz. Lanza el siguiente comando para cargar solo el modelo:
```bash
roslaunch hoverboard_driver robot.launch
```

---

## **4. Notas adicionales**

- Este proyecto fue extendido para incluir la funcionalidad de mapeo con Hector Mapping.
- RViz se configura automáticamente al ejecutar el archivo `map.launch`.
- Asegúrate de verificar las transformaciones del robot utilizando `rqt_tf_tree`:
  ```bash
  rosrun rqt_tf_tree rqt_tf_tree
  ```

Si encuentras problemas o necesitas ayuda adicional, no dudes en preguntar. 😊
