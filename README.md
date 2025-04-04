# ExamenRedes1

# Parte 1: Conceptos y teoría


## Ejercicio 1: El mural de las 7 capas
![_- visual selection](https://github.com/user-attachments/assets/7f2eca05-5d6d-4a91-8793-eb16fc0841ed)

# 🌐 Modelo OSI - Descripción de Capas

El modelo OSI que es el que se pide en el enunciado, esta compuesto por las siguientes 7 capas:

---

## 🧱 1. Capa Física 

- **Función:** Transmite bits sin formato a través del medio físico.
- **Ejemplos:** Cables, señales eléctricas, conectores.
- **Dispositivos típicos:** Cables Ethernet, hubs, repetidores.

---

## 🧾 2. Capa de Enlace de Datos 

- **Función:** Agrupa los bits en tramas y controla el acceso al medio.
- **Ejemplos:** Ethernet, Wi-Fi.
- **Dispositivos típicos:** Switches, tarjetas de red.

---

## 🛰 3. Capa de Red 

- **Función:** Rutea los paquetes entre redes distintas.
- **Ejemplos:** IP (IPv4/IPv6), ICMP.
- **Dispositivos típicos:** Routers.

---

## 🚚 4. Capa de Transporte

- **Función:** Asegura la entrega confiable (o no) de los datos.
- **Ejemplos:** TCP (confiable), UDP (rápido pero sin garantía).
- **Funciones clave:** Control de flujo, segmentación, detección de errores.

---

## 🔄 5. Capa de Sesión

- **Función:** Administra las sesiones entre aplicaciones.
- **Ejemplos:** RPC, NetBIOS, sesiones TLS/SSL.
- **Extras:** Establecimiento, control y finalización de sesiones.

---

## 🧠 6. Capa de Presentación

- **Función:** Traduce, cifra y comprime los datos.
- **Ejemplos:** SSL/TLS, JPEG, MP3, ASCII.
- **Extras:** Interpreta formatos de datos entre sistemas diferentes.

---

## 🧑‍💻 7. Capa de Aplicación 

- **Función:** Proporciona servicios de red al usuario final.
- **Ejemplos:** HTTP, FTP, SMTP, DNS, POP3.
- **Extras:** Aquí viven los navegadores, apps, clientes de correo, etc.


## Ejercicio 2: Los dos pergaminos del mensajero
![_- visual selection (2)](https://github.com/user-attachments/assets/3c8496ac-4567-4368-a9a3-28076fabbd2c)

## 🔁 TCP (Transmission Control Protocol)

### ✅ Características:
- Conexión orientada.
- Entrega confiable de datos.
- Control de flujo y congestión.
- Reenvío en caso de pérdida.

### ➕ Ventajas:
- Alta fiabilidad.
- Entrega ordenada.
- Detección y corrección de errores.

### ➖ Desventajas:
- Más lento por la sobrecarga de control.
- Mayor uso de recursos.

---

## 💨 UDP (User Datagram Protocol)

### ✅ Características:
- No orientado a conexión.
- No garantiza entrega ni orden.
- Bajo overhead, mayor velocidad.
- No realiza reintentos.

### ➕ Ventajas:
- Rápido y eficiente.
- Ideal para tiempo real (juegos, video, VoIP).
- Menor consumo de recursos.

### ➖ Desventajas:
- Pérdida de paquetes posible.
- Sin mecanismos de recuperación o control.


## Ejercicio 3: El enigma de las subredes
![_- visual selection (3)](https://github.com/user-attachments/assets/e931ae07-dc3f-41fe-b97f-8cfe0a93daeb)


# 🧮 División de Subred: 192.168.50.0 para 4 gremios

## ✅ Datos iniciales:
- Dirección de red base: `192.168.50.0`
- Clase: **Clase C** (por defecto /24 → 255.255.255.0)
- Necesitamos: **4 subredes iguales**

---

## 📏 Paso 1: Determinar la nueva máscara

- Partimos de `/24` → 256 direcciones totales.
- Para crear **4 subredes**, necesitamos **2 bits extra** para subneteo (2² = 4).
- Resultado: `/26` (24 bits originales + 2 bits)  
- Máscara de subred: `255.255.255.192`

---

## 🧮 Paso 2: Calcular direcciones por subred

- Cada subred con `/26` → 2⁶ = **64 direcciones totales**
- Direcciones **utilizables por hosts**:  
  `64 - 2 = 62` (una para red, una para broadcast)

---

## 📦 Subredes resultantes:

| Subred # | Rango de IPs              | Dirección de red   | Broadcast         |
|----------|---------------------------|--------------------|-------------------|
| 1        | 192.168.50.1 – 192.168.50.62   | 192.168.50.0       | 192.168.50.63     |
| 2        | 192.168.50.65 – 192.168.50.126 | 192.168.50.64      | 192.168.50.127    |
| 3        | 192.168.50.129 – 192.168.50.190| 192.168.50.128     | 192.168.50.191    |
| 4        | 192.168.50.193 – 192.168.50.254| 192.168.50.192     | 192.168.50.255    |


## Ejercicio 4: La encrucijada de las rutas
![_- visual selection (4)](https://github.com/user-attachments/assets/ade2fc93-ed7e-4091-98fe-8c4e936c8d1b)


# 🧭 Enrutamiento en Redes: La Tabla y sus Caminos

## 📘 ¿Qué representa el tótem?
El tótem con flechas representa una **tabla de enrutamiento**, un componente esencial en los routers modernos para decidir **por dónde enviar los paquetes de datos**.

---

## 📋 ¿Qué es una Tabla de Enrutamiento?

Una **tabla de enrutamiento** es una base de datos que mantiene un router y que contiene rutas hacia diferentes redes o destinos. Cada entrada en la tabla indica:

- Dirección de destino (red o IP específica).
- Máscara de red (prefijo).
- Gateway o siguiente salto (next hop).
- Interfaz de salida.
- Métrica (costo o prioridad de la ruta).

Cuando llega un paquete, el router:
1. Consulta la tabla.
2. Busca la ruta más específica (longest match).
3. Reenvía el paquete por la interfaz correspondiente.

---

## 🗿 Flechas talladas vs. flechas móviles

| Tipo de flecha         | Enrutamiento Estático                     | Enrutamiento Dinámico                      |
|------------------------|--------------------------------------------|--------------------------------------------|
| **Flechas talladas**   | Configuradas manualmente                  | No cambian a menos que el admin las edite  |
| **Flechas móviles**    | Aprendidas automáticamente                | Se actualizan si cambia la topología       |

---

### 🧱 Enrutamiento Estático

- Rutas configuradas a mano por un administrador.
- Predecible y controlado.
- Ideal para redes pequeñas o con poca variación.

**Ventajas:**
- Menor uso de recursos.
- Más seguridad (menos vectores de ataque).

**Desventajas:**
- No se adapta automáticamente.
- Requiere mantenimiento manual.

---

### 🔄 Enrutamiento Dinámico

- El router aprende rutas a través de protocolos dinámicos.
- Se adapta a cambios en tiempo real.

**Protocolos comunes:** OSPF, RIP, EIGRP, BGP

**Ventajas:**
- Escalable y automatizado.
- Se recupera solo ante fallos.

**Desventajas:**
- Más complejo.
- Consumo adicional de CPU, memoria y ancho de banda.


## Ejercicio 5: El guardián de la máscara única
![_- visual selection (5)](https://github.com/user-attachments/assets/44e4d4df-991e-46de-b277-13004341bde8)


# 🎭 El Guardián de la Máscara: NAT (Network Address Translation)

## 🧠 ¿Qué técnica representa?
La leyenda describe el mecanismo de **NAT (Network Address Translation)**.

NAT permite que **múltiples dispositivos en una red privada compartan una única dirección IP pública** al comunicarse con el exterior.

---

## ⚙️ ¿Cómo funciona NAT?

1. **Salida (de la red local a Internet):**
   - Dispositivo local (ej. 192.168.0.10) envía un paquete.
   - El router reemplaza la IP privada con su propia IP pública.
   - Guarda una tabla interna que asocia:
     - IP privada + puerto de origen → IP pública + puerto traducido.

2. **Entrada (respuesta desde Internet):**
   - Llega una respuesta a la IP pública del router.
   - NAT consulta su tabla para saber a qué IP interna reenviar el paquete original.

---

## 🧾 Tipos de NAT comunes:

- **SNAT (Source NAT):** cambia la IP de origen (más común para salida a Internet).
- **DNAT (Destination NAT):** cambia la IP de destino (usado en port forwarding).

---

## ✅ Beneficios de usar NAT

1. **Ahorro de direcciones IP públicas:**
   - Múltiples dispositivos comparten una sola IP pública.
   - Fundamental ante la escasez de direcciones IPv4.

2. **Cierto nivel de seguridad:**
   - Los dispositivos internos no son accesibles directamente desde el exterior.
   - Oculta la topología interna de la red.


# Parte 2: Práctica con Cisco Packet Tracer (Documentación)

## Ejercicio 1: La ruta perdida entre dos reinos

## 🧱 1. Descripción General

Esta topología representa una red de interconexión entre dos ciudades (Ciudad A y Ciudad B), las cuales están unidas mediante una red **WAN con redundancia**, utilizando dos nubes (Cloud principal y Cloud secundaria) que simulan enlaces MPLS. Cada ciudad cuenta con su red LAN local con switches y PCs, y están conectadas a la red WAN mediante routers.

---

## 🖥️ 2. Componentes de la Red

| Dispositivo     | Ciudad     | Modelo           | Función                          |
|------------------|------------|------------------|----------------------------------|
| Router0          | Ciudad A   | Cisco 1941       | Enrutador local                  |
| Switch0          | Ciudad A   | Cisco 2960-24TT  | Conexión LAN                     |
| PC0, PC1         | Ciudad A   | PC-PT            | Dispositivos finales             |
| Router1          | Ciudad B   | Cisco 1941       | Enrutador local                  |
| Switch1          | Ciudad B   | Cisco 2960-24TT  | Conexión LAN                     |
| PC2, PC3         | Ciudad B   | PC-PT            | Dispositivos finales             |
| Cloud0           | Red WAN    | Cloud-PT         | Cloud principal (192.168.30.0)   |
| Cloud1           | Red WAN    | Cloud-PT         | Cloud secundaria (192.168.40.0)  |

---

## 🌐 3. Direccionamiento IP

### Ciudad A – Red 192.168.10.0/24

| Dispositivo | IP           |
|-------------|--------------|
| PC0         | 192.168.10.2 |
| PC1         | 192.168.10.3 |
| Router0 LAN | 192.168.10.1 |

### Ciudad B – Red 192.168.20.0/24

| Dispositivo | IP           |
|-------------|--------------|
| PC2         | 192.168.20.2 |
| PC3         | 192.168.20.3 |
| Router1 LAN | 192.168.20.1 |

### Enlaces WAN

| Enlace           | IP Router A | IP Router B | Subred          |
|------------------|-------------|-------------|------------------|
| Cloud Principal  | 192.168.30.2 | 192.168.30.1 | 192.168.30.0/30 |
| Cloud Secundaria | 192.168.40.2 | 192.168.40.1 | 192.168.40.0/30 |

*(X e Y representan los valores específicos asignados en los routers en esas interfaces)*

---

## 🔁 4. Conectividad WAN

- **Router0** está conectado a **Cloud0 (principal)** y **Cloud1 (secundaria)** mediante interfaces seriales.
- **Router1** está conectado de la misma forma, simulando enlaces redundantes en la red WAN.
- Se utilizan **Frame Relay** o rutas estáticas con **diferente distancia administrativa** para establecer conmutación por error (failover).
- Si un enlace falla, el tráfico se enruta automáticamente por el enlace alternativo.

---

## 🧭 5. Ruteo entre ciudades

Ambos routers están configurados para enrutar entre las LAN de Ciudad A (10.0.0.0/24) y Ciudad B (192.168.20.0/24), ya sea por el enlace principal o el secundario.

- Se puede implementar ruteo estático con respaldo:
  - Ruta principal vía Cloud0 (192.168.30.0)
  - Ruta secundaria vía Cloud1 (192.168.40.0)
- Alternativamente, se puede usar **ruteo dinámico** (EIGRP, OSPF) para detección automática de fallos.

---

## ✅ 6. Funcionamiento Esperado

- **Conectividad completa entre PCs de ambas ciudades**
- **Redundancia WAN activa**: si falla un enlace, la comunicación se mantiene por el secundario.
- **Enrutamiento funcional** entre LANs mediante los routers.
- **Pruebas exitosas de ping** entre:
  - PC0 ↔ PC2
  - PC1 ↔ PC3
  - Desde cualquier PC hacia cualquier router

---

## 🧪 7. Pruebas realizadas

| Prueba                          | Resultado Esperado         |
|----------------------------------|-----------------------------|
| Ping de PC0 a PC2               | Éxito (vía enlace principal) |
| Apagar Cloud0 y volver a hacer ping | Éxito (vía enlace secundario) |
| Ping de PC1 a 192.168.20.1      | Éxito                        |
| Ping entre routers              | Éxito por ambos enlaces      |

---


## Ejercicio 2: La ciudad de las redes aisladas

## 🧱 1. Descripción General

Esta topología representa una red LAN segmentada por VLANs, con múltiples PCs, un servidor DHCP centralizado y un router conectado mediante un enlace troncal (trunk) al switch principal. El objetivo es proporcionar conectividad entre diferentes VLANs y permitir asignación automática de direcciones IP mediante DHCP relay.

---

## 🖥️ 2. Componentes de la Red

| Dispositivo    | Modelo          | Función                                 |
|----------------|------------------|------------------------------------------|
| Router         | Cisco 1941       | Router-on-a-Stick (inter-VLAN routing)   |
| Switch         | Cisco 2960-24TT  | Segmentación de VLANs y enlace troncal   |
| Servidor       | Server-PT        | Servidor DHCP para múltiples VLANs       |
| PC0, PC1       | PC-PT            | Usuarios de la VLAN 10 (Ventas)          |
| PC2, PC3       | PC-PT            | Usuarios de la VLAN 20 (Finanzas)        |

---

## 🌐 3. VLANs Utilizadas

| VLAN ID | Nombre      | Dispositivos asignados | Rango IP         | Gateway        |
|---------|-------------|-------------------------|------------------|----------------|
| 10      | Arquitectos | PC0, PC1                | 192.168.10.0/24  | 192.168.10.1   |
| 20      | Escribas    | PC2, PC3                | 192.168.20.0/24  | 192.168.20.1   |
| 30      | Servidor    | Server0                 | 192.168.30.0/24  | 192.168.30.1   |

---

## 🔀 4. Enlace Trunk

El enlace entre el router y el switch es de tipo trunk, lo que permite transportar múltiples VLANs sobre una única interfaz física. Esto facilita la comunicación entre VLANs a través de subinterfaces en el router, actuando como gateway para cada VLAN.

---

## 📦 5. Servidor DHCP

El servidor se encuentra en la VLAN 30 y proporciona direcciones IP a dispositivos de las VLANs 10 y 20 mediante la funcionalidad de DHCP relay. Las solicitudes DHCP llegan al router, el cual las reenvía al servidor ubicado en otra VLAN.

### Configuración del servidor:
- IP del servidor: 192.168.30.10
- Máscara: 255.255.255.0
- Gateway: 192.168.30.1

### Rango de direcciones asignadas:

| VLAN | Rango DHCP           | Gateway         |
|------|-----------------------|------------------|
| 10   | 192.168.10.100+       | 192.168.10.1     |
| 20   | 192.168.20.100+       | 192.168.20.1     |

---

## ✅ 6. Funcionamiento Esperado

- Todos los PCs obtienen una dirección IP automáticamente mediante DHCP.
- El router enruta correctamente entre VLANs (inter-VLAN routing).
- La red está segmentada por VLANs para mejorar la organización y la seguridad.
- El servidor DHCP puede atender a todas las VLANs desde una sola ubicación (VLAN 30) gracias al reenvío de solicitudes.

---

## 🧪 7. Pruebas Realizadas

| Prueba                          | Resultado Esperado        |
|---------------------------------|----------------------------|
| Ping entre PC0 y PC1            | Éxito (misma VLAN)         |
| Ping entre PC2 y PC3            | Éxito (misma VLAN)         |
| Ping de PC0 a PC2               | Éxito (inter-VLAN routing) |
| Solicitud DHCP desde cualquier PC | Dirección IP válida recibida |
| Ping desde PCs al servidor      | Éxito                      |

---


