Cambiar el shell predeterminado de un usuario linux 




# Administracion de Servidores Linux

## Cambiar el shell predeterminado de un usuario linux 
En este artículo, describiremos cómo cambiar el shell de un usuario en Linux. El shell es un programa que acepta e interpreta comandos; hay **varios shells como bash, sh, ksh, zsh, fish y muchos otros** shells menos conocidos disponibles en Linux.

Bash (/ bin/bash) es un shell popular en la mayoría de los sistemas Linux, si no en todos, y normalmente es el shell predeterminado para las cuentas de usuario.

Hay varias razones para cambiar el shell de un usuario en Linux, incluidas las siguientes:

* Para bloquear o deshabilitar los inicios de sesión normales de los usuarios en Linux usando un shell nologin.
* Utilice un programa o script de envoltura de shell para iniciar sesión en los comandos de usuario antes de que se envíen a un shell para su ejecución. Aquí, especifica el contenedor de shell como el shell de inicio de sesión de un usuario.
* Para satisfacer las demandas de un usuario (quiere usar un shell específico), especialmente aquellos con derechos administrativos.

Al crear cuentas de usuario con las utilidades useradd o adduser, la marca --shell se puede usar para especificar el nombre del shell de inicio de sesión de un usuario que no sea el especificado en los archivos de configuración respectivos.

Se puede acceder a un shell de inicio de sesión desde una interfaz basada en texto o mediante un SSH desde una máquina Linux remota. Sin embargo, si inicia sesión a través de una interfaz gráfica de usuario (GUI), puede acceder al shell desde emuladores de terminal como xterm, konsole y muchos más.

Primero enumeremos todos los shells disponibles en su sistema Linux, escriba.

`# cat /etc/shells`

> /bin/sh  
> /bin/bash  
> /sbin/nologin  
> /bin/tcsh  
> /bin/csh  
> /bin/dash  

Antes de continuar, tenga en cuenta que:

* Un usuario puede cambiar su propio shell a cualquier cosa: la cual, sin embargo, debe estar listada en el archivo/etc/shells.
* Solo root puede ejecutar un shell que no esté incluido en el archivo/etc/shells.
* Si una cuenta tiene un shell de inicio de sesión restringido, solo root puede cambiar el shell de ese usuario.

Ahora analicemos tres formas diferentes de cambiar el shell de usuario de Linux.  



## Cambiar Idioma de Teclado
***Linux: Configurar teclado español: Ubuntu/Debian***
``` 
# Instalamos paquetes:
sudo apt-get install console-data
# Cambiamos idioma:
sudo setxkbmap -layout 'es,es' -model pc105
```
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
