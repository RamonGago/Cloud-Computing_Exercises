# Ejercicios de Introducción a la virtualización ligera: Contenedores
======================================================================

Para la realización de los ejercicios se ha utilizado una máquina virtual a través de la plataforma de **[Azure]**(https://azure.microsoft.com/es-es/) provisionada a través de la herramienta **[Ansible]**(https://www.ansible.com/).

# Ejercicio 1º
## Instala LXC en tu versión de Linux favorita. Normalmente la versión en desarrollo, disponible tanto en GitHub como en el sitio web está bastante más avanzada; para evitar problemas sobre todo con las herramientas que vamos a ver más adelante, conviene que te instales la última versión y si es posible una igual o mayor a la 2.0.

Para comenzar con el manejo de [lxc](https://linuxcontainers.org/) se ha procedido a su instalación en la máquina virtual destinada a la realización de los ejercicios.

![alt text](/images/tema5/Ejercicio1.png "Ejercicio 1")

# Ejercicio 2º
## Instalar una distro tal como Alpine y conectarse a ella usando el nombre de usuario y clave que indicará en su creación.

Tras la creación del contenedor a través del comando `sudo lxc-create -t alpine -n ejercicio2` y una vez iniciado el mismo con `sudo lxc-start -n ejercicio2` se puede observar su correcto funcionamiento:

![alt text](/images/tema5/Ejercicio2.png "Ejercicio 2")

![alt text](/images/tema5/Ejercicio2_2.png "Ejercicio 2_2")

# Ejercicio 3º
## Provisionar un contenedor LXC usando Ansible o alguna otra herramienta de configuración que ya se haya usado.

Para provisionar el contenedor LXC creado en el ejercicio anterior se ha pretendido utilizar Ansible.
Tras su instalación en la máquina virtual host para proceder al provisionamiento, se ha obtenido un error debido a la incapacidad de establecer una conexión por ssh con el contenedor LXC.
Por ello el resultado obtenido ha sido el siguiente:

![alt text](/images/tema5/Ejercicio3.png "Ejercicio 3")

# Ejercicio 4º
## Buscar alguna demo interesante de Docker y ejecutarla localmente, o en su defecto, ejecutar la imagen anterior y ver cómo funciona y los procesos que se llevan a cabo la primera vez que se ejecuta y las siguientes ocasiones.

Se ha tomado como imagen del docker la proporcionada en los apuntes de la materia. Tras su ejecución a través del comando `sudo docker run --rm jjmerelo/docker-daleksay -f smiling-octopus Uso argumentos, ea`se ha obtenido como primera ejecución el siguiente resultado:

![alt text](/images/tema5/Ejercicio4.png "Ejercicio 4")

Y tras proceder con una segunda ejecución para ver los nuevos resultados, se ha comprobado que una vez instalada la imagen (que no existía de forma local) directamente muestra la ejecución del docker accediendo a su imagen ya descargada, sin tener que realizarlo una segunda vez:

![alt text](/images/tema5/Ejercicio4_2.png "Ejercicio 4_2")

# Ejercicio 5º
## Comparar el tamaño de las imágenes de diferentes sistemas operativos base, Fedora, CentOS y Alpine, por ejemplo.

Para comparar el tamaño de las imágenes se ha procedido a la descarga y comprobación del tamaño de varias imágenes como se puede comprobar a continuación:

![alt text](/images/tema5/Ejercicio5.png "Ejercicio 5)

# Ejercicio 6º
## Comparar el tamaño de las imágenes de diferentes sistemas operativos base, Fedora, CentOS y Alpine, por ejemplo.

Utilizando el [contenedor de Fedora](https://hub.docker.com/_/fedora/) creado en el ejercicio anterior se ha utilizado el comando `sudo docker ps -a=false` para conseguir su ID.

A continuación para realizar un cambio a través de commit se utiliza el comando `sudo docker inspect <id obtenido>` con el ID obtenido y con el se obtendrá la información suficiente como para conseguir el ID completo mucho más largo.

Ya con este id podremos realizar cambios en la imagen y guardarlos con commit a través del comando `sudo docker commit <id imagen completo> <nombre-commit>`.

Para observar sus resultados basta con ejecutar `sudo docker images`:

![alt text](/images/tema5/Ejercicio6.png "Ejercicio 6)


# Ejercicio 7º
## Examinar la estructura de capas que se forma al crear imágenes nuevas a partir de contenedores que se hayan estado ejecutando.

Una vez realizado el commit del ejercicio anterior, se devolverá automaticamente una clave sha256. Para obtener la estructura de capas que se forman con las nuevas imagenes se utiliza el comando `sudo jq '.' /var/lib/docker/image/aufs/imagedb/content/sha256/<clave sha256>`.

Para poder ejecutarse dicho comando, previamente ha tenido que instalarse `jq` en la máquina para poder ver el JSON formateado.

Por otro lado, en el caso concreto de esta máquina, no existe el directo /aufs, sino el /overlay2. Esta diferencia se presupone que puede ser por el uso de la versión [CE de Docker](https://www.docker.com/community-edition) (Community Edition). A continuación se muestran los resultados obtenidos del JSON:

![alt text](/images/tema5/Ejercicio7.png "Ejercicio 7")

![alt text](/images/tema5/Ejercicio7_2.png "Ejercicio 7_2")

# Ejercicio 8º
## Crear un volumen y usarlo, por ejemplo, para escribir la salida de un programa determinado.

Para utilizar un volumen en docker, primeramente ha de crearse a través del siguiente comando `sudo docker volume create <nombre volumen>`, tras su creación se realiza un pull de la imagen a utilzar `sudo docker pull fedora` y por último se crea un microservicio que devuelva por ejemplo el número de ficheros `sudo docker run -it --rm -v benchmark:/app fedora /bin/bash` y dentro del bash `ls -R / | wc`. Con ello se consigue ejecutar un microprograma de tal forma que este puede ser ejecutado independientemente en el SO que se prefiera, tal y como se muestra en la imagen:

![alt text](/images/tema5/Ejercicio8.png "Ejercicio 8)

# Ejercicio 9º
## Usar un miniframework REST para crear un servicio web y introducirlo en un contenedor, y componerlo con un cliente REST que sea el que finalmente se ejecuta y sirve como “frontend”.

En proceso.

# Ejercicio 10º
## Reproducir los contenedores creados anteriormente usando un Dockerfile.



# Ejercicio 11º
## Crear con docker-machine una máquina virtual local que permita desplegar contenedores y ejecutar en él contenedores creados con antelación.
