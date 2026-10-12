# TP3 - TODO API con Docker y PostgreSQL

**Materia:** Programación Avanzada  
**Estudiante:** Jenaro Galdini  
**Tecnologías:** Node.js, Express, PostgreSQL, Docker Compose  

## Descripción

API REST para la gestión de tareas (TODO list) conectada a una base de datos PostgreSQL persistente, contenerizada y orquestada completamente mediante Docker Compose.

Implementa operaciones CRUD completas, validación de estados y soporte para paginación.

## Estructura del Proyecto

```text
TP3/
├── db/
│   └── init.sql         # Script SQL de inicialización (crea tabla y datos iniciales)
├── db.js                # Conexión y Pool hacia PostgreSQL
├── server.js            # Servidor Express y controladores de rutas
├── Dockerfile           # Configuración de imagen multi-stage para Node.js
├── docker-compose.yml   # Orquestación de servicios: api y db
├── .env                 # Variables de entorno locales
├── .env.example         # Ejemplo de variables de entorno
├── .dockerignore
└── package.json         # Dependencias y scripts
```

## Requisitos previos

- [Docker](https://www.docker.com/) y Docker Compose instalados.

## Cómo ejecutar

1. Configurar variables de entorno (si no existe `.env`):
   ```bash
   cp .env.example .env
   ```

2. Levantar los contenedores con Docker Compose:
   ```bash
   docker compose up --build
   ```

3. La API estará disponible en: `http://localhost:3001/tasks`  
   PostgreSQL estará accesible en el puerto `5432`.

4. Para detener los contenedores:
   ```bash
   docker compose down
   ```
   *(Para borrar también los datos del volumen persistente: `docker compose down -v`)*

## Endpoints de la API

| Método | Endpoint | Descripción | Parámetros / Body |
|---|---|---|---|
| `GET` | `/tasks` | Listar tareas (soporta filtro por status y paginación) | Query params: `?status=pending&limit=10&offset=0` |
| `GET` | `/tasks/:id` | Obtener una tarea por su ID | `id` en URL |
| `POST` | `/tasks` | Crear una nueva tarea | JSON: `{"title": "...", "description": "...", "status": "pending", "dueDate": "YYYY-MM-DD"}` |
| `PUT` | `/tasks/:id` | Actualizar una tarea existente | JSON: `{"title": "...", "status": "completed", ...}` |
| `DELETE` | `/tasks/:id` | Eliminar una tarea por ID | `id` en URL |
