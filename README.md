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


---

## 🌐 Configuración de Router IPv6 (Link-Local)

| **Comando**                           | **Descripción**                                            | **Tips**                                               |
|---------------------------------------|------------------------------------------------------------|--------------------------------------------------------|
| `$hostname NOMBRE`                   | Cambia el nombre del router                                | Ayuda a identificar el dispositivo                     |
| `$interface fa0/0`                   | Entra a la interfaz FastEthernet 0/0                       | Puede variar según el modelo                           |
| `&ipv6 address IP_LOCAL link-local`  | Asigna una dirección IPv6 link-local a la interfaz         | Se usa para conectar routers directamente (IP privadas)|
| `&no shutdown`                       | Activa la interfaz                                         | Necesario para que funcione                            |
| `&description TEXTO`                | Agrega una descripción a la interfaz                       | Útil como ayuda memoria                                |
| `&exit`                              | Sale del modo de interfaz                                  | Regresa al modo `$`                                    |

---

## 🖧 Configuración de Switch y VLAN

| **Comando**                                 | **Descripción**                                               | **Tips**                                                  |
|---------------------------------------------|---------------------------------------------------------------|-----------------------------------------------------------|
| `#show mac-address-table`                  | Muestra la tabla CAM del switch                               | Verifica qué dispositivos están conectados               |
| `#show int gi0/1`                          | Muestra detalles de la interfaz gi0/1                         | Útil para ver la MAC del router conectado                |
| `#show vlan1`                              | Muestra información de la VLAN 1                              | Por defecto es la VLAN administrativa                    |
| `#configure terminal`                      | Entra al modo de configuración global                         | Necesario para modificar configuraciones del switch      |
| `$hostname SLAN2`                          | Cambia el nombre del switch                                   | Mejora la identificación del equipo                      |
| `$interface vlan 1`                        | Entra a la interfaz VLAN 1                                    | VLAN administrativa por defecto                          |
| `&ip address 192.168.116.3 255.255.255.128`| Asigna IP al switch para administración                       | Ejemplo: segunda IP utilizable de la red                 |
| `&description IP de admin del SW`          | Agrega una descripción a la interfaz                          | Ayuda a identificar la función de la VLAN                |
| `&no shutdown`                             | Activa la interfaz VLAN 1                                     | No siempre es necesario, depende del modelo              |
| `&exit`                                    | Sale del modo de interfaz                                     | Regresa al modo `$`                                      |
| `$ip default-gateway 192.168.116.126`      | Configura la puerta de enlace del switch                      | Necesaria para conexión fuera de la red local            |
| `#show ip interface brief`                | Muestra un resumen del estado de interfaces                   | Verifica si la VLAN 1 está activa y con IP asignada      |



## 📦 Configuración de DHCPv6 con Pool

| **Comando**                                 | **Descripción**                                                  | **Tips**                                                     |
|---------------------------------------------|------------------------------------------------------------------|--------------------------------------------------------------|
| `$ipv6 dhcp pool NOMBRE_POOL`              | Crea un pool DHCPv6 con el nombre especificado                   | Puedes usar un nombre representativo como `RED-LAN6`         |
| `&address prefix 2001:DB8:1::/64`           | Define el prefijo de red que se asignará a los clientes          | Asegúrate de que este prefijo sea válido y esté enrutado     |
| `&dns-server 2001:4860:4860::8888`          | Define un servidor DNS para los clientes                         | Puedes usar DNS público de Google IPv6                       |
| `&domain-name ejemplo.com`                 | Asigna un nombre de dominio a los clientes                       | Opcional pero útil                                           |
| `&exit`                                    | Sale del modo de configuración del pool                          |                                                              |
| `$interface fa0/0`                         | Entra a la interfaz donde se ofrecerá el servicio DHCPv6         | Debe ser una interfaz activa y conectada a la red LAN        |
| `&ipv6 address 2001:DB8:1::1/64`           | Asigna dirección IPv6 a la interfaz                              | Debe coincidir con el prefijo del pool                      |
| `&ipv6 dhcp server NOMBRE_POOL`            | Asocia el pool DHCPv6 a la interfaz                              | Usa el nombre que diste al pool                             |
| `&ipv6 nd other-config-flag`              | Indica que hay parámetros adicionales mediante DHCPv6            | Obligatorio si no estás usando SLAAC                        |
| `&no shutdown`                             | Activa la interfaz                                               |                                                              |
| `&exit`                                    | Sale del modo interfaz                                           |                                                              |

---
### 🔧 Activar y Configurar RIP v2
---

| **Comando**                     | **Descripción**                                              | **Tips**                                                   |
|----------------------------------|--------------------------------------------------------------|------------------------------------------------------------|
| `$router rip`                   | Inicia el proceso de configuración de RIP                   | Debes estar en modo de configuración global                |
| `&version 2`                    | Establece RIP versión 2 (más segura y compatible con VLSM)  | Obligatorio para evitar usar la versión antigua            |
| `&no auto-summary`             | Desactiva el resumen automático de rutas claseful           | Necesario cuando usas subredes                             |
| `&passive-interface [int/n/n]` | Evita enviar anuncios RIP por una interfaz específica       | Útil en interfaces de acceso hacia hosts (como VLANs)      |
| `&network [RED_LOCAL]`         | Incluye una red directamente conectada en el proceso RIP    | Debes usar la red **no la IP de la interfaz**              |
| `show ip protocols`         | Ver la tabla de protocolos de un router|           |

---

## 🧱 Creación y Configuración de VLAN en Switch

| **Comando**               | **Descripción**                                           | **Tips**                                             |
|---------------------------|-----------------------------------------------------------|------------------------------------------------------|
| `$vlan 10`               | Crea una VLAN con ID 10                                   | Puedes usar cualquier número del 2 al 4094           |
| `&name VENTAS`           | Asigna un nombre descriptivo a la VLAN                    | Opcional, pero útil para organización                |
| `&exit`                  | Sale de la configuración de la VLAN                       |                                                      |
| `$interface fa0/2`       | Entra a configurar una interfaz física                    | Reemplaza por el puerto que deseas configurar        |
| `&switchport mode access`| Configura la interfaz como puerto de acceso               | Requerido para asignar una VLAN                     |
| `&switchport access vlan 10`| Asocia la interfaz a la VLAN 10                         | Asegúrate que la VLAN ya exista                     |
| `&description PC de ventas`| Añade una descripción a la interfaz                     | Mejora la documentación                             |
| `&no shutdown`           | Activa la interfaz si está deshabilitada                  |                                                      |
| `&exit`                  | Sale del modo de interfaz                                 |                                                      |
| `#show vlan brief`       | Verifica la configuración de VLANs                        | Muestra qué puertos están asignados a qué VLAN      |


## 🔁 Configurar un Switch Capa 3 como Router

Un **Switch Capa 3 (multicapa)** permite enrutar entre VLANs sin necesidad de un router externo. Para esto se habilita el enrutamiento IP y se usan interfaces VLAN como puertas de enlace.

| **Comando**             | **Descripción**                              | **Tips**                                     |
|-------------------------|----------------------------------------------|----------------------------------------------|
| `#configure terminal`   | Entra al modo de configuración global        |                                               |
| `$ip routing`           | Habilita el enrutamiento entre interfaces    | Esencial para inter-VLAN routing              |
| `$vlan 10`                         | Crea la VLAN 10                                     |                                                  |
| `&name VENTAS`                     | Nombra la VLAN 10                                   |                                                  |
| `&exit`                            | Sale del modo VLAN                                  |                                                  |
| `$interface vlan 10`              | Entra a la interfaz VLAN 10                         | Estas interfaces actuarán como gateways         |
| `&ip address 192.168.10.1 255.255.255.0` | Asigna IP a la interfaz VLAN                   | Será el gateway para la red de esa VLAN         |
| `&no shutdown`                     | Activa la interfaz                                  |                                                  |
| `&exit`                            | Sale del modo interfaz                              |                                                  |
| `$interface vlan 20`              | Repetir para otra VLAN (ej. VLAN 20)                |                                                  |
| `&ip address 192.168.20.1 255.255.255.0` |                                                  |                                                  |
| `&no shutdown`                     |                                                    |                                                  |
| `&exit`                            |                                                    |                                                  |
| `$interface fa0/2`                 | Entra al puerto que va a la PC                      | Cambia según el puerto usado                 |
| `&switchport mode access`          | Configura como puerto de acceso                     |                                              |
| `&switchport access vlan 10`       | Asocia el puerto a la VLAN 10                       |                                              |
| `&description PC de Ventas`        | Añade descripción                                   |                                              |
| `&no shutdown`                     | Activa el puerto si está apagado                    |                                              |
| `&exit`                            | Repite para cada puerto y VLAN correspondiente      |                                              |
| `#show vlan brief`       | Verifica las VLANs existentes y puertos asignados     |
| `#show ip interface brief`| Muestra las interfaces VLAN y sus IPs configuradas    |
| `#ping 192.168.20.1`     | Prueba de conectividad entre VLANs                    |




switchport trunk allowed vlan 100,200,300
 switchport mode trunk
 switchport nonegotiate

interface FastEthernet0/23
!
interface FastEthernet0/24
 switchport trunk allowed vlan 100,200,300
 switchport mode trunk
 switchport nonegotiate
spanning-tree vlan 100,200,300 priority 24576  //swt3



 //juniper
set interfaces ge-0/0/2 unit 0 family ethernet-switching vlan members <nombre o id vlan> //asocia interfaz a una vlan
		set interfaces ge0/0/0 unit 0 family ethernet-switching interface-mode access/trunk // define el modo de la interfaz




!
ip dhcp pool DATOS
 network 172.18.100.0 255.255.254.0
 default-router 172.18.101.254
 dns-server 8.8.8.8
ip dhcp pool SECRETARIA
 network 172.18.96.0 255.255.252.0
 default-router 172.18.99.254
 dns-server 8.8.8.8
ip dhcp pool RECTORADO
 network 172.18.102.0 255.255.255.0
 default-router 172.18.102.254
 dns-server 8.8.8.8
!
