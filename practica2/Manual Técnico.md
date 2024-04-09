# Manual técnico

## Configuración de Dispositivos

### Router R2

El Router R2 se configura de la siguiente manera:

1. **Configuración básica:**
   ```bash
   enable
   configure terminal
   no ip domain-lookup
   hostname R2
   ```

2. **Interfaces:**
   - Interfaz f0/1:
     ```bash
     interface f0/1
     ip add 132.168.0.2 255.255.255.0
     standby 11 ip 132.168.0.1
     standby 11 priority 150
     standby 11 preempt
     no shutdown
     ```
   - Interfaz f0/0:
     ```bash
     interface f0/0
     ip add 132.168.1.1 255.255.255.248
     no shutdown
     ```

### Router R3

El Router R3 se configura de la siguiente manera:

1. **Configuración básica:**
   ```bash
   enable
   configure terminal
   no ip domain-lookup
   hostname R3
   ```

2. **Interfaces:**
   - Interfaz f0/1:
     ```bash
     int f0/1
     ip add 132.168.0.3 255.255.255.0
     no shutdown
     ```
   - Interfaz f0/0:
     ```bash
     int f0/0
     ip add 132.168.2.1 255.255.255.248
     no shutdown
     ```

### Router R5

El Router R5 se configura de la siguiente manera:

1. **Configuración básica:**
   ```bash
   enable
   configure terminal
   no ip domain-lookup
   hostname R5
   ```

2. **Interfaces:**
   - Interfaz f0/1:
     ```bash
     int f0/1
     ip add 132.178.0.2 255.255.255.0
     standby 12 ip 132.178.0.1
     standby 12 priority 150
     standby 12 preempt
     no shutdown
     ```
   - Interfaz f0/0:
     ```bash
     int f0/0
     ip add 132.178.1.2 255.255.255.248
     no shutdown
     ```

### Router R6

El Router R6 se configura de la siguiente manera:

1. **Configuración básica:**
   ```bash
   enable
   configure terminal
   no ip domain-lookup
   hostname R6
   ```

2. **Interfaces:**
   - Interfaz f0/1:
     ```bash
     int f0/1
     ip add 132.178.0.3 255.255.255.0
     no shutdown
     ```
   - Interfaz f0/0:
     ```bash
     int f0/0
     ip add 132.178.2.2 255.255.255.248
     no shutdown
     ```

### Router R1

El Router R1 se configura de la siguiente manera:

1. **Configuración básica:**
   ```bash
   enable
   configure terminal
   no ip domain-lookup
   hostname R1
   ```

2. **Interfaces:**
   - Interfaz se0/0:
     ```bash
     int se0/0
     ip add 10.0.0.1 255.255.255.252
     no shutdown
     ```
   - Interfaz f0/0:
     ```bash
     int f0/0
     ip add 132.168.1.2 255.255.255.248
     no shutdown
     ```
   - Interfaz f0/1:
     ```bash
     int f0/1
     ip add 132.168.2.2 255.255.255.248
     no shutdown
     ```

### Router R4

El Router R4 se configura de la siguiente manera:

1. **Configuración básica:**
   ```bash
   enable
   configure terminal
   no ip domain-lookup
   hostname R4
   ```

2. **Interfaces:**
   - Interfaz se0/0:
     ```bash
     interface se0/0
     ip add 10.0.0.2 255.255.255.252
     no shutdown
     ```
   - Interfaz f0/0:
     ```bash
     interface f0/0
     ip add 132.178.1.1 255.255.255.248
     no shutdown
     ```
   - Interfaz f0/1:
     ```bash
     interface f0/1
     ip add 132.178.2.1 255.255.255.248
     no shutdown
     ```

## Configuración de Rutas Estáticas

Para establecer la conectividad entre las redes, se deben configurar rutas estáticas en cada router. Por ejemplo, en el Router R1:

```bash
enable
conf t
ip route 132.168.0.0 255.255.255.0 132.168.1.1
ip route 132.168.0.0 255.255.255.0 132.168.2.1
ip route 132.168.1.0 255.255.255.248 132.168.1.1
ip route 132.168.2.0 255.255.255.248 132.168.2.1
ip route 10.0.0.0 255.255.255.252 10.0.0.2
ip route 132.178.1.0 255.255.255.248 10.0.0.2
ip route 132.178.2.0 255.255.255.248 10.0.0.2
ip route 132.178.0.0 255.255.255.0 10.0.0.2
do w
```

Repite este proceso en todos los routers para establecer las rutas estáticas necesarias.

## Configuración de Switches

Para establecer enlaces de agregación de enlaces en los switches:

### Switch 0

```bash
enable
configure terminal
int range fa0/2-3
channel-protocol pagp
channel-group 1 mode desirable
do w
```

### Switch 1

```bash
enable
configure terminal
int range fa0/1-2
channel-protocol pagp
channel-group 1 mode desirable
do w
```

### Switch 2

```bash
enable
configure terminal
int range fa0/4-5
channel-protocol lacp
channel-group 1 mode active
do w
```



### Switch 3

```bash
enable
configure terminal
int range fa0/4-5
channel-protocol lacp
channel-group 1 mode active
do w
```

## Configuración de Direcciones IP

Es necesario asignar direcciones IP estáticas a cada dispositivo para establecer la conectividad. Por ejemplo:

- IP: 132.168.0.4 / Máscara: 255.255.255.0 / Puerta de enlace: 132.168.0.1 (para Router R2)
- IP: 132.178.0.4 / Máscara: 255.255.255.0 / Puerta de enlace: 132.178.0.1 (para Router R5)

---
