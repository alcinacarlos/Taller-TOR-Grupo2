# Instalación de Tor Browser (Windows, macOS, Linux, Android e iOS)

Esta guía explica cómo **descargar e instalar Tor Browser desde fuentes oficiales** en distintos sistemas operativos.


---

## 1) Requisitos y notas rápidas

- **Fuente oficial de descarga:** https://www.torproject.org/download/
- **Puentes/Bridges si Tor está bloqueado:** consulta [Bridges](../bridges/README.md)
- **Actualizaciones:** Tor Browser se actualiza desde el propio navegador (te avisará cuando haya una nueva versión).

---

## 2) Windows (10/11)

1. Entra a https://www.torproject.org/download/
2. Descarga **Tor Browser para Windows** (archivo `.exe`).
3. Ejecuta el instalador.
4. Elige idioma y carpeta de instalación.
5. Abre **Tor Browser** desde el acceso directo.
6. Pulsa **Connect/Conectar** (o configura puentes si estás en una red censurada).

**Notas comunes en Windows**

- Si Windows SmartScreen muestra un aviso, verifica que el instalador venga de `torproject.org`.
- Evita “packs” o “descargas rápidas” de páginas no oficiales.

---

## 3) macOS

1. Entra a https://www.torproject.org/download/
2. Descarga **Tor Browser para macOS** (archivo `.dmg`).
3. Abre el `.dmg`.
4. Arrastra **Tor Browser** a la carpeta **Applications/Aplicaciones**.
5. Abre Tor Browser.

**Si macOS bloquea la app (Gatekeeper)**

- Haz clic derecho en Tor Browser → **Open/Abrir** → confirma.
- En algunos casos: **System Settings** → **Privacy & Security** → permitir la apertura.

---

## 4) Linux

Este método funciona en la mayoría de distribuciones.

1. Entra a https://www.torproject.org/download/
2. Descarga el archivo para **Linux** (normalmente un `.tar.xz`).
3. Extrae el archivo en una carpeta (por ejemplo `~/tor-browser`).
4. Entra a la carpeta extraída y ejecuta el lanzador.

Ejemplo desde terminal (ajusta el nombre del archivo):

```bash
cd ~/Descargas
tar -xf tor-browser-linux-*.tar.xz
cd tor-browser*/
./start-tor-browser.desktop
```

**Consejos en Linux**

- Si no se abre el `.desktop`, prueba ejecutarlo desde el gestor de archivos o revisa permisos de ejecución.
- Evita instalar “torbrowser” desde repositorios no oficiales si no confías en su mantenimiento.

### Alternativa: “Tor Browser Launcher” (si tu distro lo ofrece)

Algunas distribuciones incluyen un lanzador que descarga y mantiene Tor Browser por ti.

- Ubuntu/Debian (si está disponible en tu versión):

```bash
sudo apt update
sudo apt install torbrowser-launcher
```

- Arch

```bash
pacman -S torbrowser-launcher 
```

- Luego ejecuta `torbrowser-launcher`.

> Si tu distro no tiene el paquete, usa el método oficial (tarball) de arriba.

---

## 5) Android

Opciones recomendadas:

1) **Google Play**: busca **Tor Browser** (publicado por *The Tor Project*).

2) **APK oficial**: desde https://www.torproject.org/download/ (útil si no tienes Play Store).

Pasos generales:

1. Instala Tor Browser.
2. Ábrelo y pulsa **Connect/Conectar**.
3. Si tu red bloquea Tor, activa **Bridges/Puentes** y configura uno (ver [Bridges](../bridges/README.md)).

