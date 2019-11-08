# Montar dispositivo

Una vez finalizado el proceso de [Borrado seguro con la herramienta SHRED de Linux](https://github.com/IngriMV/Borrado_seguro_SHRED_Linux) se debe montar de nuevo la unidad.

Al ejecutar el comando para formatear la unidad

**Paso 1:** 

```
$sudo fdisk -l
```

**Paso 2:**
```
$sudo umount /dev/sdb
```
Si genera el siguiente mensaje **Refusing to make a filesystem here!** eso quiere decir que la salida de `fdisk` muestra que no hay partición en su dispositivo usb. 

Los siguientes pasos son para dar solución al mensaje,

**Paso 3:**
Ya identificada la unidad se ejecuta el siguiente comando

```
$sudo fdisk /dev/sdb
```

**Paso 4:**

Se debe crear una nueva tabla de particiones una vez ejecutado el comando anterior presionar la letra `o` seguido de `Enter` 
se mostrará algo así:

```
Command (m for help): o

Created a new DOS disklabel with disk identifier 0x100000.
```

**Paso 5:**

Presione la tecla `n` luego presione 4 veces `enter`  o configure el valor deseado.

```
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): 
```

**Paso 6:**

Ahora se selecciona el tipo de partición, presionar la tecla `t` y luego `enter` se debe seleccionar y/o asignar el número de la partición

```
Command (m for help): t

Selected partition 1
Hex code (type L to list all codes): 
```
**Paso 7:**

A continuación, debe insertar el código del tipo de partición, puede usar `L` para obtener la lista de códigos disponibles, para NTFS puede digitar el número `7` 


```
Hex code (type L to list all codes): L

 0  Empty           24  NEC DOS         81  Minix / old Lin bf  Solaris        
 1  FAT12           27  Hidden NTFS Win 82  Linux swap / So c1  DRDOS/sec (FAT-
 2  XENIX root      39  Plan 9          83  Linux           c4  DRDOS/sec (FAT-
 3  XENIX usr       3c  PartitionMagic  84  OS/2 hidden or  c6  DRDOS/sec (FAT-
 4  FAT16 <32M      40  Venix 80286     85  Linux extended  c7  Syrinx         
 5  Extended        41  PPC PReP Boot   86  NTFS volume set da  Non-FS data    
 6  FAT16           42  SFS             87  NTFS volume set db  CP/M / CTOS / .
 7  HPFS/NTFS/exFAT 4d  QNX4.x          88  Linux plaintext de  Dell Utility   
 8  AIX             4e  QNX4.x 2nd part 8e  Linux LVM       df  BootIt
  
```

**Paso 8:**

Para ejecutar y/o escribir los cambios en el disco presionar la tecla `W` seguido de `Enter`

```
Command (m for help): w
The partition table has been altered.
Syncing disks.
```
**Paso 9:**

Ahora se crea el sistema de archivos en este caso NTFS con el siguiente comando:

```
$sudo mkfs.ntfs /dev/sdb1

```



