# INSTALACIÓN DE ARCH LINUX EN VIRTUALBOX
Instalación de Arch Linux como una máquina virtual en virtualbox.
	<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/18.png" alt="virtualbox">
	<hr>

<code>Descargamos la imagen iso de Arch Linux -> <a href="https://archlinux.org/download">iso Arch Linux</a>/</code>

<h3>Para crear una máquina virtual en virual box como mínimo estos requisitos</h3>
<ul>
	<li>minimo 248M de ram</li>
	<li>minimo 20G memoria</li>
</ul>

<h3>La máquina del ejemplo tendrá estas características como mínimo</h3>
	<ul>
		<li>50GB Almacenamiento</li>
		<li>4GB Ram</li>
		<li>128MB memoria gráfico</li>
	</ul>

<h3>En Oracle VM VirtualBox</h3>
	<ul>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/1.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/2.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/3.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/4.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/5.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/6.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/7.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/8.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/9.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/10.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/11.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/12.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/13.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/14.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/15.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/16.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/17.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/18.png" alt="instalación de virtualbox">
		</li>
		<li>
			<img src="https://raw.githubusercontent.com/Curipoma/instalacion_arch_linux_virtualbox/main/img/20_1.png" alt="instalación de virtualbox">
		</li>
	</ul>

<h3>En la linea de comandos de la máquina virtual</h3>
<ul>
	<li>
		<p>Lo primero sera configurar el teclado</p>
		<code>loadkeys es</code><br>
		<code>loadkeys la-latin1</code>
	</li>
	<li>
		<p>Ver todas las distribuciones de idioma del teclado</p>
		<code>localectl list-keymaps | less</code>
	</li>
	<li>
		<p>Comprobar si la computadora tiene internet</p>
		<code>ping google</code>
		<p>Como es una maquina virual tiene acceso a la red mediante una NAT</p>
	</li>
	<li>
		<p>Menu para crear particiones</p>
		<code>fdisk -l</code>
	</li>
	<li>
		<p>Menu para crear tabla de particiones mbr</p>
		<code>fdisk /dev/sda</code>
	</li>
	<li>
		<p>Creamos la tabla de particiones mbr</p>
		<code>o</code>
	</li>
	<li>
		<p>Guardamos los cambios<p>
		<code>w</code>
	</li>
	<li>
		<p>Entramos a la tabla para crear particiones</p>
		<code>cfdisk</code>
	</li>
	<li>
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
	</li>
	<li>
		<p>Formatemos las particiones para luego motarlar e instalarlas</p>
		<p><code>mkfs.ext2 /dev/sda1</code> Es la partición del boot</p>
		<p><code>mkfs.ext4 /dev/sda2</code> Es la partición de la raiz</p>
		<p><code>mkfs.ext4 /dev/sda3</code> Es la partición del home</p>
		<p><code>mkswap /dev/sda4</code> Es la partición de la memoria de intercambio o swap</p>
		<p><code>swapon</code> Encendemos el swap</p>
	</li>
	<li>
		<p>Montamos las particiones</p>
		<p>La raiz se ba a montar en la carpeta mnt</p>
			<code>mount /dev/sda2 /mnt</code>
		<p>Creamos la carpeta o directorio para el boot</p>
			<code>mkdir /mnt/boot</code>
		<p>Mostamos el boot en la carpeta /mnt/home</p>
			<code>mount /dev/sda1 /mnt/boot</code> La particion boot es la 1
		<p>Creamos la carpeta o directorio para el home</p>
			<code>mkdir /mnt/home</code>
		<p>Mostamos el home en la carpeta /mnt/home</p>
			<code>mount /dev/sda3 /mnt/home</code> La particion home es la 3
	</li>
	<li>
		<p>Instalamos el sistema operativo base y unos paquetes más</p>
		<code>pacstrap /mnt linux linux-firmware base nano os-prober grub networkmanager dhcpcd xterm efibootmgr</code>
	</li>
	<li>
		<p>Guardamos nuestro trabajo de descarga en el fichero fstab</p>
		<p>Creamos el fichero fstab y guerdamos lo descargado</p>
		<code>genfstab /mnt >> /mnt/etc/fstab</code>
	</li>
	<li>
		<code>Así vemos el contenido del fichero</code>
		<p>cat /mnt/etc/fstab</p>
	</li>
	<li>
		<p>Accedemos al sistema operativo descargado</p>
		<code>arch-chroot /mnt</code>
	</li>
	<li>
		<p>Estamos en el directorio raiz ( root@archiso ).</p>
		<p>Configuramos el nombre de la maquina</p>
		<code>echo alvaropc > /etc/hostname</code>
	</li>
	<li>
		<p>Ver zonas horarias buscamos la nuestra para asegurarnos que exista</p>
		<code>timedatectl list-timezones</code>
	</li>
	<li>
		<p>Configuramos el relog</p>
		<code>ln -sf /usr/share/zoneinfo/America/Guayaquil /etc/localtime</code>
	</li>
	<li>
		<p>Configuramos el idioma, abriendo con el editor de tecto nano</p>
		<code>nano /etc/locale.gen</code>
	</li>
	<li>
		<p>Buscamos nuestro idioma es_EC.UTF-8 UTF-8. Le descomentamos<p>
		<p><code>ctrl + o</code> Guardamos y nos preguntara el nombre de damos intro para selecionar el mismo</p>
		<p><code>ctrl + x</code> Salimos</p>
	</li>
	<li>
		<p>Activamos el idioma seleccionado</p>
		<code>locale-gen</code>
	</li>
	<li>
		<p>Configuramos el relog según la zona horaria</p>
		<code>hwclock -w </code>
	</li>
	<li>
		<p>Configuramos el idioma del teclado a español</p>
		<code>echo KEYMAP=es > /etc/vconsole.conf</code>
	</li>
	<li>
		<p>Configuramos el idioma o lenguaje</p>
		<code>echo LANG=es_EC.UTF-8 > /etc/locale.conf</code>
	</li>
	<li>
		<p>Instalamos el grub ( viene siendo el gestor de aranque de linux )</p>
		<p><code>grub-install /dev/sda</code> No le ponemos nada mas ni numeros de las particiones ni nada</p>
	</li>
	<li>
		<p>Configuramos el grub</p>
		<code>grub-mkconfig -o /boot/grub/grub.cfg</code>
	</li>
	<li>
		<p>Creamos la contraseña del usuario root</p>
		<p><code>passwd</code> Le damos una contraseña para el usuario root.</p>
	</li>
	<li>
		<p>Empezamos a añadir los usuarios</p>
		<p><code>useradd -m alvaro</code> Se abra creado dentro de nuestra partición home un directorio llamado alvaro y ahí se almacenará toda la información referente a ese usuario.</p>
	</li>
	<li>
		<p>Le damos una clave a ese usuario</p>
		<p><code>passwd alvaro</code> Escribimos la clave para el usuario alvaro.</p>
	</li>
	<li>
		<p>Instalamos un controlador de video</p>
		<code>pacman -S xf86-video-vesa</code>
	</li>
	<li>
		<p>Instalamos xorg</p>
		<code>pacman -S xorg-server xorg-xinit mesa mesa-demos</code>
	</li>
	<li>
		<p>Cargador de arranque</p>
		<code>grub-install --target=x86_64-efi --efi-directory=/boot</code>
		<code>os-prober</code>
		<code>grub-mkconfig -o /boot/grub/grub.cfg</code>
	</li>
	<li>
		<p>Instalamos sudo</p>
		<code>pacman -S sudo</code>
	</li>
	<li>
		<p>Agregar usuarios al wheel para despues tener permisos de super usuario mediante el comando sudo</p>
		<code>usermod -aG wheel,video,audio,storage username</code>
	</li>
	<li>
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
	</li>
	<li>
		<p>Yo tengo internet mediante cable, así que no tendre problemas con el internet</p>
		<p>Comprobamos si tenemos internet en la máquina</p>
			<code>ping google</code>
		<p>No tendremos internet así que hay que activar el NetworkManager</p>
			<code>systemctl start NetworkManager.service</code>
			<code>systemctl enable NetworkManager.service</code>
		<p>Comprobamos si tenemos internet en la máquina</p>
			<code>ping google</code>
	</li>
	<li>
		<p>Instalamos xorg</p>
		<code>sudo pacman -S xorg</code>
	</li>
	<li>
		<h3>Entorno gráfico</h3>
		<p>Instalamos algunos paquetes como un entorno grafico ( En este caso instalare Qtile )</p>
			<code>sudo pacman -S lightdm lightdm-gtk-greeter qtile xterm code firefox</code>
		<p>Activa el servicio de lightdm y reinicia el ordenador, deberías poder iniciar sesión en Qtile a través de lightdm.</p>
			<code>sudo systemctl enable lightdm</code>
			<code>reboot</code>
		<p>Dentro de Qtile cambiamos el idioma del teclado a españon</p>
			<code>setxkbmap es</code>
	</li>
</ul>

