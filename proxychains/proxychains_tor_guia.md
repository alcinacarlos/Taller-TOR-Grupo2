# PROXYCHAINS + TOR: Guía Práctica para Taller de Anonimato en Red

## Índice
1. [Introducción](#introducción)
2. [¿Qué es Proxychains + Tor?](#qué-es-proxychains--tor)
3. [Instalación y Configuración](#instalación-y-configuración)
4. [Casos de Uso Profesionales](#casos-de-uso-profesionales)


---

## Introducción

Este documento resume la **instalación, configuración y uso de proxychains + Tor** para conseguir **anonimato en la línea de comandos (CLI)** en Kali Linux. Es especialmente útil para **pentesters y profesionales de ciberseguridad** que necesitan OPSEC (Operational Security) en reconocimiento y escaneo.

**Diferencia clave**: Tor Browser es para navegación web. Proxychains + Tor es para **herramientas de línea de comandos** (nmap, ssh, curl, wget, etc.), permitiendo que cualquier aplicación TCP se enrute anónimamente.

---

## ¿Qué es Proxychains + Tor?

### Proxychains

Proxychains es una herramienta que **intercepta conexiones TCP de cualquier programa** (nmap, curl, ssh, etc.) y las redirige a través de un proxy SOCKS5 (en nuestro caso, Tor en 127.0.0.1:9050).

```
Aplicación CLI (nmap, curl, ssh)
    ↓
Proxychains (intercepta)
    ↓
Proxy SOCKS5 (127.0.0.1:9050 = Tor local)
    ↓
Red Tor
    ↓
Servidor objetivo
```

### Tor

Tor (The Onion Router) es una red de anonimato que enruta tráfico a través de **múltiples nodos en distintos países** con **cifrado en capas**:

```
Tu IP real (España)
    ↓ CIFRADO
Nodo Entrada (Guard) → sabe quién eres, no el destino
    ↓ CIFRADO
Nodo Intermedio → no sabe quién eres ni dónde vas
    ↓ CIFRADO
Nodo Salida (Exit) → sabe el destino, no quién eres
    ↓
Servidor objetivo (ve solo: 45.84.107.222 Alemania, NO tu IP)
```

### Combo Proxychains + Tor

Usar ambos permite:
- Enrutar **cualquier herramienta CLI** por Tor
- Máximo anonimato para pentesting autorizado
- OPSEC profesional

---

## Instalación y Configuración

### Paso 1: Instalación (2 comandos)

```bash
sudo apt update
sudo apt install -y tor proxychains
```

### Paso 2: Arrancar Tor (Kali)

```bash
sudo systemctl start tor
sudo ss -tlnp | grep 9050      # Verificar puerto abierto
```

**Salida esperada**:
```
tcp  0  0 127.0.0.1:9050  0.0.0.0:*  LISTEN
```

### Paso 3: Configurar Proxychains 

```bash
sudo nano /etc/proxychains.conf
```

**Dejar SOLO esto**:

```bash
# MODO (solo dynamic_chain activo)
dynamic_chain
#strict_chain
#random_chain

# DNS protection
proxy_dns

# Timeouts
tcp_read_time_out 15000
tcp_connect_time_out 8000

# ProxyList - SOLO UN PROXY
[ProxyList]
socks5  127.0.0.1 9050
```

**Puntos clave**:
- `dynamic_chain` = flexible y estable (recomendado)
- `proxy_dns` = anti-fuga DNS
- Solo **9050** en ProxyList (no 9051 ni 9052 - causaban timeouts)

Guardar: `Ctrl+O`, `Enter`, `Ctrl+X`

### Paso 4: Verificación

```bash
# IP sin Tor
curl -s icanhazip.com
# 150.10.15.102 (tu IP real)

# IP con Tor
proxychains curl -s icanhazip.com
# 45.84.107.222 (IP Tor diferente)
```

Si son diferentes: **✅ FUNCIONA**

---

## Casos de Uso Profesionales

### 1. Reconnaissance Anónimo
```bash
# Enumeración DNS
proxychains dnsenum -f objetivo.com

# Escaneo de puertos
proxychains nmap -sC -sV -T2 -p- objetivo.com

# Descubrimiento de subdominios
proxychains subfinder -d objetivo.com
```

### 2. Fingerprinting y Banner Grabbing
```bash
proxychains nmap -sC -sV -O objetivo.com
proxychains nc objetivo.com 80
proxychains nc objetivo.com 22
```

### 3. Transferencia de Archivos
```bash
proxychains wget http://objetivo.com/payload.exe
proxychains scp archivo.pdf admin@bastion:/tmp/
```

### 4. SSH y Pivoting
```bash
proxychains ssh pentester@bastion-server.com
proxychains ssh -R 8080:localhost:4444 user@target
```

### 5. OSINT y Web Scraping
```bash
proxychains gobuster dir -u http://target.com -w wordlist.txt
proxychains python3 scraper.py
proxychains nuclei -u urls.txt
```

---

*Enero 2026 - Cadiz, España*
