# DulceriaWeb Python Flask

Este proyecto consiste en una aplicación web de **Dulcería** dividida en tres partes principales: un **backend** basado en Flask que gestiona la API y se comunica con la base de datos, un **frontend** que despliega los templates y consume la API, y una **base de datos PostgreSQL**. Todo el sistema está gestionado y orquestado utilizando **Docker** y **Docker Compose**.

A continuación se detallan los pasos necesarios para construir y desplegar la aplicación en un entorno Dockerizado utilizando Docker Swarm.

## Arquitectura del Proyecto

El proyecto está dividido en las siguientes partes:

1. **Backend (Flask API)**: La API de Flask se comunica con una base de datos PostgreSQL y maneja la lógica de negocio. Se encuentra en el directorio [backend](backend/).
2. **Frontend**: El frontend es responsable de mostrar los templates y consumir la API de Flask para interactuar con los datos. Se encuentra en el directorio [frontend](frontend/).
3. **Base de Datos (PostgreSQL)**: Se utiliza PostgreSQL como base de datos para almacenar los datos relacionados con las ventas y los productos de la dulcería. Los scripts de creación de tablas y datos iniciales se encuentran en el directorio [base_datos](base_datos/).

## Backend

El backend de la aplicación está basado en Flask, un microframework de Python. Se encarga de gestionar la lógica de negocio y la comunicación con la base de datos PostgreSQL. Algunas de las características principales del backend son:

- **API RESTful**: Proporciona endpoints para realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre los recursos de la aplicación, como usuarios, productos, categorías, carritos y órdenes.
- **Autenticación y Autorización**: Implementa mecanismos de autenticación y autorización para asegurar que solo los usuarios registrados puedan acceder a ciertas funcionalidades.
- **Gestión de Sesiones**: Utiliza sesiones para mantener el estado de autenticación de los usuarios.
- **Validación de Datos**: Valida los datos de entrada para asegurar que cumplen con los requisitos esperados antes de procesarlos.
- **Manejo de Errores**: Gestiona los errores de manera adecuada, proporcionando respuestas claras y útiles a los clientes de la API.

El archivo principal del backend es [backend/backend.py](backend/backend.py), y las dependencias necesarias están listadas en [backend/requirements.txt](backend/requirements.txt).

## Frontend

El frontend de la aplicación también está basado en Flask y utiliza Jinja2 para renderizar las páginas HTML. Algunas de las características principales del frontend son:

- **Templates Jinja2**: Utiliza templates de Jinja2 para generar dinámicamente las páginas HTML a partir de los datos proporcionados por el backend.
- **Interacción con la API**: Consume la API del backend para obtener y enviar datos, permitiendo a los usuarios interactuar con la aplicación de manera intuitiva.
- **Diseño Responsivo**: Utiliza CSS para asegurar que la aplicación se vea bien en diferentes dispositivos y tamaños de pantalla.
- **Gestión de Sesiones**: Mantiene el estado de autenticación de los usuarios y muestra contenido personalizado basado en su estado de sesión.
- **Manejo de Formularios**: Gestiona formularios para el registro, inicio de sesión, búsqueda de productos, y más.

El archivo principal del frontend es [frontend/front.py](frontend/front.py), y las dependencias necesarias están listadas en [frontend/requirements.txt](frontend/requirements.txt).

## Comandos para Docker Swarm

### **1. Construir las imágenes Docker para el backend, frontend y base de datos**
```bash
docker build -t backend ./backend
docker build -t frontend ./frontend
docker build -t basedatos ./base_datos
```

### **2. Inicializar Docker Swarm y despliege**:
```bash
docker swarm init
docker stack deploy --compose-file docker-compose.yml dulceria-stack
```

### **3. Escalar el servicio del backend**:
```bash
docker service scale dulceria-stack_flask-api=<Numero relicas>
```
