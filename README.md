# Taller: Navegación Anónima y Red TOR

## 1. Introducción: El mito de la privacidad
* **Privacidad vs. Anonimato vs. Seguridad:** Diferencias clave.
* **¿Quién nos vigila?** Rastreadores, ISP (Proveedores de Internet), Gobiernos y Capitalismo de Vigilancia.
* **La Huella Digital:** Metadatos, *Browser Fingerprinting* y direcciones IP.

## 2. ¿Qué es TOR? (The Onion Router)

* **Historia y propósito:** Del laboratorio naval de EE.UU. al activismo global.
* **Funcionamiento técnico simplificado:**
    * El concepto de "Capas de Cebolla".
    * Nodos de Entrada (Guard), Nodos Intermedios y Nodos de Salida.
    * Por qué la red es lenta (latencia y saltos).
* **Mitos sobre la Deep Web y Dark Web:** Diferenciando contenido oculto de actividades ilegales.

## 3. Taller Práctico: Tor Browser
* **Descarga y Verificación:**
    * Fuentes oficiales (torproject.org).
    * Verificación de firmas PGP (Nivel intermedio/avanzado).
* **Instalación y Primer Inicio:**
    * Configuración básica.
    * ¿Qué hacer si Tor está bloqueado en tu país? (Uso de **Bridges/Puentes**).
* **La Interfaz:**
    * El botón de "Nueva Identidad" vs. "Nuevo Circuito".
    * Niveles de Seguridad (Estándar, Seguro, El más seguro) y qué deshabilitan (JavaScript).

Material de apoyo:

- Guía de instalación multi-sistema: [instalacion/README.md](instalacion/README.md)
- Guía de puentes (bridges): [bridges/README.md](bridges/README.md)

## 4. OpSec: Reglas de Oro para el Anonimato
> **Nota crucial:** Usar Tor no te hace invisible si tu comportamiento te delata.

* **Lo que NUNCA debes hacer en Tor:**
    * Loguearte en cuentas personales (Google, Facebook) vinculadas a tu identidad real.
    * Abrir documentos (PDF, DOC) descargados mientras estás conectado a internet.
    * Usar Torrent sobre Tor (Desanonimización y carga a la red).
* **HTTPS sobre Tor:** El problema de los nodos de salida maliciosos.
* **Hábitos de navegación:** Maximizar ventanas (fingerprinting) y uso de extensiones externas.

## 5. Navegando los Servicios Ocultos (.onion)
* **¿Qué es una dirección .onion?** Cifrado de extremo a extremo dentro de la red.
* **Buscadores en la red Tor:** DuckDuckGo (versión onion), Ahmia, Torch.
* **Casos de uso legítimo:**
    * Periodismo (SecureDrop).
    * Correo anónimo (ProtonMail versión onion).
    * Evasión de censura en regímenes autoritarios.

## 6. Herramientas Avanzadas y Ecosistema

* **Tails OS (The Amnesic Incognito Live System):**
    * Qué es y por qué Snowden lo recomienda.
    * Ejecutar un sistema operativo desde un USB que no deja rastro.
* **Tor en Móviles:**
    * **Android:** Tor Browser para Android y Orbot.
    * **iOS:** Onion Browser.
* **OnionShare:** Compartir archivos de forma anónima y efímera.

## 7. Conclusiones y Debate
* **Limitaciones de Tor:** Ataques de correlación de tráfico (teórico).
* **Ética del anonimato:** Responsabilidad del usuario.
* **Ronda de Preguntas (Q&A).**
