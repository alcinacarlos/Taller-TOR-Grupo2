# PROXYCHAINS + TOR: Guía Práctica para Taller de Anonimato en Red

## Índice
1. [Introducción](#introducción)
2. [¿Qué es Proxychains + Tor?](#qué-es-proxychains--tor)
3. [Instalación y Configuración](#instalación-y-configuración)
4. [Casos de Uso Profesionales](#casos-de-uso-profesionales)
5. [Demo para Taller](#demo-para-taller)
6. [VPN vs Proxychains + Tor](#vpn-vs-proxychains--tor)
7. [Limitaciones](#limitaciones)
8. [Ética Legal](#ética-legal)

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

En Kali, systemctl no funciona bien para Tor. Usamos daemon:

```bash
sudo killall tor 2>/dev/null  # Matar procesos viejos
sudo tor &                     # Arrancar en background
sleep 5                        # Esperar conexión
sudo ss -tlnp | grep 9050      # Verificar puerto abierto
```

**Salida esperada**:
```
tcp  0  0 127.0.0.1:9050  0.0.0.0:*  LISTEN
```

### Paso 3: Configurar Proxychains (VERSIÓN CORRECTA)

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

## Demo para Taller (90 minutos)

### Estructura

**0-10 min**: Intro + contexto legal  
**10-30 min**: Instalación y configuración en vivo  
**30-55 min**: Demostración práctica  
**55-90 min**: CTF competitivo  

### Demo Paso a Paso

#### **Paso 1: IP Real (rastreable)**
```bash
echo "=== Tu IP REAL ==="
curl -s icanhazip.com
# Salida: 150.10.15.102
# 📍 Jerez, España (fácil de rastrear)
```

#### **Paso 2: IP con Proxychains + Tor**
```bash
echo "=== Tu IP CON PROXYCHAINS + TOR ==="
proxychains curl -s icanhazip.com
# Salida: 45.84.107.222
# 📍 Alemania (IP del nodo Tor, NO tu IP real)
```

#### **Paso 3: Comparación Visual**
```
SIN PROXYCHAINS:
├─ IP: 150.10.15.102
├─ Ubicación: Jerez, España
├─ Rastreable: ✅ SÍ (fácilmente)
└─ Riesgo: 🔴 ALTO

CON PROXYCHAINS + TOR:
├─ IP: 45.84.107.222
├─ Ubicación: Alemania (nodo salida)
├─ Rastreable: ❌ NO (imposible)
└─ Riesgo: 🟢 BAJO
```

#### **Paso 4: NMAP Anónimo**
```bash
proxychains nmap -p 80,443 8.8.8.8
# [proxychains] Dynamic chain ... 127.0.0.1:9050 ... OK
# PORT    STATE SERVICE
# 80/tcp  open  http
# 443/tcp open  https

echo "Admin de Google ve: 45.84.107.222 (Alemania)"
echo "Admin de Google NO ve: 150.10.15.102 (Jerez)"
```

#### **Paso 5: Rotación IP (Hosts Diferentes)**
```bash
echo "Intento 1: icanhazip.com"
proxychains curl -s icanhazip.com
# 45.84.107.222

echo "Intento 2: httpbin.org"
proxychains curl -s httpbin.org/ip
# 89.234.157.12 (posiblemente diferente - nuevo host)

echo "Intento 3: ifconfig.me"
proxychains curl -s ifconfig.me
# 203.145.67.89 (posiblemente diferente - nuevo host)
```

**Nota**: Con 1 solo Tor, la IP puede permanecer igual durante ~10 minutos (Tor mantiene circuito abierto). Cambiar de host ayuda a simular atacantes distribuidos.

---

## VPN vs Proxychains + Tor

### La Diferencia CLAVE

| Aspecto | **VPN** | **Proxychains + Tor** |
|---------|---------|----------------------|
| **Número de IPs** | 1 fija | ∞ miles (potencialmente) |
| **Rotación** | Manual (reconectar) | Automática (circuito Tor cada 10 min) |
| **Velocidad** | Rápida ⚡ | Lenta 🐌 (2-30s) |
| **Anonimato** | Medio (1 túnel) | Alto (3+ capas cifrado) |
| **CLI Universal** | Configurable | ✅ Cualquier app TCP |
| **Bloqueo** | Rápido (IP fija) | Difícil (IPs infinitas) |

### Demo Comparativa

```
ESCENARIO: Pentesting a servidor web del cliente

❌ CON VPN:
firewall.log:
10:00: 123.45.67.89 → target.com:443 SYN
10:01: 123.45.67.89 → target.com:80 SYN  
10:02: 123.45.67.89 → target.com:22 SYN
→ Cliente: "¿Una sola IP? Fácil de bloquear"
→ IDS: Bloqueada después de 5 minutos

✅ CON PROXYCHAINS + TOR:
firewall.log:
10:00: 45.84.107.222(DE) → target.com:443 SYN
10:01: 89.234.157.12(FR) → target.com:80 SYN
10:02: 203.145.67.89(NL) → target.com:22 SYN
→ Cliente: "¡Ataque distribuido desde 3 países!"
→ IDS: Imposible correlacionar (IP diferente cada vez)
```

### ¿Cuándo Usar Cada Uno?

```
FASE 1: Reconnaissance Rápido → VPN
  • Masscan 10.0.0.0/24 --rate=10000 (velocidad)
  • Full port scan (rápido)

FASE 2: Enumeración Detallada → Proxychains + Tor
  • nmap -sC -sV con anonimato
  • Gobuster, Nuclei, etc.
  • OPSEC crítica

FASE 3: Explotación → Pivoting Interno
  • SSH desde bastion (comprometido)
  • Nmap interno desde objetivo
```

### Ventaja Única de Proxychains + Tor

```
"Imposible de bloquear"

VPN:
IP → 123.45.67.89 → BLOQUEADA (5 min)

Tor:
IP1 → 45.84.107.222 (DE)
IP2 → 89.234.157.12 (FR)
IP3 → 203.145.67.89 (NL)
IP4 → 192.42.116.194 (SE)
→ IMPOSIBLE BLOQUEAR (infinitas IPs)
```

---

## Scripts Útiles

### Script 1: Setup Completo
```bash
#!/bin/bash
sudo apt install -y tor proxychains
sudo killall tor 2>/dev/null
sudo tor &
sleep 5
sudo sed -i 's/^#dynamic_chain/dynamic_chain/' /etc/proxychains.conf
sudo sed -i 's/^random_chain/#random_chain/' /etc/proxychains.conf
sudo sed -i 's/^#proxy_dns/proxy_dns/' /etc/proxychains.conf
echo "✅ Setup completado. Prueba: proxychains curl -s icanhazip.com"
```

### Script 2: Demo Taller
```bash
#!/bin/bash
echo "🎭 DEMO: Proxychains + Tor"
echo "=== IP Real (rastreable) ==="
curl -s icanhazip.com
echo ""
echo "=== IP Tor (anónima) ==="
proxychains curl -s icanhazip.com 2>/dev/null
echo ""
echo "=== Escaneo anónimo ==="
proxychains nmap -p 80,443 8.8.8.8 2>/dev/null | grep -E "PORT|open"
```

### Script 3: Validación Rápida
```bash
#!/bin/bash
echo "[1] Tor corriendo:"
sudo ss -tlnp 2>/dev/null | grep 9050

echo "[2] Proxychains config:"
grep "^dynamic_chain" /etc/proxychains.conf && echo "✅ dynamic_chain OK" || echo "❌ ERROR"

echo "[3] IP Test:"
echo "Real: $(curl -s icanhazip.com)"
echo "Tor: $(proxychains curl -s icanhazip.com 2>/dev/null)"
```

---

**Documento preparado para taller de ciberseguridad**  
*Enero 2026 - Cadiz, España*
