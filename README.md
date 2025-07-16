# TFG
Trabajo Fin de Grado Miguel Sánchez-Beato
# TFG: Plataforma de Autoevaluación para Bases de Datos con IA 🧠

Este proyecto es una aplicación web diseñada para ayudar a los estudiantes de la asignatura "Sistemas de Bases de Datos" a autoevaluarse. La plataforma utiliza un modelo de lenguaje grande (LLM), Llama 3, para generar automáticamente preguntas de tipo test, ofreciendo una herramienta de estudio interactiva y personalizada.

## Características Principales

* **Dashboard de Progreso**: Visualiza tu avance general, el progreso por objetivos de aprendizaje y el total de preguntas respondidas, pendientes y falladas.
* **Evaluación por Objetivos**: La aplicación se estructura en torno a los objetivos de aprendizaje de la asignatura.
* **Generación de Preguntas a Demanda**: ¿Necesitas más práctica? Solicita nuevas preguntas para criterios de aceptación específicos y el modelo las generará para ti.
* **Feedback Instantáneo**: Al responder una pregunta, verás inmediatamente si tu respuesta es correcta (🟢) o incorrecta (🔴), junto con una explicación detallada.
* **Historial de Intentos**: Todos tus intentos se guardan, permitiéndote reintentar las preguntas falladas y seguir tu evolución.
* **Notificaciones Intuitivas**: El sistema te informa sobre el estado de las operaciones (éxito, en proceso, error) mediante un código de colores.

---

## Guía de Instalación y Puesta en Marcha

Sigue estos pasos para poner en marcha el proyecto en tu entorno local.

### 1. Requisitos Previos

Asegúrate de tener instalado lo siguiente:

* **Docker Desktop** (v20.10 o superior).
* **Node.js** (v18.0 o superior).
* **npm** (se instala con Node.js).
* Mínimo **8 GB de RAM** disponibles.
* Procesador Intel i7 de 7ª generación o similar.
* Conexión a Internet.

### 2. Clonar el Repositorio

Abre tu terminal y clona el proyecto desde GitHub:

```bash
git clone [https://github.com/Miguelsbdh/TFG.git](https://github.com/Miguelsbdh/TFG.git)
cd TFG
```

La estructura del proyecto será:

cliente/
servidor/
README.md
tfg.sql

### 3. Configurar la Base de Datos 🗄️
Se recomienda usar XAMPP para gestionar la base de datos MySQL.

1. Inicia los módulos de Apache y MySQL en el panel de control de XAMPP.

2. Accede a tu gestor de base de datos (p. ej., phpMyAdmin) y ejecuta la siguiente consulta SQL para crear el usuario y darle permisos:

-- Crea el usuario para conexiones locales y desde Docker
CREATE USER 'tfg'@'localhost' IDENTIFIED BY 'tfg';
CREATE USER 'tfg'@'%' IDENTIFIED BY 'tfg';
GRANT ALL PRIVILEGES ON tfg.* TO 'tfg'@'localhost';
GRANT ALL PRIVILEGES ON tfg.* TO 'tfg'@'%';
FLUSH PRIVILEGES;

3. Crea la base de datos:
CREATE DATABASE tfg;

4. Selecciona la base de datos tfg y utiliza la función de importación para cargar el archivo tfg.sql que se encuentra en la raíz del proyecto.

### 4. Instalar Dependencias
Abre dos terminales en la raíz del proyecto (una para el backend y otra para el frontend).

Terminal Backend:
cd servidor
npm install

Terminal Frontend:
cd cliente
npm install

### 5. Ejecutar el Modelo LLM (Llama 3) con Docker 🐳
Descarga el modelo llama-3-finetuned-bases-de-datos-unsloth.Q5_K_M.gguf desde Hugging Face.

Guarda el archivo en una carpeta de tu elección (p. ej., C:/llama.cpp/models).

Ejecuta el siguiente comando en tu terminal, asegurándote de que Docker Desktop está abierto.

Bash

docker run --rm -it -p 8000:8000 \
-v /c/llama.cpp/models:/models \
-e MODEL=/models/llama-3-finetuned-bases-de-datos-unsloth.Q5_K_M.gguf \
ghcr.io/abetlen/llama-cpp-python:v0.3.1
Importante: Modifica la ruta -v /c/llama.cpp/models para que apunte a la carpeta donde guardaste el modelo .gguf.

### 6. Iniciar el Backend
En la terminal del backend (/servidor), ejecuta:

Bash

npm start
El servidor se iniciará y quedará escuchando en el puerto 9001.

### 7. Iniciar el Frontend
En la terminal del frontend (/cliente), ejecuta:

Bash

npm run dev
La aplicación se abrirá automáticamente en tu navegador en http://localhost:9000.
