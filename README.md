# appointments-api

REST API para gestión de turnos con usuarios y roles, pensada para casos de uso empresariales reales.

## Features
- Autenticación de usuarios (JWT)
- Roles: ADMIN / USER
- CRUD de turnos (crear, leer, actualizar, eliminar)
- Persistencia en base de datos relacional
- Validaciones y manejo de errores

## Tech Stack
- Node.js + Express
- PostgreSQL
- JWT
- ORM: Sequelize (opcional según stack)

## API Endpoints (ejemplo)
- POST   /auth/login → login de usuarios
- POST   /users → crear usuario
- GET    /appointments → listar turnos
- POST   /appointments → crear turno
- PUT    /appointments/:id → actualizar turno
- DELETE /appointments/:id → eliminar turno

## Cómo correr el proyecto
1. Clonar el repositorio
```bash
git clone https://github.com/tuusuario/appointments-api.git

npm install
npm run dev


