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

- `gateway`: host `80`
- `bff`: interno `8080`
- `usuarios-service`: interno `8081`
- `productos-service`: interno `8082`

## Levantar todo

Desde este repo:

```bash
docker compose up --build
```

## Endpoints

- `GET http://localhost/health`
- `GET http://localhost/api/usuarios`
- `GET http://localhost/api/usuarios/1`
- `GET http://localhost/api/productos`
- `GET http://localhost/api/overview`

Nginx preserva el prefijo `/api/` y resuelve el servicio `bff` por DNS interno de Docker para tolerar recreaciones de contenedores.
