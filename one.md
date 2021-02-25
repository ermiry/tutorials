# Differences between sda, hda and vda
### sda and hda
1. sdx es el primer disco de tipo IDE/SATA/SCSI.
2. hdx es un disco fisico emulado.  
Cuando el kernel o algun programa accesan a estos se pueden realizar diferentes cosas especificas de discos fisicos.
### vda
1. vdx es para discos virtuales. Lo que el kernel hace cuando accesa es decirle al software de visualizacion que la informacion se necesita leer o escribir.  
En general, vdx es mas rapido dado que el kernel no tiene que decirle al disco que hacer, solo debe comunicarse con el **hypervisor** de la VM.