# -instalar-tres-SGBD

##  Desplegar Oracle Database 23ai Free con Podman

- Preparar Podman y descargar la imagen
  
![Captura 1](img/Captura%20de%20pantalla%202026-10-07%20133203.png)
![Captura 2](img/Captura%20de%20pantalla%202026-10-07%20133831.png)
![Captura 4](img/Captura%20de%20pantalla%202026-10-08%20105525.png)


## ERRORES
- No se si es un error, pero he utilizado una máquina mint que ya tenía pero era de 50 GB de almacenamiento y la tarea me ponia de 250 GB por lo que en la terminal de mi pc he cambiado el tamaño con el comando `VBoxManage modifyhd "C:\Users\X1704\VirtualBox VMs\ASGBD-Mint-Miriam\ASGBD-Mint-Miriam.vdi" --resize 256000`, pero mi máquina todavía utilizaba los 50GB así que he instalado gparted con el comando sudo apt install gparted, lo he abierto desde sudo gparted y he ocupado todo el espacio sin asignar, le he dado a aplicar y he reiniciado la máquina. He vuelto a abrir una terminal y he puesto el comando df -h
![Captura 3](img/Captura%20de%20pantalla%202026-10-08%20104508.png)
