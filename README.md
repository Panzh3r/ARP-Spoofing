# ARP-Spoofing
Laboratorio: Simulación de Ataque ARP Spoofing

## 🎯Objetivo
Comprender cómo funciona un ataque de ARP Spoofing y observar sus efectos en una red local, utilizando herramientas básicas de Kali Linux.

## 📋Requisitos
- Kali Linux (máquina atacante)
- Windows (máquina víctima)
- Ambas máquinas conectadas a la misma red local (puede ser una red virtual como en VirtualBox o VMware)

## 🔧Herramientas:
  - arpspoof (incluida en Kali)
  - Wireshark (opcional, para análisis de tráfico)
  - ping o navegación web desde Windows

## ☑ Actividades a realizar en el Laboratorio
### 1.Configuración de red
Verifica que ambas máquinas estén en la misma red:
- En Kali: `ip a`
- En Windows: `ipconfig`

Anota las IPs de:
- Kali Linux *(ej. 192.168.62.140)*
- Windows *(ej. 192.168.62.144)*
- Gateway de la Red *(ej. 192.168.62.2)*

### 2.Habilitar el reenvío de paquetes en Kali
En Kali, ejecuta el siguiente comando para habilitar el reenvío de paquetes:

`echo 1 > /proc/sys/net/ipv4/ip_forward`

### 3.Ejecutar ARP Spoofing desde Kali
Abre dos terminales en Kali:
- Terminal 1: Enviar paquetes falsos al equipo Windows:

`arpspoof -i eth0 -t 192.168.62.144 192.168.62.2`

- Terminal 2: Enviar paquetes falsos al router:

`arpspoof -i eth0 -t 192.168.62.2 192.168.62.144`

Reemplaza `eth0` con el nombre correcto de tu interfaz de red si es diferente (puedes verificarlo con `ip a`).

### 4. Observar el tráfico (opcional)
Abre Wireshark en Kali y filtra por `ip.addr == 192.168.62.144`

Desde Windows, navega por internet o haz `ping` a una página.

Observa cómo Kali intercepta el tráfico.

### 5.Detener el ataque
Detén los procesos de `arpspoof` con `Ctrl+C`

Desactiva el reenvío de paquetes:

`echo 0 > /proc/sys/net/ipv4/ip_forward`

## Preguntas de analisis
1. ¿Qué observaste en Wireshark durante el ataque?
2. ¿Cómo podrías proteger una red contra este tipo de ataques?

