# -instalar-tres-SGBD

##  Desplegar Oracle Database 23ai Free con Podman

### Preparar Podman y descargar la imagen
  
![Captura 1](img/Captura%20de%20pantalla%202026-10-07%20133203.png)
![Captura 2](img/Captura%20de%20pantalla%202026-10-07%20133831.png)
![Captura 4](img/Captura%20de%20pantalla%202026-10-08%20105525.png)
![Captura 5](img/Captura%20de%20pantalla%202026-10-08%20105732.png)

### Crear y  comprobar el contenedor
![Captura 6](img/Captura%20de%20pantalla%202026-10-08%20132356.png)
![Captura 7](img/Captura%20de%20pantalla%202026-10-08%20133131.png)
![Captura 8](img/Captura%20de%20pantalla%202026-10-08%20132541.png)

### Entrar en Oracle y crear el usuario de trabajo
![Captura 9](img/Captura%20de%20pantalla%202026-10-09%20115953.png)
![Captura 10](img/Captura%20de%20pantalla%202026-10-09%20120157.png)
![Captura 11](img/Captura%20de%20pantalla%202026-10-09%20120701.png)
![Captura 12](img/Captura%20de%20pantalla%202026-10-09%20120924.png)

### Desplegar PostgreSQL


## ERRORES
1. No se si es un error, pero he utilizado una máquina mint que ya tenía pero era de 50 GB de almacenamiento y la tarea me ponia de 250 GB por lo que en la terminal de mi pc he cambiado el tamaño con el comando
- `VBoxManage modifyhd "C:\Users\X1704\VirtualBox VMs\ASGBD-Mint-Miriam\ASGBD-Mint-Miriam.vdi" --resize 256000`, pero mi máquina todavía utilizaba los 50GB así que he instalado gparted con el comando
- `sudo apt install gparted`  ,   lo he abierto desde
- `sudo gparted` y he ocupado todo el espacio sin asignar, le he dado a aplicar y he reiniciado la máquina. He vuelto a abrir una terminal y he puesto el comando `df -h`
![Captura 3](img/Captura%20de%20pantalla%202026-10-08%20104508.png)


2. Me aparece un error como que el archivo se ha creado con un tamaño incorrecto para solucionarlo he instalado una versión anterior la **23.4.0.0**

  ![Captura 7](img/Captura%20de%20pantalla%202026-10-08%20123001.png)


