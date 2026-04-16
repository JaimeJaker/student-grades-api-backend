# 🏫 Students & Grades API REST

![Java](https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=java&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5.4-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?style=for-the-badge&logo=docker&logoColor=white)

API REST robusta desarrollada en **Java 17 / Spring Boot** para gestionar alumnos, materias y sus respectivas calificaciones (notas).
Desarrollada enfocándose fervientemente en **Clean Code**, uso profundo de **DTOs (Data Transfer Objects)**, Validación exhaustiva de peticiones y un Gestor Global de Excepciones para una experiencia unificada en el cliente.

---

## 🚀 Tecnologías Principales

- **Java 17** con **Spring Boot 3.5.4**
- **Spring Data JPA** para la capa de persistencia.
- **Validación** de entradas (`spring-boot-starter-validation`).
- **Lombok** para optimización y limpieza del código (getters, setters, constructores de uso general).
- **Docker & Docker Compose** para orquestación del servidor web y base de datos.
- **PostgreSQL 15** (Despliegue default vía Docker) y **H2 Database** (Memoria / Pruebas).

---

## ▶️ Guía de Ejecución Rápida

La aplicación está completamente contenedorizada, por lo cual solo necesitas **dos simples comandos** para ejecutar toda la infraestructura localmente:

### 1️⃣ Configurar variables de entorno
```bash
cp .env.example .env
```
*(Esto habilitará dinámicamente los parámetros de conexión hacia el servidor PostgreSQL en Docker)*.

### 2️⃣ Levantar los servicios y lanzar el servidor
```bash
docker compose up -d --build
```
¡Listo! La API estará expuesta y operativa en `http://localhost:8080`.

> [!TIP]
> Si deseas ejecutar el binario clásico de Maven sin Docker de forma nativa (y utilizando la base de datos de fallback H2 en memoria), puedes ejecutar directamente `./mvnw spring-boot:run`.

---

## 🗄️ Entregables y Datos de Prueba (Evaluación Técnica)

Se han preparado activos empaquetados pensando de la forma más cómoda para la revisión técnica:
1. **Archivo de Volcado (`.dump`)**: En la carpeta `database_backup/` se encuentra el archivo `backend.dump` ejecutado en Formato Custom (`-F c`). Este respaldo nativo de PostgreSQL almacena 10 Alumnos generados, 5 Materias y 50 interacciones de Nota listas para ser restauradas libremente por el evaluador usando la herramienta `pg_restore`.
2. **Puertos Desacoplados**: El archivo *docker-compose.yml* lee activamente los puertos y las credenciales desde `API_PORT` y `DB_PORT` del archivo  `.env` incluido.

---

## 📡 API Endpoints

Las rutas exponen de forma clara sus recursos mediante el manejo adecuado del paradigma REST. La API consume y produce datos estrictamente en formato `application/json` con una estricta protección de Excepciones Globales de la forma 400 (*Bad Request*) y 404 (*Resource Not Found*).

### 👨‍🎓 Alumnos (`/alumnos`)
| Método | Endpoint | Acción |
|--------|----------|--------|
| `GET` | `/alumnos` | Listar todos los alumnos registrados |
| `POST` | `/alumnos` | Crear un nuevo alumno |
| `GET` | `/alumnos/{id}` | Consultar alumno específico por ID |
| `PUT` | `/alumnos/{id}` | Modificar datos integrales de un alumno existente |
| `DELETE` | `/alumnos/{id}`| Eliminar alumno permanentemente |

### 📚 Materias (`/materias`)
| Método | Endpoint | Acción |
|--------|----------|--------|
| `GET` | `/materias` | Obtener listado de todas las materias ofrecidas |
| `POST` | `/materias` | Insertar una nueva materia académica |
| `GET` | `/materias/{id}` | Consultar materia específica por su ID |
| `PUT` | `/materias/{id}` | Editar detalles y cantidad de créditos de una materia |
| `DELETE` | `/materias/{id}`| Eliminar materia globalmente |

### 📝 Notas y Calificaciones (`/notas`)
| Método | Endpoint | Acción |
|--------|----------|--------|
| `GET` | `/notas` | Listar el registro histórico total de calificaciones |
| `POST` | `/notas` | Registrar una calificación atando un `.alumnoId` a una `.materiaId` |
| `GET` | `/notas/alumno/{id}` | Ver reporte individual de notas del estudiante por Materia |

---

## 🧪 Estructura de un Payload Típico

### Crear una Nota

**Request** `POST /notas`
```json
{
  "valor": 4.5,
  "alumnoId": 1,
  "materiaId": 1
}
```

---

## 👨‍💻 Autor

Jaime Darley Angulo Tenorio
