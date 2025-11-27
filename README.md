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
---

# 2. Comprobar funcionamiento del contenedor:

Una vez crear el contenedor, vamos a mirar si funciona entrando a nuestro localhost:

<img width="1920" height="1039" alt="image" src="https://github.com/user-attachments/assets/418cdf37-bfc1-4bc4-86b1-91def5ecbc31">

La página nos sale así porque, al principio, habíamos puesto este comando:

```
git clone https://github.com/cloudacademy/static-website-example .
```

Por ende, nos sale eso por defecto.
