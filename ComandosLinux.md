Cambiar el shell predeterminado de un usuario linux 
Cambiar la ip de un linux
Cambiar Idioma de Teclado

Notas
Entender el uso de IP
Que es la IP 127.0.0.0


# Administracion de Servidores Linux

## Cambiar el shell predeterminado de un usuario linux 
En este artículo, describiremos cómo cambiar el shell de un usuario en Linux. El shell es un programa que acepta e interpreta comandos; hay **varios shells como bash, sh, ksh, zsh, fish y muchos otros** shells menos conocidos disponibles en Linux.

**Bash (/ bin/bash)** es un shell popular en la mayoría de los sistemas Linux, si no en todos, y normalmente es el shell predeterminado para las cuentas de usuario.

Hay varias razones para cambiar el shell de un usuario en Linux, incluidas las siguientes:

* Para bloquear o deshabilitar los inicios de sesión normales de los usuarios en Linux usando un shell nologin.
* Utilice un programa o script de envoltura de shell para iniciar sesión en los comandos de usuario antes de que se envíen a un shell para su ejecución. Aquí, especifica el contenedor de shell como el shell de inicio de sesión de un usuario.
* Para satisfacer las demandas de un usuario (quiere usar un shell específico), especialmente aquellos con derechos administrativos.

Al crear cuentas de usuario con las utilidades useradd o adduser, la marca --shell se puede usar para especificar el nombre del shell de inicio de sesión de un usuario que no sea el especificado en los archivos de configuración respectivos.

Se puede acceder a un shell de inicio de sesión desde una interfaz basada en texto o mediante un SSH desde una máquina Linux remota. Sin embargo, si inicia sesión a través de una interfaz gráfica de usuario (GUI), puede acceder al shell desde emuladores de terminal como xterm, konsole y muchos más.

Primero enumeremos todos los shells disponibles en su sistema Linux, escriba.

``` shell
# cat /etc/shells

> /bin/sh  
> /bin/bash  
> /sbin/nologin  
> /bin/tcsh  
> /bin/csh  
> /bin/dash  
```
Antes de continuar, tenga en cuenta que:

* Un usuario puede cambiar su propio shell a cualquier cosa: la cual, sin embargo, debe estar listada en el archivo/etc/shells.
* Solo root puede ejecutar un shell que no esté incluido en el archivo/etc/shells.
* Si una cuenta tiene un shell de inicio de sesión restringido, solo root puede cambiar el shell de ese usuario.

Ahora analicemos tres formas diferentes de cambiar el shell de usuario de Linux.  
















## Cambiar la ip de un equipo linux
establecer las configuraciones actuales asi como las interfaces de red existentes 

### Comandos Diversos de Linux para gestionar la red
ip a
```
Esto enumera todas las interfaces conectadas a su sistema
```shell
> ip a  
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever  
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:07:24:93 brd ff:ff:ff:ff:ff:ff
    altname enp2s1
    inet 192.168.126.37/24 brd 192.168.126.255 scope global noprefixroute ens33
       valid_lft forever preferred_lft forever
    inet6 fe80::20c:29ff:fe07:2493/64 scope link 
       valid_lft forever preferred_lft forever
```
Alternativamente, puede usar
```shell
> ip link show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 00:0c:29:07:24:93 brd ff:ff:ff:ff:ff:ff
    altname enp2s1

```
Como se ve en las 2 salidas anteriores, la interfaz conectada a la red es ens33

Para obtener una lista de los servicios de red de escucha, los deamons y los programas, escriba el siguiente comando:

```shell
> netstat -tulpen
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       User       Inode      PID/Program name    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      101        43007      -                   
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      0          50584      -                   
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      0          47524      -                   
tcp        0      0 127.0.0.1:33060         0.0.0.0:*               LISTEN      127        55758      -                   
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      127        55760      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      0          50699      -                   
tcp6       0      0 ::1:631                 :::*                    LISTEN      0          47523      -                   
tcp6       0      0 :::80                   :::*                    LISTEN      0          51341      -                   
udp        0      0 127.0.0.53:53           0.0.0.0:*                           101        43006      -                   
udp        0      0 0.0.0.0:631             0.0.0.0:*                           0          47079      -                   
udp        0      0 0.0.0.0:5353            0.0.0.0:*                           115        48472      -                   
udp        0      0 0.0.0.0:34197           0.0.0.0:*                           115        48474      -                   
udp6       0      0 :::49912                :::*                                115        48475      -                   
udp6       0      0 :::5353                 :::*                                115        48473      -  
```
para realizar un scaneo con el puerto
```shell
> nc -v 192.168.126.37 22
Connection to 192.168.126.37 22 port [tcp/ssh] succeeded!
SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.4
```

***Linux:Cambiar ip utilizando netplan: Ubuntu/Debian***
```
nano /etc/netplan/01-netcfg.yml
```
```
# esta configuracion es para uso de DHCP.
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: yes
```
```
# Esta configuracion es para una configuracion estatica con ip 192.168.126.37 mascara de sub red 255.255.255.0 (/24), la puerta de enlace predeterminada es 192.168.126.1 y servidores de DNS 8.8.8.8, 200.48.225.130 

network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
     dhcp4: no
     addresses: [192.168.126.37/24]
     gateway4: 192.168.126.1
     nameservers:
       addresses: [8.8.8.8,200.48.225.130]
```
```
sudo netplan apply
```
***Linux: Cambiar ip utilizando archivo de interfaces: Ubuntu/Debian***
Alternativamente, puede configurar una IP estática usando el archivo de configuración de interfaces que se encuentra en
```
/etc/network/interfaces
```
```
# interfaces por defecto configurado
auto lo
iface lo inet loopback
```
El siguiente paso es identificar la interfaz de red que necesitamos para asignar una dirección IP estática. Para lograr esto, ejecute el siguiente comando
```
Para configurar la dirección como una IP estática, abra el /etc/network/interfaces archivar y adjuntar las siguientes líneas
```
auto ens33
iface ens33 inet static
        address 192.168.126.37
        netmask 255.255.255.0
        gateway 192.168.126.1
        dns-nameservers 192.168.126.1 8.8.8.8
```



## Cambiar Idioma de Teclado
***Linux: Configurar teclado español: Ubuntu/Debian***
``` 
# Instalamos paquetes:
sudo apt-get install console-data
# Cambiamos idioma:
sudo setxkbmap -layout 'es,es' -model pc105

***Linux: Configurar teclado español: Kali Linux***
```
#Cargamos idioma de teclado español:
setxkbmap es sundeadkeys
```
***Linux: Configurar teclado español: CentOS7 / RHEL7***
```
#Si no tenemos el comando loadkeys
yum install kbd -y
#Cargar el idioma de teclado español de forma temporal:
loadkeys es
#Cargar el idioma de teclado español de forma permanente:
localectl set-keymap es
#Ver la configuración de idioma del teclado:
localectl
#Ver idiomas disponibles:
localectl list-keymaps
```
***Linux: Configurar teclado español: CentOS6 / RHEL6***
```
#Editamos el fichero de configuración con un editor de texto:
/etc/sysconfig/keyboard
#Cambiamos los siguientes parámetros para configurar el idioma español:
KEYTABLE="es"
MODEL="pc105+inet"
LAYOUT="es"
KEYBOARDTYPE="pc"
```

# Notas
## *Entender el uso de IP*   

[IP Addressing and Subnetting for New Users](https://www.cisco.com/c/es_mx/support/docs/ip/routing-information-protocol-rip/13788-3.html)

La direcciones IP privadas no son de nadie, y cualquier organización puede usarla sin necesidad de aprobación ni registro, pero estás direcciones no pueden transmitir a través del Internet público.

Entender cómo se usan los números de cada IP es algo bastante intrincado, pero los rangos que abarcan son algo más sencillos. Existen tres clases de direcciones IP privadas y abarcan unos 18 millones de números de direcciones IP en total:

    Clase A: van desde 10.0.0.0 a 10.255.255.255
    Clase B: van desde 172.16.0.0 a 172.31.255.255
    Clase C: van desde 192.0.0.1 a 192.168.255.255

* ***La Clase A es la clase para las redes muy grandes***, como las de una compañía internacional. 
* ***Las Clase B son para redes de tamaño mediano***, como por ejemplo la red de una universidad. 
* ***Las direcciones IP de la clase C se usan normalmente para las redes más pequeñas***. 192.168.1.1 cae dentro del espacio de direcciones privadas más pequeño (entre 192.168.0.0 y 192.168.255.255). Fíjate que el rango de las IP Clase C empiezan en 192.0.0.1.
## *Que es la IP 127.0.0.0*
No hay lugar como el hogar. Otra dirección bastante interesante es 127.0.0.1, la dirección de bucle local o loopback. Es la IP que usa tu ordenador para hablar consigo mismo.

**La IP 127.0.0.1 hace referencia al localhost, es decir al anfitrión local, es decir a la PC que estás usando.** Se puede usar para para localizar alguna avería, para hacer pruebas de la red, o para acceder a un servicio web que se haya instalado en el propio ordenador.

**Los estándares de redes IPv4 utilizan en su mayoría la dirección 127.0.0.1 como loopback,** por ello las direcciones 127.x.x.x se reservan para designar la propia máquina. En 1981, 0 y 127 eran las únicas redes clase A reservadas. 0 fue usada para apuntar al huésped local y eso dejó a 127 para el bucle local.

La lógica detrás de esto es que 127 es el último número en una red clase A. 127.0.0.1 es el primer número asignable en la subred. **En binario 127 es es 01111111**, lo que hace a la dirección una "muy fácil de recordar". IPv6 usa en cambio ::1 o 0:0:0:0:0:0:0:1, una dirección que para muchos tiene más sentido porque es bastante más fácil de recordar.

