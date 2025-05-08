# Bitacora-IPV6
Bitacora de comandos de la clase SIS 252
- *#*: modo encendido
- *$*: modo configure terminal
- *&*: modo interface

| *Comando* | *Informacion* | *Tips* |
|:--------|:--------:|:--------:|
|  enable   |  Enciende el equip   |     |
|  #configure terminal   |  Row 2   |    |

# Configuracion Router IPV4

| *Comando* | *Informacion* | *Tips* |
|:--------|:--------:|:--------:|
|  $hostname NAME  |  Cambia el nombre a nuestro router  |     |
|  $interface fa0/0   |  Entramos a configurar la interfaz de la red mencionada   |    |
|  &ip address 'IPV4' 'MASK'  |  Asignamos la un host a nuestra router   |  Idealmente sera el gateway de esa seccion | 
|  &no shutdown   |  Enciende la interface  |   | 
|  &description TEXT   |  Agregamos una descripcion a la interfaz para ayudamemoria  |   |
|  &exit   | Salimos del modo interface   |   |


# Configuracion Telnet
| *Comando* | *Informacion* | *Tips* |
|:--------|:--------:|:--------:|
|  $hostname NAME   |    |   | 
|  $username NAME privilege 15 secret PASSWORD  | creamos un usuario y contrasena para el router  | Los privilegios son 0-15, 15 mayor  | 
|  $line vty 0 4  |  Entramos a configurar las líneas virtuales para Telnet  |  los numeros son cuantas sesiones pueden estar activas   |
|  &login local  |  Habilitamos el acceso con el usuario local configurado  |   |
|  &transport input telnet |    |    |
|  &exit  |  Salimos del modo de configuración de líneas virtuales  |   |
|  $*interface vlan1*   |  Modo interface de la VLAN seleccionada   |     |
|  &ip address IPV4   |  Anadimos un host en donde estara habiliado la IPV6   |    |
|  &description [STRING]   |  Row 2   |    |
|  &exit   |  Row 2   |    |
|  $ip default-gateway IPV4   |  Row 2   |    |
|||
| *EXTRA TIP* | BORRAR CONFIGURACION DE USUARIO  | *EXTRA TIP* |
|  $dir flash:/ | Listamos los archivos de configuracion de ese directorio | |
|  $delete flas:vlan | Borramos el archivo de la configuracion de la VLAN | |
|  $delete flas:config.test |  | |



# Configuracion Router IPV6 LINK LOCAL

| *Comando* | *Informacion* | *Tips* |
|:--------|:--------:|:--------:|
|  $hostname NAME  |  Cambia el nombre a nuestro router  |     |
|  $interface fa0/0   |  Entramos a configurar la interfaz de la red mencionada   |    |
|  &ipv6 address IPLOCAL link-local  |  Asignamos la un host a nuestra router   |  Idealmente sera el gateway de esa seccion | 
|  &no shutdown   |  Enciende la interface  |   | 
|  &description TEXT   |  Agregamos una descripcion a la interfaz para ayudamemoria  |   |
|  &exit   | Salimos del modo interface   |   |
