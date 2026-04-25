# KAIROS v0.2 — Sistema de Trazabilidad Quirúrgica

## 🚀 INICIO RÁPIDO

### 1. Descargar
- Descarga la carpeta `kairos-v0.2` completa

### 2. Instalar
```bash
# Opción A: Abre directamente en navegador
Haz doble click en index.html

# Opción B: Usa un servidor local
python3 -m http.server 8000
# O con Node.js
npx http-server
```

### 3. Usar
- Abre http://localhost:8000 (o la URL que aparezca)
- Se mostrará un modal para seleccionar tu rol
- Selecciona tu rol y comienza a navegar

---

## 📂 ESTRUCTURA DE ARCHIVOS

```
kairos-v0.2/
├── index.html                          ⭐ ABRE ESTO PRIMERO
├── 
├── Pantallas (8 archivos HTML)
│   ├── 01_panel_roles.html            Administración de roles
│   ├── 02_coordinador_turno_qx_v2.html Gestión de turno
│   ├── 03_dashboard_monitoreo.html    Monitoreo en tiempo real
│   ├── 04_flujo_paciente_v3.html      Flujo pre-quirúrgico
│   ├── 05_circulante_qx.html          Circulante / Anestesia
│   ├── 06_uca_jefatura.html           UCA + Jefatura
│   └── 08_tablero_camilleros.html     Tablero de camilleros
│
└── Documentación (4 archivos MD)
    ├── DOCUMENTACION_SISTEMA_ROLES.md  Especificación técnica
    ├── GUIA_RAPIDA_ROLES.md            Guía visual y flujos
    ├── SNIPPETS_CUSTOMIZACION.md       Ejemplos de código
    └── LIMPIEZA_SANATORIO_FINOCHIETTO.md Cambios realizados
```

---

## 🔐 SISTEMA DE ROLES FUNCIONAL

### 7 Roles Disponibles

| Rol | Acceso | Descripción |
|-----|:------:|-------------|
| 👨‍⚕️ Director | 6 pantallas | Jefatura del área quirúrgica |
| 📋 Coordinador | 3 pantallas | Coordinador de turno |
| ⬡ Circulante | 2 pantallas | Técnico en quirófano |
| 🚑 Camillero | 2 pantallas | Traslado de pacientes |
| 🏥 UCA | 1 pantalla | Recepcionista 2° piso |
| 👤 Paciente | 1 pantalla | Vista pre-quirúrgica |
| ⚙️ Admin | 1 pantalla | Gestión del sistema |

### Cómo Funciona

1. **Primer acceso:** Ve un modal con 7 roles
2. **Selecciona tu rol:** Se guarda en localStorage
3. **Menú filtrado:** Solo ves tus pantallas
4. **Persistencia:** Al volver, tu rol se recuerda
5. **Cambiar rol:** Click en "Cambiar rol" en sidebar o topbar

---

## 🎯 PRIMEROS PASOS

### Paso 1: Abre index.html
```
Double click en index.html
O arrastra a tu navegador
```

### Paso 2: Selecciona un rol
```
Haz click en el que quieras probar
(Prueba con "Director" para ver todo)
```

### Paso 3: Navega
```
Usa el menú lateral para cambiar de pantalla
Cada pantalla es totalmente funcional
```

### Paso 4: Experimenta
```
Haz click en elementos
Prueba diferentes roles
Cambia de rol cuando quieras
```

---

## 📖 DOCUMENTACIÓN

### Para Entender Todo
→ Lee **DOCUMENTACION_SISTEMA_ROLES.md**  
Especificación técnica completa, cómo funciona localStorage, estructura de roles, etc.

### Para Ver Ejemplos Visuales
→ Lee **GUIA_RAPIDA_ROLES.md**  
Flujos visuales, matrices de acceso, ejemplos de uso por rol

### Para Personalizar o Integrar
→ Lee **SNIPPETS_CUSTOMIZACION.md**  
Ejemplos de código, cómo cambiar roles, integración con APIs, logging

### Qué Cambió
→ Lee **LIMPIEZA_SANATORIO_FINOCHIETTO.md**  
Resumen de eliminación de datos específicos

---

## 🔧 CONFIGURACIÓN (Opcional)

### Cambiar Institución
Si tienes un `config.js`:

```javascript
const CONFIG = {
  proyecto: {
    nombre: 'Kairos',
    empresa: 'Tu Institución',
    tagline: 'Tu tagline aquí',
    version: 'v0.2'
  },
  institucion: {
    nombre: 'Tu Centro Médico'
  }
};
```

Luego en el `<head>` del index:
```html
<script src="config.js"></script>
```

---

## 🚀 DEPLOYMENT

### Opción 1: Servidor Local (Desarrollo)
```bash
# Python 3
python3 -m http.server 8000

# Node.js (npx)
npx http-server

# Node.js (http-server)
npm install -g http-server
http-server
```

### Opción 2: Servidores Reales
- Firebase Hosting
- Vercel
- Netlify
- GitHub Pages
- Tu servidor web (Apache, Nginx)

---

## ⚙️ REQUISITOS

### Mínimo
- ✅ Navegador moderno (Chrome, Firefox, Safari, Edge)
- ✅ JavaScript habilitado
- ✅ LocalStorage disponible

### Recomendado
- 🎯 Chrome/Firefox actualizado
- 🎯 Conexión a internet para primero uso
- 🎯 Pantalla 1024x768 o mayor

---

## 🔐 PRIVACIDAD Y SEGURIDAD

### ⚠️ IMPORTANTE
- **Frontend-only:** Este es un prototipo de interface
- **No es seguro para datos reales:** Sin validación en servidor
- **Sin base de datos:** Todo se guarda en localStorage (navegador)
- **Sin autenticación:** Solo almacenamiento local

### Para Producción
Necesitarás:
1. Backend con validación
2. Base de datos
3. JWT/OAuth para autenticación
4. HTTPS obligatorio
5. Auditoría de accesos

---

## 🐛 TROUBLESHOOTING

### No aparece el modal de roles
- ✅ Limpiar localStorage: Press F12 → Application → LocalStorage → Clear
- ✅ Actualizar página (Ctrl+F5)
- ✅ Probar en navegador diferente

### Menú no se filtra
- ✅ Verificar que rol esté en localStorage
- ✅ En consola (F12): `localStorage.getItem('kairos-user-role')`
- ✅ Si está vacío, limpiar y recargar

### Las pantallas no cargan
- ✅ Verificar que todos los HTML estén en la misma carpeta
- ✅ Abrir con servidor local, no con file://
- ✅ Ver consola (F12) para ver errores

### Problema de CORS
- ✅ Usar servidor local (no abrir HTML directo)
- ✅ `python3 -m http.server 8000`

---

## 💡 TIPS Y TRUCOS

### Cambiar rol rápidamente
Click en el nombre del usuario en topbar derecha → "Cambiar rol"

### Ver localStorage en consola
```javascript
// Ver rol actual
localStorage.getItem('kairos-user-role')

// Ver todo
localStorage

// Limpiar
localStorage.clear()
location.reload()
```

### Probar acceso por rol
```javascript
// En consola del navegador
localStorage.setItem('kairos-user-role', 'camillero')
location.reload()
// Ahora eres Camillero
```

### Modificar roles en código
Editar en `index.html`:
```javascript
const ROLES_CONFIG = {
  tunuevorol: {
    icon: '🎯',
    name: 'Tu Rol',
    // ...
  }
}
```

---

## 📞 SOPORTE

### Documentación
- DOCUMENTACION_SISTEMA_ROLES.md
- GUIA_RAPIDA_ROLES.md
- SNIPPETS_CUSTOMIZACION.md

### Validación
- Abre DevTools (F12)
- Ve a Console
- Busca errores en rojo
- Copia el error y búscalo en documentación

---

## ✅ CHECKLIST DE USO

- [ ] Descargué la carpeta kairos-v0.2
- [ ] Abrí index.html en navegador
- [ ] Vi el modal de selección de roles
- [ ] Seleccioné un rol (prueba Director)
- [ ] El menú se filtró correctamente
- [ ] Navegué a diferentes pantallas
- [ ] Cambié de rol exitosamente
- [ ] Leí al menos una documentación
- [ ] Entiendo cómo funciona el sistema

---

## 🎓 PRÓXIMOS PASOS

1. **Explorar:** Prueba todos los roles
2. **Entender:** Lee la documentación
3. **Personalizar:** Adapta a tu institución
4. **Integrar:** Conecta con tu backend
5. **Deployar:** Sube a producción

---

## 📊 VERSIÓN

**Kairos v0.2**
- Sistema de roles funcional
- Tablero de camilleros integrado
- Menú reorganizado
- Sin datos de Sanatorio Finochietto
- Completamente genérico

**Fecha:** 25 de Abril de 2026  
**Status:** ✅ Listo para usar  
**Licencia:** Proyecto de prototipo

---

## 🙌 ¡Listo para usar!

Solo abre **index.html** en tu navegador y comienza.

**¡Que disfrutes Kairos!** 🚀
