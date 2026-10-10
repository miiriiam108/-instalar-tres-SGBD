# -instalar-tres-SGBD

##  Desplegar Oracle Database 23ai Free con Podman

### Preparar Podman y descargar la imagen

En primer lugar lo que he echo ha sido actualizar la lista de paquetes e instalar podman. Una vez instalado podman he descargado la imagen y he comprobado que se había guardado correctamente 

![Captura 1](img/Captura%20de%20pantalla%202026-10-07%20133203.png)

![Captura 2](img/Captura%20de%20pantalla%202026-10-07%20133831.png)

![Captura 4](img/Captura%20de%20pantalla%202026-10-08%20105525.png)

![Captura 5](img/Captura%20de%20pantalla%202026-10-08%20105732.png)

### Crear y  comprobar el contenedor

Luego de haber instalado la imagen de podman, he creado el volumen para almacenar los datos de la base de datos. Luego le he puesto un nombre al contenedor (cont_oracle(me he confundido al copiar de la práctica)), publicando el puerto 1521 y lo he vinculado al volumen. Por último he comprobado que el contenedor estaba en ejecución y comprobar que la base de datos estaba iniciándose correctamente.

![Captura 6](img/Captura%20de%20pantalla%202026-10-08%20132356.png)

![Captura 7](img/Captura%20de%20pantalla%202026-10-08%20133131.png)

![Captura 8](img/Captura%20de%20pantalla%202026-10-08%20132541.png)

### Entrar en Oracle y crear el usuario de trabajo

Una vez que he comprobado que el contenedor si estaba en ejecución, he entrado en el para verificar el entorno interno y luego iniciar la consola de Oracle como administrador

- Sudo podman exec -it cont_oracle /bin/bash: 
  Este comando es el que me entra al contenedor para ver que todo funciona correctamente

- sudo podman exec -it cont-oracle sqlplus / as sysdba: 
  Con esto he ejecutado SQL*Plus dentro del contenedor y me he conectado como usuario
  
![Captura 9](img/Captura%20de%20pantalla%202026-10-09%20115953.png)

Dentro de SQL, he comprobado el PDB y he creado el usuario FREEPDB1

![Captura 10](img/Captura%20de%20pantalla%202026-10-09%20120157.png)

![Captura 11](img/Captura%20de%20pantalla%202026-10-09%20120701.png)

Por último he comprobado la conexión como usuario de trabajo

![Captura 12](img/Captura%20de%20pantalla%202026-10-09%20120924.png)

### Desplegar PostgreSQL

Lo primero que he vuelto a hacer es actualizar los repositorios del sistema y después he instalado el paquete del servidor. Una vez instalado, he iniciado el servicio, y lo he habilitado para que se ejecutara automáticamente al arrancar la máquina. Al final he entrado al usuario.

- sudo apt install postgresql postgresql-contrib php-pgsql:
  Con este comando se instala postgreSQL, los módulos adicionales y el paquete PHP para conectar aplicaciones web con la base de datos
  
![Captura 13](img/Captura%20de%20pantalla%202026-10-09%20121324.png)

![Captura 14](img/Captura%20de%20pantalla%202026-10-09%20121420.png)

![Captura 15](img/Captura%20de%20pantalla%202026-10-09%20122030.png)

He creado el usuario y le he dado a pguser todos los privilegios de la base de datos

![Captura 16](img/Captura%20de%20pantalla%202026-10-09%20122051.png)

He salido de la sesión del usuario de postgre y he comprobado la conexión

![Captura 17](img/Captura%20de%20pantalla%202026-10-09%20122525.png)

###  Desplegar MariaDB

Para instalar MariaDB, primero he actualizado los repositorios del sistema y después instalé el servidor y el cliente

![Captura 18](img/Captura%20de%20pantalla%202026-10-09%20123519.png)

Una vez instalado, he activado el servicio para que se iniciara automáticamente y lo arranco. Una vez dentro creo la base de datos y el usuario, le damos todos los permisos y actualizo la tabla interna de permisos para que los cambios se aplique 

![Captura 19](img/Captura%20de%20pantalla%202026-10-09%20123603.png)

Por último compruebo el acceso local

![Captura 20](img/Captura%20de%20pantalla%202026-10-09%20123630.png)


## Conexiones desde otra máquina

- **POSTGRESQL**
![Captura 2](img/Captura%20de%20pantalla%202026-10-10%20133349.png)
![Captura 22](img/Captura%20de%20pantalla%202026-10-10%20133514.png)

- **MARIADB**
![Captura 23](img/Captura%20de%20pantalla%202026-10-10%20133514.png)


## Características de la VM y versiones instaladas de Oracle 23ai Free, PostgreSQL y MariaDB.

- Sistema operativo: Linux Mint
- Versiones de los SGBD:
  - Oracle Database 23ai Free (23.4.0.24.05)
  - PostgreSQL (Ubuntu 16.15-0ubuntu0.24.04.1
  - Mariadb ( ver 15.1 Distrib 10.11.14-MariaDB)
 
  ##  Cómo comprobaste el estado de los tres gestores y la conexión con orauser, pguser y muser.
  
1. Para comprobar el estado del contenedor de **Oracle**, he utilizado los siguientes comandos:

- `sudo podman ps`
- `sudo podman ps-a`
- `sudo podman logs cont_oracle`
     
Después he comprobado la conexión con el comando:

- `sudo podman exec -it cont_oracle sqlplus / as sysdba`

2. Para comprobar que el servicio de **Postgre** estaba activo ejecuté el siguiente comando:
- `sudo systectl status postgresql`

 Luego he entrado por consola:

 - `sudo -i -u postgres`
 - `psql`

He comprobado la conexión con:

- `psql -U pguser -d dbpg -W`


3. He comprobado que el servicio de **MariaDB** estaba activo con:

- `sudo systemctl status mariadb`

He entrado en la consola:

- `sudo maridb`

He comprobado la conexión con muser:

- `mariadb -u muser -p dbm`

  
##  Configuración de red realizada, si habilitaste conexiones desde otra máquina

No he habilitado conexiones desde otra máquina

## ERRORES
1. No se si es un error, pero he utilizado una máquina mint que ya tenía pero era de 50 GB de almacenamiento y la tarea me ponia de 250 GB por lo que en la terminal de mi pc he cambiado el tamaño con el comando
- `VBoxManage modifyhd "C:\Users\X1704\VirtualBox VMs\ASGBD-Mint-Miriam\ASGBD-Mint-Miriam.vdi" --resize 256000`, pero mi máquina todavía utilizaba los 50GB así que he instalado gparted con el comando
- `sudo apt install gparted`  ,   lo he abierto desde
- `sudo gparted` y he ocupado todo el espacio sin asignar, le he dado a aplicar y he reiniciado la máquina. He vuelto a abrir una terminal y he puesto el comando `df -h`
  
![Captura 3](img/Captura%20de%20pantalla%202026-10-08%20104508.png)


2. Me aparece un error como que el archivo se ha creado con un tamaño incorrecto para solucionarlo he instalado una versión anterior la **23.4.0.0**

  ![Captura 7](img/Captura%20de%20pantalla%202026-10-08%20123001.png)

## BIBLIOGRAFÍA

[(¿Qué es utf8mb4? ](https://oneuptime.com/blog/post/2026-03-31-mysql-utf8mb4-what-it-is-and-why-use-it/view)
