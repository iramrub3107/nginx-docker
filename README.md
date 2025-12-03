# Nginx I: Instalación y configuración de servidor web en DOCKER | Hecho por Izan Ramos Rubio

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
<img width="694" height="647" alt="image" src="https://github.com/user-attachments/assets/6a085fd0-42c6-486a-b74c-b0eba068cdd0" />

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

Aquí, por ejemplo, vamos a cambiar el nombre del servidor y le vamos a poner "patata.test"

<img width="1199" height="792" alt="image" src="https://github.com/user-attachments/assets/032ef948-a313-40ee-9eb5-8a80f9e28993" />

Y una vez hechos los cambios, guardamos y nos vamos a la terminal a ejecutar ```docker restart nginx-example```

<img width="1106" height="622" alt="image" src="https://github.com/user-attachments/assets/af673fa6-9fe7-4ef0-a8f1-7ea22b5b2716" />

Por último, vamos a eliminar nuestro contenedor. Para ello: primero, lo vamos a parar:

<img width="1107" height="624" alt="image" src="https://github.com/user-attachments/assets/341adfb3-7a6b-4c07-b1b0-8be8c920a1e9" />

Y, a continuación, lo vamos a borrar escribiendo ```docker rm nginx-example```

<img width="1111" height="619" alt="image" src="https://github.com/user-attachments/assets/429389da-13ee-4717-aa1b-2eb5502ee710" />

También nos aseguraremos de que el contenedor se ha borrado mirándolo en el Docker Desktop

<img width="1442" height="709" alt="image" src="https://github.com/user-attachments/assets/aad8de6e-77ce-439d-9e41-74ca4e3c3e45" />

---

# 8. Uso de docker-compose

Hay una forma más rápida de hacer contenedores **usando docker-compose**. Para ello, vamos a crear un archivo docker-compose.yml en la carpeta "izan.test", y le adjuntaremos el siguiente contenido:

<img width="563" height="152" alt="image" src="https://github.com/user-attachments/assets/4d4441b1-b9f5-4e74-90de-04b311968908" />
<img width="1919" height="1030" alt="image" src="https://github.com/user-attachments/assets/a7062c32-f048-4a5f-95ef-5de624726055" />

Una vez lo tenemos, vamos a ver si funciona. Para ello, vamos a ejecutarlo escribiendo este comando:

```
docker-compose up -d
```

Y como podemos observar, el docker-compose se ha inicializado correctamente

<img width="1109" height="273" alt="image" src="https://github.com/user-attachments/assets/8eb12b09-8bed-4880-a829-61116f835996" />

Con el comando ```docker-compose logs -f``` podemos ver todos los logs de nuestro docker-compose, en donde sale la siguiente información:

<img width="1909" height="779" alt="image" src="https://github.com/user-attachments/assets/bbe7c6e9-9404-4950-9787-2aa051d5a7be" />

Y por último, con ```docker-compose down``` detenemos los contenedores:

<img width="1101" height="152" alt="image" src="https://github.com/user-attachments/assets/18979b2f-78eb-44f7-ad1c-0e75bc65d162" />

Y podemos observar que se ha detenido correctamente.

---

# Nginx II: Autenticación con Docker | Hecho por Izan Ramos Rubio

# 1.1: Paquetes necesarios

Para esta práctica necesitamos OpenSSL, por lo que nos lo instalaremos usando este comando en la terminal:

```
docker pull stakater/ssl-certs-generator
```
Lo ejecutamos en la terminal y nos esperamos a que se instale.

<img width="1112" height="619" alt="image" src="https://github.com/user-attachments/assets/087d7ed8-cfc1-4275-bb8a-5e709b12d282" />

---

# 1.2: Creación de usuarios y contraseñas para el acceso web:

Primero, vamos a hacer un archvo htpasswd, y después introduciremos "izan:" en él

<img width="1103" height="240" alt="image" src="https://github.com/user-attachments/assets/9b64921f-26db-4311-9374-a0295772f5cc" />
<img width="767" height="486" alt="image" src="https://github.com/user-attachments/assets/179c1e5f-34ff-48c2-a72e-10983a8379c8" />

He puesto "izan:" dentro del htpasswd porque, a continuación, toca crear un password cifrado para este usuario.
Para ello, ejecutaremos este comando en la terminal:

```
docker run --rm stakater/ssl-certs-generator openssl passwd -apr1 'tupassword' >> htpasswd
```

<img width="1111" height="95" alt="image" src="https://github.com/user-attachments/assets/d7892e61-2d1b-445f-b839-6e855a71a990" />

Verificamos que la contraseña encriptada se ha añadido correctamente a nuestro fichero...

<img width="771" height="492" alt="image" src="https://github.com/user-attachments/assets/c89dfe21-d22c-405e-857f-38cbf5f6faf3" />
<img width="771" height="532" alt="image" src="https://github.com/user-attachments/assets/b440f4a8-0790-402b-b34f-8578c16c78d4" />

...y efectivamente, se ha añadido correctamente la contraseña al fichero, sin dejar espacios ni cosas raras.

A continuación, vamos a repetir este mismo proceso, pero con otro usuario: ramos (mi primer apellido, como se indica en la práctica)

1. Añadimos el usuario

<img width="770" height="494" alt="image" src="https://github.com/user-attachments/assets/fe81f971-d8f1-4b7c-90e7-4018333ebf5d" />

2. Creamos la contraseña encriptada:

<img width="1108" height="616" alt="image" src="https://github.com/user-attachments/assets/8428694e-20f8-4433-ad80-43e50742f6a9" />

3. Nos aseguramos de que se la contraseña se ha añadido correctamente:

<img width="769" height="492" alt="image" src="https://github.com/user-attachments/assets/eea098aa-e1fb-4755-b5ae-eff0b9087dce" />

Y como se puede observar, la contraseña encriptada me la ha introducido, pero no correctamente. Para esto, hacemos que la contraseña esté en la misma línea que el usuario (sin espacios), y ya está. Es algo que nosotros mismos podemos arreglar sin problema.

<img width="768" height="490" alt="image" src="https://github.com/user-attachments/assets/a856b4cd-bec1-4869-ac13-a3a748607723" />

Hecho el nuevo usuario, solamente guardaremos el fichero y ya.

---

# 1.3: Configuración del contenedor Nginx para la autenticación básica:

Ahora editaremos el archivo de configuración de Nginx, el cual pondremos este comando en la terminal para crearlo: ```docker run --rm --entrypoint=cat nginx /etc/nginx/conf.d/default.conf > example.izan.conf```

Creamos el archivo y, a continuación, lo editamos.

<img width="1098" height="89" alt="image" src="https://github.com/user-attachments/assets/e2eddffe-082e-4895-bc8f-145664adba2a" />

<img width="770" height="536" alt="image" src="https://github.com/user-attachments/assets/acc3dcf6-093c-403e-ba4a-25fb3616ce90" />

Y, después, ejecutamos este comando (ha sido adaptado para poder usarse en la terminal de Windows, que es la que estoy usando):

```
docker run -d --name nginx-example ^
 -p 8080:80 ^
 -v "%cd%\conf:/etc/nginx/conf" ^
 -v "%cd%\html:/usr/share/nginx/html" ^
 nginx

```
<img width="643" height="152" alt="image" src="https://github.com/user-attachments/assets/ab917beb-a8e8-4ea5-85ed-190cf9117479" />

---

# 1.4: Probando la nueva configuración

En esta captura, como se puede observar, al entrar al servidor me dice que ha rechazado la conexión, por lo que, técnicamente, se podría decir que funciona.

<img width="1918" height="1035" alt="Captura de pantalla 2025-12-02 203802" src="https://github.com/user-attachments/assets/a5a53505-7453-4518-96f9-0385cbf70b20" />

---

# 2. y 3. TAREAS

#2.1: Intentos de login

Aquí se ven todos los logs que han habido en el contenedor:

<img width="1110" height="775" alt="image" src="https://github.com/user-attachments/assets/5ed1c4ea-4ee2-449a-bfdd-ec40fc3c8dc7" />

#2.2: Proteger solamente contact.html

Para ello, vamos a crear primero el archivo y le vamos a meter algo de contenido:

<img width="1917" height="1032" alt="image" src="https://github.com/user-attachments/assets/4c39ce1d-db66-42d4-9f3e-0d02b1d0f9b6" />

A continuación, vamos a editar un poco nuestro archivo de configuración para que se pueda acceder a contact.html exclusivamente con contraseña

<img width="1916" height="1007" alt="image" src="https://github.com/user-attachments/assets/c13e5fb3-abf5-4482-ab16-56e586bdd544" />

Reiniciamos el contenedor y comprobamos que funcione:

<img width="1108" height="256" alt="image" src="https://github.com/user-attachments/assets/63b3ac26-5bf4-44a8-b91b-5c227e916aa2" />

# 2.3: Combinación por IP y autenticación

Primero, vamos a cambiar un poco el archivo de configuración, y meteremos una location /api:

<img width="1256" height="941" alt="image" src="https://github.com/user-attachments/assets/bbea058b-6c55-491a-9656-ac79df7ebb2c" />

Dentro, podemos encontrar dos allows, que son básicamente los de nuestro PC, y un deny, que es para el resto. Juntando todo el código (como en la captura), podemos tener hecho este ejercicio.

# 3.1: Bloquear acceso por IP

Esto es tan sencillo como crear otra "ruta" en la cual bloqueemos el acceso a la carpeta raíz. Para ello, vamos a crear esta "ruta" y simplemente vamos a cambiar "allow" por "deny" en nuestra IP local, y al resto de IPs, le pondremos "allow":

<img width="1257" height="935" alt="image" src="https://github.com/user-attachments/assets/4576d2be-b7b8-4328-a98a-42d94ff2b61c" />

#3.2: IP válida y usuario también (al mismo tiempo)

Para esto, pondremos este código sobre la misma "ruta":

<img width="1260" height="939" alt="image" src="https://github.com/user-attachments/assets/77d96cd0-06d6-49e4-8c7f-aaac4144bc11" />

---

# Nginx III: Acceso seguro con Nginx Docker | Hecho por Izan Ramos Rubio

# 1. Configuración de Nginx:
# 1.1. Nombre del servidor:

Para ello, vamos a establecer una directiva server_name dentro de nuestro archivo de configuración:

<img width="1260" height="939" alt="image" src="https://github.com/user-attachments/assets/cf8d90ed-53e6-43ce-be61-64782fd12f0e" />

Lo subrayado ha sido lo único que he tenido que añadir al fichero para poder hacer este paso.

# 2. Generar un certificado autofirmado:

Para ello, primero, vamos a escribir en la terminal este comando:

```
docker pull stakater/ssl-certs-generator
```
Esto nos descargará el generador de certificados SSL.

<img width="1096" height="184" alt="image" src="https://github.com/user-attachments/assets/edb61802-52ee-4645-8f04-c88f060039d6" />

Y, a continuación, crearemos la clave y el certificado SSL con ```docker run -v .:/certs stakater/ssl-certs-generator```

<img width="1106" height="829" alt="image" src="https://github.com/user-attachments/assets/8692e07d-cf8a-4738-bd19-429dba7fea5d" />

# 3. Configuración:

Ahora que ya tenemos nuestro certificado SSL, vamos a introducírselo a nuestro archivo de configuración. Para ello, vamos a editar este archivo e introduciremos el siguiente código:
Hay que tener en cuenta que, como esto lo estoy haciendo desde Windows, he tenido que "adaptar" un poco el archivo de configuración para que todo pueda funcionar bien.

<img width="1257" height="936" alt="image" src="https://github.com/user-attachments/assets/8ff77171-3f9f-4fef-a564-c580ff77713d" />

# 3.1. Mapeo de puertos y montaje de volumen con los certificados

Finalmente, para hacer este mapeo, vamos a ejecutar el siguiente comando en la terminal:

```
docker run -d ^
  --name nginx-exampletest ^
  -p 80:80 -p 443:443 ^
  -v "C:\Users\Izan\nginx\izan.test\conf\izan.test.conf:/etc/nginx/conf.d/default.conf:ro" ^
  -v "C:\Users\Izan\nginx\izan.test\certs\izan.test.crt:/etc/ssl/certs/izan.test.crt:ro" ^
  -v "C:\Users\Izan\nginx\izan.test\certs\izan.test.key:/etc/ssl/private/izan.test.key:ro" ^
  -v "C:\Users\Izan\nginx\izan.test\html:/var/www/izan.test/html:ro" ^
  nginx:latest
```

El comando lo he tenido que adaptar un poco para que me funcionase correctamente y, como se puede observar, funciona

<img width="1093" height="203" alt="image" src="https://github.com/user-attachments/assets/a28aab1f-9aea-4cb9-9a51-f4267ccb3ef6" />


