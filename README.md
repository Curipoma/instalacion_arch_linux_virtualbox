# INSTALACIÓN DE ARCH LINUX EN VIRTUALBOX
Instalación de Arch Linux como una máquina virtual en virtualbox.
<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_VirtualBox/main/18.png" alt="virtualbox">
<hr>

<code>Descargamos la imagen iso de -> https://archlinux.org/download/</code>

<h3>Características de la máquina del ejemplo</h3>
50GB Almacenamiento<br>
4GB Ram<br>
128MB memoria gráfico<br>

<h3>Para crear una maquina virtual en virual box como minimo estos requisitos</h3>
minimo 248M de ram<br>
minimo 20G memoria<br>

<h3>Cambiamos el orden de arranque</h3>
optica activo<br>
disco duro activo<br>
disquete<br>
red<br>

<h3>Configuramos las demas cosas según el gusto</h3>

<h3>Lo primero sera configurar el teclado</h3>
<code>loadkeys es</code>
<code>loadkeys la-latin1</code>

<h3>Ver todas las distribuciones de idioma del teclado</h3>
<code>localectl list-keymaps | less</code>

<h3>Comprobar si la computadora tiene internet</h3>
<code>ping google</code><br>
<p>Como es una maquina virual tiene acceso a la red mediante una NAT</p>

<h3></h3>
<code></code>
<br>

<h3>verificamos si tenemos particiones en el disco</h3>
<code>cfdisk</code><br>


# menu para crear particiones
fdisk -l

# menu para crear tabla de particiones mbr
fdisk /dev/sda
Creamos la tabla de particiones mbr
o 
Guardamos los cambios
w

# Entramos a la tabla para crear particiones
cfdisk

# Creando las particiones
primera particion => para el boot
	512M
	primary
	bootable
	write = yes
segunda particion => para la raiz => donde se instalara todo el sistema oeprativo
	20G
	primary
	write = yes
tercera particion = para el home => segun los usuario que vayas a tener ( menos la menoria para el swap (menoria del swap la misma que la de la menoria ram ) )
	espacioTotal - 2G
	primary
	write = yes
cuarta particion = para la memoria de intercambio o swap
	la_misma_cantidad_que_le_dimos_en_memoria_ram
	primary => No importa mucho si es primary o extend
	write = yes
Debemos cambiar el tipo de la memoria swap => 82 linux swap / solaris
write = yes
quit

# Formatemos las particiones para luego motarlar e instalarlas
mkfs.ext2 /dev/sda1 => Es la particion del boot
mkfs.ext4 /dev/sda2 => Es la particion de la raiz
mkfs.ext4 /dev/sda3 => Es la particion del home

mkswap /dev/sda4 => Es la particion de la memoria de intercambio
swapon => Encendemos el swap



# Montamos las particiones
mount /dev/sda2 /mnt => La raiz se ba a montar en la carpeta mnt

creamos la carpeta o directorio para el boot
mkdir /mnt/boot

mostamos el boot en la carpeta mnt
mount /dev/sda1 /mnt/boot => la particion boot es la 1

mkdir /mnt/home
mount /dev/sda3 /mnt/home => la particion home es la 2



# Desde aqui puedes puedes guiar en otro manual para ayudarte
https://github.com/antoniosarosi/dotfiles/blob/master/README.es.md



# Instalamos el sistema operativo base y unos paquetes mas
pacstrap /mnt linux linux-firmware base nano os-prober grub networkmanager dhcpcd xterm efibootmgr

# Guardamos nuestro trabajo en el fichero fstab
# Creamos el fichero fstab
genfstab /mnt >> /mnt/etc/fstab

# ver el contenido del fichero
cat /mnt/etc/fstab

# Accedemos al sistema operativo descargado
arch-chroot /mnt

# Estamos en el directorio raiz cuando el prom dice root@archiso ( si es asi esta instalado correctamente los paquetes iniciales )
# configuramos el nombre de la maquina
echo alvaropc > /etc/hostname

# Ver zonas horarias buscamos la nuestra para asegurarnos que exista
timedatectl list-timezones

# configuramos el relog
ln -sf /usr/share/zoneinfo/America/Guayaquil /etc/localtime

# configuramos el idioma => abriendo con el editor de tecto nano
nano /etc/locale.gen

# Buscamos nuestro idioma es_EC.UTF-8 UTF-8
Le descomentamos
ctrl + o => guardamos y nos preguntara el nombre de damos enter para selecionar el mismo
ctrl + x => salimos

# Activamos el idioma
locale-gen

# configuramos el relog segun la zona horaria
hwclock -w 

# Configuramos el idioma del teclado
echo KEYMAP=es > /etc/vconsole.conf

# Configuramos el idioma o lenguaje
echo LANG=es_EC.UTF-8 > /etc/locale.conf

# Instalamos el grub ( viene siendo el gestor de aranque de linux )
grub-install /dev/sda => No le ponemos nada mas ni numeros de las particiones ni nada

# configuramos el grub
grub-mkconfig -o /boot/grub/grub.cfg

# creamos la contraseña del usuario root
passwd => Le damos una contraseña para el usuario root

# Empezamos a añadir los usuarios
useradd -m alvaro => Se abra creado dentro de nuestra particion home un directorio llamado alvaro y ahi se almacenara toda la informacion referente a este usuario

# Le damos una clave a ese usuario
passwd alvaro => Escribimos la clave para el usuario alvaro

# Instalamos un controlador de video
pacman -S xf86-video-vesa

# instalamos xorg
pacman -S xorg-server xorg-xinit mesa mesa-demos

*Gestor de archivos pacman

# cargador de arranque
grub-install --target=x86_64-efi --efi-directory=/boot
os-prober
grub-mkconfig -o /boot/grub/grub.cfg

# agregar usuarios a wheel para despues tener permisos de super usuario
usermod -aG wheel,video,audio,storage username

#instalamos sudo
pacman -S sudo

# Edita /etc/sudoers con nano o vim y descomenta la línea con "wheel":
## Uncomment to allow members of group wheel to execute any command
# %wheel ALL=(ALL) ALL

# Sal de la imagen ISO, desmóntala y extráela
exit
umount -R /mnt
reboot

# Si reinicias y usas wifi te conectas a una red mediante esos comandos
# Lista las redes disponibles
nmcli device wifi list
# Conéctate a tu red
nmcli device wifi connect TU_SSID password TU_CONTRASEÑA

# Instalamos xorg
sudo pacman -S xorg

# Instalamos algunos paquetes como un entorno grafico ( En este caso instalare Qtile )
sudo pacman -S lightdm lightdm-gtk-greeter qtile xterm code firefox

# Activa el servicio de lightdm y reinicia el ordenador, deberías poder iniciar sesión en Qtile a través de lightdm.
sudo systemctl enable lightdm
reboot

# Dentro de Qtile cambiamos el idioma del teclado a españon 
setxkbmap es
