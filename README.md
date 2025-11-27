# nginx-docker
Nginx I: Instalación y configuración de servidor web en DOCKER | Hecho por Izan Ramos Rubio

# 1. Comprobar que Docker está instalado en el PC:

Para ello, ejecutamos el siguiente comando en nuestra terminal:

```
docker --version
```
<img width="1919" height="1031" alt="image" src="https://github.com/user-attachments/assets/64a6e3a7-88ae-4ac1-9382-77eff09ea224" />

En mi caso, como se puede observar, ya tenía instalado de antes Docker.

# 2. Crear estructura de carpetas del sitio web:

Ejecutamos los comandos que se piden para crear las carpetas, y en HTML clonamos el siguiente repositorio de GitHub:

```
git clone https://github.com/cloudacademy/static-website-example .
```
Al ejecutar el git clone, podemos observar cómo se clona el repositorio a la carpeta indicada:
<img width="937" height="198" alt="image" src="https://github.com/user-attachments/assets/e339d79a-5ed4-459c-9f16-7f7e2ea9cb7c" />

Así nos quedaría la estructura de este proyecto:
<img width="294" height="247" alt="image" src="https://github.com/user-attachments/assets/6a085fd0-42c6-486a-b74c-b0eba068cdd0" />


# 3. Crear archivo de configuración del contenedor y el contenedor:
Para crear el archivo de configuración de Nginx, como esto lo estoy haciendo desde Windows, he buscado cómo crear archivos desde la terminal y he encontrado esto: 

```
type nul > nombre_archivo.txt
```

Por ende, para crear el archivo, pondremos:

```
type nul > nginx.conf
```
Y aquí tendríamos el archivo creado correctamente

<img width="1356" height="734" alt="image" src="https://github.com/user-attachments/assets/88b31a4a-76c3-4bc9-8ff2-54dc6deb7180" />

Para configurar el archivo que recién hemos creado, he tenido que cambiar un poco el comando que crea el contenedor para que se pueda ejecutar correctamente:
(pongo nombre-usuario para indicar que hay que poner el nombre de usuario, que en mi caso sería "Izan")

```
docker run -d --name nginx-example -p 80:80 ^
  -v C:/Users/nombre-usuario/nginx/izan.test/html:/usr/share/nginx/html ^
  -v C:/Users/nombre-usuario/nginx/izan.test/conf/nginx.conf:/etc/nginx/conf.d/default.conf ^
  nginx:latest
```

Antes de crearlo, me aseguro de tener abierto Docker Desktop, ya que en Windows es necesario tener abierto el programa para que se ejecute el comando correctamente.

---

# 4. Comprobar funcionamiento del contenedor:

Una vez crear el contenedor, vamos a mirar si funciona entrando a nuestro localhost:

<img width="1920" height="1039" alt="image" src="https://github.com/user-attachments/assets/418cdf37-bfc1-4bc4-86b1-91def5ecbc31">

La página nos sale así porque, al principio, habíamos puesto este comando:

```
git clone https://github.com/cloudacademy/static-website-example .
```

Por ende, nos sale eso por defecto.

# 5. Editar archivo hosts y usar servicio nip.io

Vamos a intentar asociar nuestra IP local (127.0.0.1) al nombre del dominio. Para ello, nos iremos a VSCode y editaremos nuestro archivo hosts desde ahí escribiendo lo que pone en la captura de (lo tengo en C:\Windows\System32\drivers\etc\hosts al ser de Windows)

<img width="1916" height="1032" alt="Captura de pantalla 2025-11-27 164420" src="https://github.com/user-attachments/assets/fa55845f-68c0-40dd-9f7f-491ca7fecc83" />

