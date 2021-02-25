# Delete all usb partitions

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
