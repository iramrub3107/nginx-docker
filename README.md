# nginx-docker
Nginx I: Instalación y configuración de servidor web en DOCKER | Hecho por Izan Ramos Rubio


# 1. Crear archivo de configuración del contenedor:

Como esto lo estoy haciendo desde Windows, he tenido que cambiar un poco el comando que crea el contenedor para que se pueda ejecutar correctamente:

```
docker run -d --name nginx-example -p 80:80 ^
  -v C:/Users/2DAW-A/nginx/izan.test/html:/usr/share/nginx/html ^
  -v C:/Users/2DAW-A/nginx/izan.test/conf/nginx.conf:/etc/nginx/conf.d/default.conf ^
  nginx:latest
```
