# INSTALACIÓN DE ARCH LINUX EN VIRTUALBOX
Instalación de Arch Linux como una máquina virtual en virtualbox.
<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_VirtualBox/main/18.png" alt="virtualbox">
<hr>

<code>Descargamos la imagen iso de Arch Linux -> https://archlinux.org/download/</code>

<h4>La máquina del ejemplo tendrá estas características como mínimo</h4>
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

<h3>Ya en la máquina virtual</h3>
<p>Lo primero sera configurar el teclado</p>
<code>loadkeys es</code>
<code>loadkeys la-latin1</code>

<p>Ver todas las distribuciones de idioma del teclado</p>
<code>localectl list-keymaps | less</code>

<p>Comprobar si la computadora tiene internet</p>
<code>ping google</code><br>
<p>Como es una maquina virual tiene acceso a la red mediante una NAT</p>

<p>Menu para crear particiones</p>
<code>fdisk -l</code><br>

<p>Menu para crear tabla de particiones mbr</p>
<code>fdisk /dev/sda</code><br>
<p>Creamos la tabla de particiones mbr</p>
<code>o</code>
<p>Guardamos los cambios<p>
<code>w</code>

<p>Entramos a la tabla para crear particiones</p>
<code>cfdisk</code><br>

<p>Creando las particiones</p>
<p>Primera particion para el boot</p>
<ul>
	<li>512M</li>
	<li>primary</li>
	<li>bootable</li>
	<li>write -> yes</li>
</ul>

<p>Segunda partición para la raiz donde se instalara todo el sistema oeprativo</p>
<ul>
	<li>20G</li>
	<li>primary</li>
	<li>write -> yes</li>
</ul>
	
<p>Tercera partición para el home donde estara toda la información de los usuarios que vaya a tener la máquina virtual. Además le restamos el tamaño de la menoria para el swap. La memoria de swap es la misma cantidad de la menoria ram</p>
<ul>
	<li>espacioTotal - 4G</li>
	<li>primary</li>
	<li>write -> yes</li>
</ul>
	
<p>Cuarta partición para la memoria de intercambio o swap</p>
<ul>
	<li>la misma cantidad que le dimos en memoria ram</li>
	<li>primary => No importa mucho si es primary o extend</li>
	<li>write -> yes</li>
</ul>
	
<p>Debemos cambiar el tipo de la memoria swap a <strong>82 linux swap / solaris</strong></p>
write -> yes <br>
quit <br>

<p>Formatemos las particiones para luego motarlar e instalarlas</p>
<p><code>mkfs.ext2 /dev/sda1</code> Es la partición del boot<br></p>
<p><code>mkfs.ext4 /dev/sda2</code> Es la partición de la raiz<br></p>
<p><code>mkfs.ext4 /dev/sda3</code> Es la partición del home<br></p>
<p><code>mkswap /dev/sda4</code> Es la partición de la memoria de intercambio o swap<br></p>
<p><code>swapon</code> Encendemos el swap<br></p>
	
<p>Montamos las particiones</p>
<code>mount /dev/sda2 /mnt => La raiz se ba a montar en la carpeta mnt</code><br>
<p>Creamos la carpeta o directorio para el boot</p><br>
	<code>mkdir /mnt/boot</code><br>
<p>Mostamos el boot en la carpeta /mnt/home</p><br>
	<code>mount /dev/sda1 /mnt/boot</code> La particion boot es la 1<br>
<p>Creamos la carpeta o directorio para el home</p><br>
	<code>mkdir /mnt/home</code><br>
<p>Mostamos el home en la carpeta /mnt/home</p><br>
	<code>mount /dev/sda3 /mnt/home</code> La particion home es la 2<br>


<p>Instalamos el sistema operativo base y unos paquetes más</p>
<code>pacstrap /mnt linux linux-firmware base nano os-prober grub networkmanager dhcpcd xterm efibootmgr</code><br>

<p>Guardamos nuestro trabajo de descarga en el fichero fstab</p>
<p>Creamos el fichero fstab y guerdamos lo descargado</p>
<code>genfstab /mnt >> /mnt/etc/fstab</code><br>

<code>Así vemos el contenido del fichero</code><br>
<p>cat /mnt/etc/fstab</p>
	
<p>Accedemos al sistema operativo descargado</p>
<code>arch-chroot /mnt</code><br>
<p>Estamos en el directorio raiz ( root@archiso )</p>
<p>Configuramos el nombre de la maquina</p>
<code>echo alvaropc > /etc/hostname</code><br>


<p>Ver zonas horarias buscamos la nuestra para asegurarnos que exista</p>
<code>timedatectl list-timezones</code><br>

<p>Configuramos el relog</p>
	<code>ln -sf /usr/share/zoneinfo/America/Guayaquil /etc/localtime</code><br>

<p>Configuramos el idioma, abriendo con el editor de tecto nano</p>
	<code>nano /etc/locale.gen</code><br>

<p>Buscamos nuestro idioma es_EC.UTF-8 UTF-8. Le descomentamos<p>
	<code>ctrl + o</code> Guardamos y nos preguntara el nombre de damos intro para selecionar el mismo<br>
	<code>ctrl + x</code> Salimos<br>
	
<p>Activamos el idioma</p>
	<code>locale-gen</code><br>

<p>Configuramos el relog segun la zona horaria</p>
	<code>hwclock -w </code><br>

<p>Configuramos el idioma del teclado</p>
	<code>echo KEYMAP=es > /etc/vconsole.conf</code><br>

<p>Configuramos el idioma o lenguaje</p>
	<code>echo LANG=es_EC.UTF-8 > /etc/locale.conf</code><br>

<p>Instalamos el grub ( viene siendo el gestor de aranque de linux )</p>
	<code>grub-install /dev/sda</code> No le ponemos nada mas ni numeros de las particiones ni nada<br>

<p>Configuramos el grub</p>
	<code>grub-mkconfig -o /boot/grub/grub.cfg</code>
	
<p>Creamos la contraseña del usuario root</p>
	<code>passwd</code> Le damos una contraseña para el usuario root.
	
<p>Empezamos a añadir los usuarios</p>
	<code>useradd -m alvaro</code> Se abra creado dentro de nuestra particion home un directorio llamado alvaro y ahi se almacenara toda la 	informacion referente a este usuario.
	
<p>Le damos una clave a ese usuario</p>
	<code>passwd alvaro</code> Escribimos la clave para el usuario alvaro.
<p>Instalamos un controlador de video</p>
	<code>pacman -S xf86-video-vesa</code>
<p>Instalamos xorg</p>
	<code>pacman -S xorg-server xorg-xinit mesa mesa-demos</code>
<p>Cargador de arranque</p>
	<code>grub-install --target=x86_64-efi --efi-directory=/boot</code>
	<code>os-prober</code>
	<code>grub-mkconfig -o /boot/grub/grub.cfg</code>
<p>Instalamos sudo</p>
	<code>pacman -S sudo</code>
<p>Agregar usuarios al wheel para despues tener permisos de super usuario mediante el comando sudo</p>
	<code>usermod -aG wheel,video,audio,storage username</code>
<p>Edita /etc/sudoers con nano o vim y descomenta la línea con "wheel":</p>
	Antes<br>
	<code>## Uncomment to allow members of group wheel to execute any command <br>
	# %wheel ALL=(ALL) ALL</code>
	Despues<br>
	<code>## Uncomment to allow members of group wheel to execute any command <br>
	%wheel ALL=(ALL) ALL</code>
<p>Salir de la imagen ISO, desmóntala y extráela</p>
	<code>exit</code>
	<code>umount -R /mnt</code>
	<code>reboot</code>
<p>Yo tengo internet mediante cable, así que no tendre problemas con el internet</p>
<p>Comprobamos si tenemos internet en la máquina</p>
	<code>ping google</code>
<p>No tendremos internet así que hay que activar el NetworkManager</p>
	<code>systemctl start NetworkManager.service</code>
	<code>systemctl enable NetworkManager.service</code>
<p>Comprobamos si tenemos internet en la máquina</p>
	<code>ping google</code>
	
	
	
<p>Instalamos xorg</p>
	<code>sudo pacman -S xorg</code>

<h3>Entorno gráfico</h3>
<p>Instalamos algunos paquetes como un entorno grafico ( En este caso instalare Qtile )</p>
	<code>sudo pacman -S lightdm lightdm-gtk-greeter qtile xterm code firefox</code>
<p>Activa el servicio de lightdm y reinicia el ordenador, deberías poder iniciar sesión en Qtile a través de lightdm.</p>
	<code>sudo systemctl enable lightdm</code>
	<code>reboot</code>
<p>Dentro de Qtile cambiamos el idioma del teclado a españon</p>
	<code>setxkbmap es</code>

