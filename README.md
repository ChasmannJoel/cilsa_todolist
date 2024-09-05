# README del Proyecto

## Descripción del Proyecto

Este proyecto es una aplicación de gestión de tareas que permite a los usuarios crear y administrar listas de tareas y realizar un seguimiento del progreso de cada tarea. La aplicación está diseñada para ser intuitiva y fácil de usar, brindando a los usuarios una manera eficaz de organizar sus actividades diarias.

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
