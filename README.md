# El lado invisible de internet: Red TOR, anonimato y rastros digitales

**Autores:**
Pablo González · Carlos Alcina · David Jimenez · Luis Carlos Romero

---

## Taller de TOR

Este taller introduce los conceptos fundamentales de **privacidad, anonimato y rastros digitales**, con un enfoque práctico en el uso de **Tor**, **Proxychains** y **Tails**, combinando teoría y práctica realista.

---

## TEORÍA

### ¿Privacidad vs Anonimato?

* **Privacidad**: protege el contenido de lo que compartes (mensajes, fotos, datos), usando HTTPS o cifrado.
* **Anonimato**: oculta quién eres (IP, identidad, ubicación).

Tor prioriza el **anonimato**, no el cifrado extremo a extremo del contenido.

---

### Anonimato básico y extensiones de navegador

El anonimato básico se apoya en extensiones como:

* uBlock Origin
* NoScript
* CanvasBlocker

Aun así, puede degradarse fácilmente por **fingerprinting** y por la información que maneja el **ISP**.

#### Threat Model

Un *Threat Model* identifica activos, atacantes, vectores y riesgos para definir mitigaciones antes de incidentes.

#### ISP

Proveedor de servicios de Internet que puede observar metadatos de conexión.

---

### Identificación del usuario

* **Canvas Fingerprinting**
* Idioma del sistema
* Zona horaria
* Tamaño de ventana (empeora el anonimato)

El *Canvas Fingerprinting* genera una huella casi única (90–99%) combinando GPU, drivers, fuentes y hardware.

---

### Comparación con extensiones de privacidad

Prueba práctica en:
[https://coveryourtracks.eff.org/](https://coveryourtracks.eff.org/)

---

### ¿Qué es TOR?

**Tor (The Onion Router)** es una red diseñada para ocultar quién se comunica con quién.

Objetivos:

* Evitar correlación origen–destino
* Ocultar IP real
* Proteger metadatos

Tor no cifra Internet: **oculta rutas**.

Cada circuito suele usar **3 nodos** y cambia periódicamente.

---

### TOR vs VPN

| Categoría  | TOR                  | VPN                     |
| ---------- | -------------------- | ----------------------- |
| Mecanismo  | 3+ nodos voluntarios | Servidor central        |
| Anonimato  | Excelente            | Bueno                   |
| Privacidad | Browser only         | Todo el sistema         |
| Velocidad  | Lenta                | Alta                    |
| Acceso geo | Aleatorio            | Controlable             |
| Coste      | Gratis               | 3–10€/mes               |
| Uso ideal  | Dark Web, censura    | Streaming, WiFi público |

---

### Cómo funciona TOR

Tor usa **Onion Routing**:

* Cifrado en capas
* Cada nodo conoce solo el salto anterior y siguiente
* Los circuitos cambian cada ~10 minutos

#### Tipos de nodos

| Nodo       | Qué hace        | Riesgo   |
| ---------- | --------------- | -------- |
| Guard      | Primer salto    | Bajo     |
| Relay      | Intermedio      | Muy bajo |
| Exit       | Sale a Internet | Alto     |
| Bridge     | Entrada oculta  | Bajo     |
| Directorio | Lista nodos     | Medio    |

Referencias:

* dan.me.uk/tornodes
* metrics.torproject.org

---

### Chat anónimo (OpenPGP + Tor)

Práctica de mensajería cifrada:

* El chat solo transporta texto
* El contenido se cifra previamente
* Solo el receptor puede descifrarlo

**Buenas prácticas:**

* No compartir claves privadas
* Verificar huellas digitales
* Firmar mensajes

---

### ¿Quién usa TOR y por qué?

* Periodistas y activistas
* Usuarios preocupados por privacidad
* Investigadores TI
* Fuerzas del orden
* Servicios .onion

Motivos: censura, privacidad frente a ISPs y Big Tech.

---

### BRIDGES

Permiten acceder a Tor cuando está bloqueado.

| Tipo      | Uso                   |
| --------- | --------------------- |
| Estándar  | Bloqueos simples      |
| obfs4     | Censura avanzada      |
| meek      | DPI extremo           |
| Snowflake | Anti-bloqueo dinámico |

---

### Qué protege TOR

Protege identidad y ubicación, **no comportamientos inseguros**.

#### Errores comunes

* Iniciar sesión en cuentas personales
* Cambiar configuración del navegador
* Abrir archivos fuera de Tor
* Descargas masivas

---

### Ataques de timing

Analizan patrones de tiempo y volumen para correlacionar tráfico de entrada y salida. Tor mitiga, pero no elimina este riesgo.

---

### Proxychains

Proxychains permite encadenar proxies (SOCKS/HTTP) y combinar herramientas CLI con Tor.

Usos:

* Pentesting
* OSINT
* Navegación avanzada

---

### Casos de uso profesionales

* Reconocimiento con nmap, dnsenum
* Fingerprinting de servicios
* Transferencia segura de archivos
* SSH con pivoting
* Web scraping sin bloqueo por IP

---

### ¿Qué es TAILS?

**Tails** es un sistema Linux amnésico:

* Arranque desde USB
* Todo el tráfico pasa por Tor
* No deja rastros tras apagarse

---

## PRÁCTICA

* Comparación con y sin extensiones de privacidad
* Instalación y uso de Tor Browser
* Análisis en ipleak.net y browserleaks.com
* Proxychains
* Chat anónimo
* Instalación de Tails

---

## Evaluación

* **25 preguntas** en formulario web (Página Luiskas Kiwi)

---

## Orden del Taller

1. Privacidad vs Anonimato
2. Fingerprinting y Threat Model
3. Comparativas prácticas
4. Funcionamiento de TOR
5. Bridges y errores comunes
6. Proxychains
7. Casos profesionales
8. Tails
9. Preguntas finales
