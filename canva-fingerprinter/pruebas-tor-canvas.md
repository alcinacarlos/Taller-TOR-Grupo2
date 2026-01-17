# 🔍 Pruebas FÁCILES: ¿Tu navegador te delata? (Sin TOR vs Con TOR)

**Imagina esto**: Sin protección, sitios ven tu IP (tu "casa digital"), idioma español y hasta tu tarjeta gráfica. TOR te hace "invisible" como los demás usuarios TOR. ¡Vamos a comprobarlo fácil!

## 🎯 PASO A PASO (5 minutos cada prueba)

### 1️⃣ **PREPARA todo**
- **Sin TOR**: Abre Chrome/Firefox normal 
- **Con TOR**: Descarga gratis torproject.org (¡usa bridges si está bloqueado!)
- 📸 Toma **pantallazo** de cada resultado

---

## 🌐 1. ipleak.net - "¿Ven mi dirección real?"
```
QUÉ BUSCAR:
❌ Sin TOR = Tu IP España + Vodafone
✅ Con TOR = IP USA/Alemania (¡no la tuya!)
```

**Haz esto**:
1. Ve a ipleak.net
2. Mira **IP** y **ISP** arriba
3. Baja a **WebRTC** (debe estar VACÍO en TOR)

---

## 🕵️‍♂️ 2. browserleaks.com - "Mi huella digital única"
```
LOS PELIGROS que te ven:
❌ Sin TOR = Canvas único, Madrid CET, español
✅ Con TOR = Canvas bloqueado, inglés UTC
```

**Prueba YA**:
```
https://browserleaks.com/canvas ← Canvas (¡LO PRINCIPAL!)
https://browserleaks.com/webrtc ← IP real leak
```

**Canvas explicado simple**: Es como tu firma digital. Cada PC la hace diferente. TOR la bloquea.

---

## 🛡️ 3. coveryourtracks.eff.org - "Puntuje EFF"
```
RESULTADOS:
❌ Sin TOR = "TU NAVEGADOR ES ÚNICO 😱"
✅ Con TOR = "MUY PROTEGIDO 🟢"
```

**Solo click** "TEST NOW" → Mira barras verdes/rojas.

---

## 📊 TABLA RÁPIDA: Lo que DEBE pasar

| Sitio | ❌ Sin TOR | ✅ Con TOR |
|-------|------------|------------|
| **IP** | Córdoba España | Virginia USA 🇺🇸 |
| **Canvas** | Hash único tuyo | **BLOQUEADO** |
| **WebRTC** | IP real | ❌ VACÍO |
| **EFF** | Fingerprint único | **Strong** |

## 🚨 ERRORES COMUNES (y solución)
```
❌ Ventana maximizada → Fingerprint único
✅ Deja barras negras (letterboxing)

❌ WebRTC muestra IP real  
✅ Tor Browser ya lo bloquea

❌ "Partial" en EFF
✅ Activa "Safer" → botón cebolla
```

## 🎉 RESULTADO PERFECTO TOR
```
✅ IP diferente cada vez
✅ Canvas: "Permission denied"
✅ EFF: Protegido + trackers bloqueados
✅ No leaks WebRTC/DNS
```