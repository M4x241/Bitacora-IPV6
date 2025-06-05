# 📘 Bitácora de Comandos – SIS 252: Redes 2

Bitácora de comandos utilizados en clase.  
Convenciones para indicar modos:
- `#`: modo privilegiado (enable)
- `$`: modo de configuración global (`configure terminal`)
- `&`: modo de configuración de interfaz (`interface`, `line vty`, `vlan`, etc.)

---

## 🔧 Comandos Básicos

| **Comando**             | **Descripción**                                | **Tips**                            |
|-------------------------|------------------------------------------------|-------------------------------------|
| `#enable`               | Entra al modo privilegiado                     | Necesario antes de hacer cambios    |
| `$configure terminal`   | Entra al modo de configuración global          | Permite configurar el equipo        |

---

## 🌐 Configuración de Router IPv4

| **Comando**                 | **Descripción**                                      | **Tips**                                     |
|-----------------------------|------------------------------------------------------|----------------------------------------------|
| `$hostname NOMBRE`          | Cambia el nombre del dispositivo                     | Útil para identificar el router              |
| `$interface fa0/0`          | Entra a la interfaz FastEthernet 0/0                 | Usa `GigabitEthernet` si aplica              |
| `&ip address IP MASK`       | Asigna IP y máscara a la interfaz                    | Generalmente el gateway de esa red           |
| `&no shutdown`              | Activa la interfaz                                   | Sin esto, la interfaz queda apagada          |
| `&description TEXTO`        | Agrega una descripción a la interfaz                 | Mejora la documentación del proyecto         |
| `&exit`                     | Sale del modo de interfaz                            | Retorna al modo `$`                          |

---

## 📞 Configuración de Telnet

| **Comando**                                        | **Descripción**                                                  | **Tips**                                           |
|----------------------------------------------------|------------------------------------------------------------------|----------------------------------------------------|
| `$hostname NOMBRE`                                | Cambia el nombre del dispositivo                                 |                                                     |
| `$username USUARIO privilege 15 secret PASSWORD`   | Crea un usuario con contraseña y nivel de privilegio             | Privilegio 15 = acceso completo                    |
| `$line vty 0 4`                                    | Entra a configuración de líneas virtuales para acceso Telnet     | Hasta 5 sesiones remotas simultáneas              |
| `&login local`                                     | Usa la base local de usuarios                                    |                                                     |
| `&transport input telnet`                          | Habilita el protocolo Telnet                                     |                                                     |
| `&exit`                                            | Sale del modo de configuración de línea                          |                                                     |
| `$interface vlan1`                                 | Entra a la interfaz VLAN 1                                       | VLAN de administración predeterminada             |
| `&ip address IP MASK`                              | Asigna una IP a la VLAN                                          | Permite el acceso remoto al switch/router         |
| `&description TEXTO`                               | Agrega una descripción a la interfaz VLAN                        |                                                     |
| `&exit`                                            | Sale del modo de interfaz                                        |                                                     |
| `$ip default-gateway IP`                           | Define la puerta de enlace por defecto                           | Necesario para conectividad externa               |

---

## 🧹 Limpieza de Configuración

| **Comando**                 | **Descripción**                                      | **Tips**                                    |
|-----------------------------|------------------------------------------------------|---------------------------------------------|
| `#dir flash:/`              | Lista los archivos en la memoria flash               | Revisa antes de borrar archivos             |
| `#delete flash:vlan.dat`    | Borra la configuración de VLAN almacenada            | Se regenera tras reiniciar el switch        |
| `#delete flash:config.text` | Elimina la configuración guardada                    | El router arranca sin configuración previa  |


# Configuracion Router IPV6 LINK LOCAL

| *Comando* | *Informacion* | *Tips* |
|:--------|:--------:|:--------:|
|  $hostname NAME  |  Cambia el nombre a nuestro router  |     |
|  $interface fa0/0   |  Entramos a configurar la interfaz de la red mencionada   |    |
|  &ipv6 address IPLOCAL link-local  |  Asignamos la un host a nuestra router   |  Se usa para conectar dos routers, IP's privadas| 
|  &no shutdown   |  Enciende la interface  |   | 
|  &description TEXT   |  Agregamos una descripcion a la interfaz para ayudamemoria  |   |
|  &exit   | Salimos del modo interface   |   |


# Configuracion Switch
# Configuración de Switch y VLAN

| *Comando* | *Información* | *Tips* |
|:----------|:--------------|:-------|
| `show mac-address-table` | Muestra la tabla CAM del switch | Útil para verificar las direcciones MAC conectadas |
| `show int gi0/1` | Vemos la MAC del router para verificar su pertenencia | Identifica la conexión al router |
| `show vlan1` | Muestra la configuración de la VLAN 1 | Por defecto, VLAN 1 está habilitada |
| `configure terminal` | Entra al modo de configuración global | Necesario para realizar cambios en el switch |
| `host SLAN2` | Cambia el nombre del switch | Ayuda a identificar el dispositivo |
| `interface vlan 1` | Configura la interfaz VLAN 1 | VLAN por defecto para administración |
| `ip address 192.168.116.3 255.255.255.128` | Asigna una IP al switch para administración | Segunda IP utilizable de la red |
| `description IP de admin del SW` | Agrega una descripción a la interfaz | Facilita la identificación de la interfaz |
| `no shutdown` | Activa la interfaz VLAN 1 | No siempre necesario, ya que VLAN 1 está activa por defecto |
| `exit` | Sale del modo de configuración actual | Útil para volver al nivel anterior |
| `ip default-gateway 192.168.116.126` | Configura el gateway predeterminado del switch | Necesario para la conectividad fuera de la red local |
| `show ip interface brief` | Verifica el estado de las interfaces | Revisa el estado y configuración de VLAN 1 |
