# appointments-api

API REST para gestión de turnos con usuarios y roles (ADMIN / USER), autenticación JWT y persistencia en PostgreSQL.

Descripción: API pensada para casos de uso empresariales reales, con control de roles, validaciones y una estructura modular.

## Características
- Autenticación con JWT
- Roles: `ADMIN` / `USER`
- CRUD de turnos (appointments)
- Persistencia en PostgreSQL (Sequelize u otro ORM)
- Validaciones y manejo centralizado de errores
- Estructura de proyecto modular (controllers, models, routes, services)

## Tech stack
- Node.js + Express
- PostgreSQL
- JWT
- ORM sugerido: Sequelize

## Requisitos
- Node.js >= 16
- npm o yarn
- PostgreSQL (local o via Docker)

## Instalación y ejecución (desarrollo)
1. Clonar el repositorio
```bash
git clone https://github.com/lucamarianoaguero/appointments-api.git
cd appointments-api
```
2. Instalar dependencias
```bash
npm install
```
3. Copiar variables de entorno
```bash
cp .env.example .env
# editar .env con tus valores (DB, JWT_SECRET, etc)
```
4. Inicializar la base de datos (migraciones / seeders)
```bash
# si usas Sequelize CLI:
npx sequelize db:migrate
npx sequelize db:seed:all
```
5. Ejecutar en modo desarrollo
```bash
npm run dev
```

## Variables de entorno (ejemplo)
En `.env.example` incluye al menos:
```
PORT=3000
DATABASE_URL=postgres://user:pass@localhost:5432/appointments_db
JWT_SECRET=tu_secreto_seguro
JWT_EXPIRES_IN=1h
NODE_ENV=development
```

## Scripts sugeridos en package.json
- `npm run dev` — ejecutar en modo desarrollo (nodemon)
- `npm run start` — ejecutar en producción
- `npm run migrate` — correr migraciones
- `npm run seed` — cargar datos de ejemplo
- `npm test` — ejecutar tests

## Endpoints principales (resumen)
- POST   /auth/login → login de usuarios
  - Request:
    ```json
    { "email": "user@example.com", "password": "secret" }
    ```
  - Response:
    ```json
    { "token": "eyJhbGciOiJI..." }
    ```
- POST   /users → crear usuario
- GET    /appointments → listar turnos (autenticado)
- POST   /appointments → crear turno (autenticado)
- PUT    /appointments/:id → actualizar turno (autenticado)
- DELETE /appointments/:id → eliminar turno (autenticado, rol ADMIN)

Ejemplo curl (login):
```bash
curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@example.com","password":"secret"}'
```

## Seguridad y buenas prácticas (recomendadas)
- Hashear contraseñas con `bcrypt` o similar
- JWT con expiración corta y rotación de tokens cuando aplique
- Validaciones de payload con `Joi` o `express-validator`
- Rate limiting (express-rate-limit) y protección contra bruteforce en endpoints de auth
- No exponer secretos en repositorio; usar variables de entorno y gestores de secretos en producción

## Docker (opcional)
Se recomienda añadir un `Dockerfile` y `docker-compose.yml` con servicio de Postgres para facilitar el entorno local y CI.

## Tests y CI
- Añadir tests unitarios/integración para auth y endpoints críticos
- Configurar GitHub Actions para ejecutar lint y tests en cada push/PR

## Contribuciones
- Añadir `CONTRIBUTING.md` con guía de estilo, pruebas y flujo de PRs
- Usar linters y hooks pre-commit (husky)

## Roadmap / mejoras
- Paginación y filtros en listados
- Notificaciones (email)
- Auditoría de cambios en turnos
- Gestión avanzada de roles y permisos

## License
MIT