# 1.- Differences between sda, hda and vda
### sda and hda
1. sdx es el primer disco de tipo IDE/SATA/SCSI.
2. hdx es un disco fisico emulado.  
Cuando el kernel o algun programa accesan a estos se pueden realizar diferentes cosas especificas de discos fisicos.
### vda
1. vdx es para discos virtuales. Lo que el kernel hace cuando accesa es decirle al software de visualizacion que la informacion se necesita leer o escribir.  
En general, vdx es mas rapido dado que el kernel no tiene que decirle al disco que hacer, solo debe comunicarse con el **hypervisor** de la VM.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 2.- Mount and Unmount usb from command line

1. Primero mostrar los discos actuales
   
```
sudo lsblk
```

![First](images/two/one.png)

2. Conectar la usb y volver a mostrar la informacion de los discos

```
sudo lsblk
```

![Second](images/two/two.png)

3. Sabemos que la usb esta montada como el disco **sda** en el path **/media/ermiry/809A-1D08**. Para desmontar la usb corremos el siguiente comando

```
sudo umount /dev/sda1
```

![Third](images/two/three.png)

4. Volver a mostrar los discos para comprobar que la usb ya no esta montada

```
sudo lsblk
```

5. Crear una nueva carpeta donde se montara la usb nuevamente

```
sudo mkdir /mnt/disks
sudo mkdir /mnt/disks/usb
```

6. Montar la usb en el nuevo path **/mnt/disks/usb**

```
sudo mount /dev/sda1 /mnt/disks/usb
```

![Fourth](images/two/four.png)

7. Ya se puede accesar la informacion de la usb en el path **/mnt/disks/usb**

```
cd /mnt/disks/usb
ls 
```

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 3.- Show device information

1.- Entramos a la terminal 

2.- En la terminal meter el comando **lsblk**

```
 lsblk
 ```
 ![First](images/Three/One.png)

  Con ese comando se visualiza los dispositivos, unidades, particiones y sus capacidades (estén montadas o no las unidades).

  3.- Si al comando se le agrega **-fm** muestra informacion mas detallada de los dispositivos.

  ```
  lsblk -fm
  ```

  ![Second](images/Three/Two.png)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 4.- View linux disk partitions table 

 * Se ingresa el comando 
```
sudo fdisk -l
```

![imagen](images/four/4.jpeg)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 5.- Connect a USB and show partitions

1. Conectar la USB a la maquina y mostrar la informacion.

```
sudo lsblk
```

![First](images/five/one.PNG)

2. Con el comando **sudo fdisk -l** mostramos su tabla de particiones.

```
sudo fdisk -l
```
![Second](images/five/two.PNG)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 6.- Delete all usb partitions

1. Primero mostrar los discos actuales
   
```
sudo lsblk
```

2. Conectar la usb y volver a mostrar la informacion de los discos. Sabemos que la usb esta montada como el disco **sda** y tiene dos particiones:

- **sda1** montada en **/media/ermiry/max**
- **sda2** montada en **/media/ermiry/mariana**

```
sudo lsblk
```

![First](images/six/one.png)

3. Para desmontar la usb corremos los siguientes comandos

```
sudo umount /dev/sda1
sudo umount /dev/sda2
```

4. Utilizamos el siguiente comando para poder hacer modificaciones a las particiones de la usb

```
sudo fdisk /dev/sda
```

5. Dentro de la consola de **fdisk** metemos el comando **d** para borar las 2 particiones. Una vez que estemos seguros de los cambios se usa el comando **w** para es escribirlos definitivamente

![Second](images/six/two.png)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 7.- Create partitions inside usb

1. Primero mostrar los discos actuales
   
```
sudo lsblk
```

2. Conectar la usb y volver a mostrar la informacion de los discos para identificar cual es el disco que vamos a modificar

```
sudo lsblk
```

4. Desmontamos la usb para poder realizar operaciones en ella

```
sudo umount /dev/sda1
```

5. Utilizamos el comando **fdisk** para crear particiones. Se crearan **3 particiones primarias de 1GB c/u**

- Introducimos el comando **n** y seleccionamos **p** para crear una particion primaria
- Le dejamos el valor del primer sector como default
- Seleccionamos el ultimo sector usando **+1024M** para indicar que la particion tendra un tamano de **1GB**

![First](images/seven/one.png)

5.1 Repetimos los pasos anteriores para crear las siguientes dos particiones

![Second](images/seven/two.png)

6. Creamos una particion extendida en el espacio sobrante

- Introducimos el comando **n** y seleccionamos **e** para crear una particion extendida
- Le dejamos el valor del primer y ultimo sector como default

![Third](images/seven/three.png)

7. Para finalizar introducimos el comando **w** para que los cambios tengan efecto en el disco

![Four](images/seven/four.png)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 8.-Create a logical partition inside an extended partition

0. Para poder crear una particion logica en un disco, es necesario contar con una particion extendida. En este ejemplo se muestra una usb con 3 particiones primarias y una extendida

1. Se debe de desmontar la usb para poder realizar operaciones en ella

```
sudo umount /dev/sda1
```

1. Utilizamos el comando **fdisk** para crear la particion logica
- Si no existen 3 particiones primarias, introducimos el comando **l** para seleccionar una particion logica. Si ya existen particones primarias (como en este ejemplo) solo tendremos la opcion de crear una particion logica
- Dejamos el valor de primer sector con el valor default
- Seleccionamos el tamanoop que le queremos dar a la particion, en este caso de 512M
- Introducimos el comando **w** para registrar los cambios en el disco

![First](images/eight/one.png)

2. Ahora podemos desplegar las particiones del disco para verificar que tengamos la nueva particion

![Second](images/eight/two.png)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 9.- Use the disks application

1. En ubuntu abrir la aplicacion denominada **disks**. Esta applicaion nos permite ver los dispositivos de almacenamiento que tengamos conectados al igual que las particiones que existen en cada uno de ellos

![First](images/nine/one.png)

2. Al insertar la usb, podemos observar que nos aparece un dispositivo nuevo en la barra izquierda; si lo seleccionamos podremos observar las particiones que actuamente tiene

![Second](images/nine/two.png)

3. Para eliminar una particion del disco, la seleccionamos haciendo click sobre ella, despues seleccionamos el boton de **-** y confirmamos en el dialogo que la queremos borrar

![Thrid](images/nine/three.png)

4. Releazamos el paso **3** con las demas particiones que existan en nuestra usb

5. En este punto no debemos de tener ninguna particion en la usb

![Four](images/nine/four.png)

6. Procedemos a crear una nueva particion que pueda abarcar todo el disco
- Seleccionar el espacio libre del disco y oprimir el boton **+**
- Seleccionamos el tamano completo del disco (en este caso de 4GB)
- Le damos un nombre a nuestra particion y selecionamos que utilice el formato FAT
- Seleccionamos el boton create

![Five](images/nine/five.png)

7. Terminamos con una particion primaria del tamano completo del disco

![Six](images/nine/six.png)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

10

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
