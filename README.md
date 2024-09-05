# README del Proyecto

## Descripción del Proyecto

Este proyecto es una aplicación de gestión de tareas que permite a los usuarios crear y administrar listas de tareas y realizar un seguimiento del progreso de cada tarea. La aplicación está diseñada para ser intuitiva y fácil de usar, brindando a los usuarios una manera eficaz de organizar sus actividades diarias.

## Desarrollado con

- ![MySQL](https://img.shields.io/badge/MySQL-000000?style=for-the-badge&logo=mysql&logoColor=white)
- ![phpMyAdmin](https://img.shields.io/badge/phpMyAdmin-000000?style=for-the-badge&logo=phpmyadmin&logoColor=white)
- ![draw.io](https://img.shields.io/badge/draw.io-000000?style=for-the-badge&logo=draw.io&logoColor=white)

## Características

- **Registro y Autenticación de Usuarios**: Los usuarios pueden registrarse, iniciar sesión y gestionar su perfil.
- **Gestión de Listas de Tareas**: Los usuarios pueden crear múltiples listas de tareas y asignarles nombres y descripciones.
- **Gestión de Tareas**: Dentro de cada lista, los usuarios pueden agregar tareas, asignarles prioridades, fechas de vencimiento y etiquetas.
- **Historial de Cambios**: La aplicación mantiene un historial detallado de todas las acciones realizadas en las tareas, incluyendo la creación, modificación, eliminación y marcado como completadas.

## Estructura de la Base de Datos

A continuación, se detalla el esquema de la base de datos, incluyendo las tablas y sus relaciones:

### Tablas

1. **Usuario**
   - `id_usuario` (INT, AUTO_INCREMENT, PRIMARY KEY): Identificador único del usuario.
   - `nombre` (VARCHAR(50), NOT NULL): Nombre del usuario.
   - `email` (VARCHAR(100), UNIQUE, NOT NULL): Dirección de correo electrónico del usuario.
   - `password` (VARCHAR(255), NOT NULL): Contraseña del usuario.
   - `fecha_creacion` (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP): Fecha y hora en que se creó el registro del usuario.

   ```sql
   CREATE TABLE Usuario (
       id_usuario INT AUTO_INCREMENT PRIMARY KEY,
       nombre VARCHAR(50) NOT NULL,
       email VARCHAR(100) UNIQUE NOT NULL,
       password VARCHAR(255) NOT NULL,
       fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
## **Tareas**

La tabla `Tareas` almacena la información relacionada con las tareas individuales dentro de una lista de tareas. A continuación se detallan los campos y su propósito:

- **id_tarea** (INT, AUTO_INCREMENT, PRIMARY KEY): Identificador único de la tarea.
- **descripcion_tarea** (TEXT, NOT NULL): Descripción detallada de la tarea.
- **id_lista** (INT): Referencia a la lista a la que pertenece la tarea.
- **fecha_creacion** (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP): Fecha y hora en que se creó la tarea.
- **fecha_vencimiento** (DATE): Fecha límite para completar la tarea.
- **prioridad** (ENUM('1', '2', '3'), NOT NULL): Prioridad de la tarea (1: baja, 2: media, 3: alta).
- **etiquetas** (VARCHAR(255)): Etiquetas asociadas a la tarea para facilitar la búsqueda y clasificación.
- **estado** (BOOLEAN, DEFAULT 0): Estado de la tarea (0: no completada, 1: completada).

```sql
CREATE TABLE Tareas (
    id_tarea INT AUTO_INCREMENT PRIMARY KEY,
    descripcion_tarea TEXT NOT NULL,
    id_lista INT,
    fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    fecha_vencimiento DATE,
    prioridad ENUM('1', '2', '3') NOT NULL, -- 1: baja, 2: media, 3: alta
    etiquetas VARCHAR(255),
    estado BOOLEAN DEFAULT 0, -- 0: no completada, 1: completada
    FOREIGN KEY (id_lista) REFERENCES Lista_Tareas(id_lista)
);

## Historial de Cambios

La tabla `Historial_Cambios` registra las acciones realizadas sobre las tareas, permitiendo un seguimiento detallado de las modificaciones. A continuación se detallan los campos y su propósito:

- **id_historial** (INT, AUTO_INCREMENT, PRIMARY KEY): Identificador único del historial.
- **id_tarea** (INT): Referencia a la tarea relacionada con la acción.
- **id_usuario** (INT): Referencia al usuario que realizó la acción.
- **accion_realizada** (ENUM('crear', 'modificar', 'eliminar', 'completar'), NOT NULL): Tipo de acción realizada sobre la tarea.
- **fecha_accion** (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP): Fecha y hora en que se realizó la acción.

```sql
CREATE TABLE Historial_Cambios (
    id_historial INT AUTO_INCREMENT PRIMARY KEY,
    id_tarea INT,
    id_usuario INT,
    accion_realizada ENUM('crear', 'modificar', 'eliminar', 'completar') NOT NULL,
    fecha_accion TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (id_tarea) REFERENCES Tareas(id_tarea),
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);
## Relaciones entre Tablas

El esquema de la base de datos está diseñado para reflejar las siguientes relaciones entre las tablas:

- **Usuario y Lista de Tareas**: 
  - **Relación**: Uno a Muchos
  - **Descripción**: Un usuario puede crear varias listas de tareas, pero cada lista de tareas pertenece a un solo usuario. Esto se implementa mediante la clave foránea `id_usuario_creador` en la tabla `Lista_Tareas`, que hace referencia a `id_usuario` en la tabla `Usuario`.

- **Lista de Tareas y Tareas**: 
  - **Relación**: Uno a Muchos
  - **Descripción**: Una lista de tareas puede contener varias tareas, pero cada tarea pertenece a una sola lista de tareas. Esto se implementa mediante la clave foránea `id_lista` en la tabla `Tareas`, que hace referencia a `id_lista` en la tabla `Lista_Tareas`.

- **Tareas y Historial de Cambios**: 
  - **Relación**: Uno a Muchos
  - **Descripción**: Cada tarea puede tener múltiples entradas en el historial de cambios, y cada entrada en el historial está asociada a una sola tarea. Esto se implementa mediante la clave foránea `id_tarea` en la tabla `Historial_Cambios`, que hace referencia a `id_tarea` en la tabla `Tareas`.

- **Usuario y Historial de Cambios**: 
  - **Relación**: Uno a Muchos
  - **Descripción**: Un usuario puede realizar múltiples acciones en las tareas, y cada entrada en el historial está asociada a un solo usuario. Esto se implementa mediante la clave foránea `id_usuario` en la tabla `Historial_Cambios`, que hace referencia a `id_usuario` en la tabla `Usuario`.



