# TPI · Caso 1 · Shell SSR + bibliotecas

Gateway Nginx para el caso de una sola aplicación SSR: el Shell renderiza en el servidor y carga bibliotecas de funcionalidad publicadas. El navegador conoce un único origen: este gateway.

## Layout esperado

Clonar los cuatro repositorios como hermanos dentro de `D:\Facultad\ejemplo-tpi-backend`:

```text
ejemplo-tpi-backend/
├── tpi-backend-gateway-main/
├── tpi-demo-shell-main/
├── tpi-backend-bff-main/
├── tpi-backend-usuarios-main/
└── tpi-backend-productos-main/
```

## Servicios y puertos

- `gateway`: host `8081` -> contenedor `80`; publica UI SSR y API
- `shell-ssr`: interno `4000`
- `bff`: interno `8080`
- `usuarios-service`: interno `8081`
- `productos-service`: interno `8082`

## Contrato público

- UI SSR: `http://localhost:8081/`
- BFF: solo `/api/v1/*`; no se publica CORS.
- Login: `POST /api/v1/auth/login`; logout: `POST /api/v1/auth/logout`.
- El gateway limita intentos de login, no reintenta escrituras y responde sin caché.
- `/internal` y `/actuator` se rechazan. Los microservicios solo se ven dentro de Docker.

## Levantar todo

Desde este repo:

```bash
export DEMO_LOGIN_EMAIL='docente@example.test'
# Export DEMO_LOGIN_PASSWORD, USERS_DB_PASSWORD and PRODUCTS_DB_PASSWORD from a local secret manager or the current shell.
docker compose up --build
```

## Endpoints

- `GET http://localhost:8081/health`
- `POST http://localhost:8081/api/v1/auth/login`
- `GET http://localhost:8081/api/v1/usuarios`
- `GET http://localhost:8081/api/v1/productos`
- `GET http://localhost:8081/api/v1/overview`
