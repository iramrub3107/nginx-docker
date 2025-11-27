# nginx-docker
Nginx I: Instalación y configuración de servidor web en DOCKER | Hecho por Izan Ramos Rubio

# 1. Comprobar que Docker está instalado en el PC:

Para ello, ejecutamos el siguiente comando en nuestra terminal:

```
docker --version
```
<img width="1919" height="1031" alt="image" src="https://github.com/user-attachments/assets/64a6e3a7-88ae-4ac1-9382-77eff09ea224" />

En mi caso, como se puede observar, ya tenía instalado de antes Docker.

---

# 2. Crear estructura de carpetas del sitio web:

Ejecutamos los comandos que se piden para crear las carpetas, y en HTML clonamos el siguiente repositorio de GitHub:

```
git clone https://github.com/cloudacademy/static-website-example .
```
Al ejecutar el git clone, podemos observar cómo se clona el repositorio a la carpeta indicada:
<img width="937" height="198" alt="image" src="https://github.com/user-attachments/assets/e339d79a-5ed4-459c-9f16-7f7e2ea9cb7c" />

Así nos quedaría la estructura de este proyecto:
<img width="294" height="247" alt="image" src="https://github.com/user-attachments/assets/6a085fd0-42c6-486a-b74c-b0eba068cdd0" />

---

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

---

# 5. Editar archivo hosts y usar servicio nip.io

Vamos a intentar asociar nuestra IP local (127.0.0.1) al nombre del dominio. Para ello, nos iremos a VSCode y editaremos nuestro archivo hosts desde ahí escribiendo lo que pone en la captura de (lo tengo en C:\Windows\System32\drivers\etc\hosts al ser de Windows)

<img width="1916" height="1032" alt="Captura de pantalla 2025-11-27 164420" src="https://github.com/user-attachments/assets/fa55845f-68c0-40dd-9f7f-491ca7fecc83" />

Comprobamos si funciona...

<img width="1916" height="1033" alt="image" src="https://github.com/user-attachments/assets/701da4db-ffce-4b84-815c-585a1fdc18c3" />

...y efectivamente, funciona.

También si ponemos esta URL:

http://127-0-0-1.izan.test.nip.io

nos sale nuestro mismo sitio web:

<img width="1920" height="1033" alt="image" src="https://github.com/user-attachments/assets/75db4608-36fe-4941-9f45-c73ae67251e6" />

---

# 6. Comprobar registros del servidor

Para ello, introducimos en nuestra terminal este comando:

```
docker logs -f nginx-example
```
Y aquí podemos observar todos nuestros logs una vez escrito el comando
<img width="1836" height="936" alt="image" src="https://github.com/user-attachments/assets/aacbfa93-b698-4677-89fb-6baa5f078981" />

---

# 7. Gestionamiento del contenedor

Una vez que tenemos nuestro contenedor en funcionamiento, hay varias cosas a saber para poder gestionar correctamente el contenedor.
Para ello, hay una serie de comandos:

```
1.- docker stop nginx-example
2.- docker restart nginx-example
```

Estos comandos nos ayudarán para los siguientes pasos.

Primero, vamos a parar y reiniciar el contenedor. Para pararlo, vamos a poner en la terminal ```docker stop nginx-example``` y se nos debería de parar correctamente:

<img width="1107" height="624" alt="image" src="https://github.com/user-attachments/assets/341adfb3-7a6b-4c07-b1b0-8be8c920a1e9" />

Al ejecutar el comando, sale el nombre del contenedor. Pero para realmente asegurarnos de que se ha parado, vamos a ir al Docker Desktop...

<img width="1271" height="716" alt="image" src="https://github.com/user-attachments/assets/98b88f63-eacc-4ee8-9db4-0e606c771756" />

...y podremos observar cómo se ha parado.

A continuación, vamos a reiniciar el contenedor. Para ello, lo inicializamos y escribimos ```docker restart nginx-example```, y se debería de reiniciar:

<img width="1106" height="622" alt="image" src="https://github.com/user-attachments/assets/af673fa6-9fe7-4ef0-a8f1-7ea22b5b2716" />

Y pasa lo mismo que con el docker stop; en la terminal nos pone el nombre del contenedor. Pero, si miramos en Docker Desktop, podemos observar lo siguiente:

<img width="1544" height="710" alt="image" src="https://github.com/user-attachments/assets/6486cad9-fc3b-40b8-b9c8-9d70d36e01a6" />

Efectivamente; se ha reiniciado. ¿Y cómo se puede observar? Mirando en donde pone "Last Started". Al poner "0 seconds ago", podemos ver que recién se ha iniciado el contenedor, y por ende, confirmamos que se ha reiniciado.

Ahora vamos a modificar el contenido del contenedor. Para ello, nos iremos al archivo de configuración (nginx.conf), y editaremos lo que sea.

<img width="1196" height="791" alt="image" src="https://github.com/user-attachments/assets/8b90efe8-07db-47c1-b711-c8ec41a2f842" />

Aquí, por ejemplo, vamos a cambiar el nombre del servidor y le vamos a poner 



