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

