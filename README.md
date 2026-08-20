# tpi-backend-gateway

Gateway Nginx para publicar el backend compartido del demo TPI.

## Layout esperado

Clonar los cuatro repositorios como hermanos dentro de `D:\Facultad\ejemplo-tpi-backend`:

```text
ejemplo-tpi-backend/
├── tpi-backend-gateway/
├── tpi-backend-bff/
├── tpi-backend-usuarios/
└── tpi-backend-productos/
```

## Servicios y puertos

- `gateway`: host `8081` -> contenedor `80`
- `bff`: interno `8080`
- `usuarios-service`: interno `8081`
- `productos-service`: interno `8082`

## Separacion con el gateway frontend

Este repo backend usa `http://localhost:8081` para no chocar con el repo frontend `tpi-multirepo-gateway`, que sigue usando `http://localhost:80`.

- Frontend gateway existente: `http://localhost`
- Backend gateway de este repo: `http://localhost:8081`

Si los frontends consumen el backend directamente, la base URL recomendada pasa a ser `http://localhost:8081/api`.

## Levantar todo

Desde este repo:

```bash
docker compose up --build
```

## Endpoints

- `GET http://localhost:8081/health`
- `GET http://localhost:8081/api/usuarios`
- `GET http://localhost:8081/api/usuarios/1`
- `GET http://localhost:8081/api/productos`
- `GET http://localhost:8081/api/overview`

Nginx preserva el prefijo `/api/` y resuelve el servicio `bff` por DNS interno de Docker para tolerar recreaciones de contenedores.
