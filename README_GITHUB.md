# KAIROS — Sistema de Trazabilidad Quirúrgica en Tiempo Real

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-Active-brightgreen.svg)](https://github.com)
[![Version](https://img.shields.io/badge/version-2.0-blue.svg)](https://github.com)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

> **Plataforma modular de coordinación quirúrgica** con trazabilidad en tiempo real, gestión de lechos (CLIX), análisis operativo y flujo prequirúrgico digital.

## 🎯 Descripción

KAIROS es una **solución de código abierto** para coordinación quirúrgica que proporciona:

- ✅ **Trazabilidad en tiempo real** del paciente desde prequirófano hasta alta
- ✅ **CLIX** — Gestión inteligente de lechos, limpieza y mantenimiento
- ✅ **Flujo digital prequirúrgico** completamente online (11 pasos)
- ✅ **Dashboard de monitoreo** con estado en vivo de recursos
- ✅ **Analítica operativa** para optimización de procesos
- ✅ **Sistema de roles flexible** adaptable a cualquier institución
- ✅ **Integraciones** con HIS, Redmine, Slack, SMS y más

No reemplaza tu HIS, lo **complementa** con una capa de coordinación que muchos sistemas no tienen.

---

## 🚀 Inicio Rápido

### Opción 1: Abrir en navegador (más fácil)
```bash
# Descargá la carpeta completa
# Haz doble click en index.html
# ¡Listo! Se abre en tu navegador
```

### Opción 2: Servidor local
```bash
# Python 3
python3 -m http.server 8000

# Node.js
npx http-server

# Luego abre http://localhost:8000
```

### Opción 3: Deployar en la nube
- [Firebase Hosting](https://firebase.google.com/hosting)
- [GitHub Pages](https://pages.github.com/)
- [Vercel](https://vercel.com)
- [Netlify](https://netlify.com)
- Tu servidor web (Apache, Nginx)

---

## 📂 Estructura del Proyecto

```
kairos/
├── index.html                           ⭐ Punto de entrada
│
├── MÓDULOS/
│   ├── Flujo Prequirúrgico
│   │   └── 04_flujo_paciente_v3.html
│   │
│   ├── Coordinación Quirófano
│   │   ├── 02_coordinador_turno_qx_v2.html
│   │   ├── 05_circulante_qx.html
│   │   └── 03_dashboard_monitoreo.html
│   │
│   ├── CLIX - Gestión de Lechos
│   │   ├── 09_clix_v1.html
│   │   ├── 10_clix_app_limpieza.html
│   │   └── CLIX_ARQUITECTURA_ESCALABLE.md
│   │
│   ├── Administrativo
│   │   ├── 01_panel_roles.html
│   │   └── 06_uca_jefatura.html
│   │
│   └── Control de Traslados
│       └── 08_tablero_camilleros.html
│
├── DOCUMENTACIÓN/
│   ├── README.md (este archivo)
│   ├── KAIROS_ARQUITECTURA.md
│   ├── CLIX_ARQUITECTURA_ESCALABLE.md
│   ├── GUIA_ROLES.md
│   ├── API_INTEGRACIONES.md
│   └── CONTRIBUTING.md
│
├── config.js                            Configuración (opcional)
└── LICENSE                              MIT License
```

---

## 🌟 Características Principales

### **KAIROS — Flujo Quirúrgico**
- Flujo prequirúrgico de 11 pasos completamente digital
- Dashboard de monitoreo en tiempo real
- Sistema de roles (7 roles base configurables)
- Coordinación de equipos y materiales
- Trazabilidad de pacientes y hitos
- Analytics operativa con KPIs

### **CLIX — Gestión de Lechos**
- Ocupación en tiempo real por piso/ala
- Información del paciente + alertas principales
- Historial de admisiones/altas
- Log de limpieza con evaluación de tercerizada
- Integración con Redmine para mantenimiento
- App PWA móvil para equipo de limpieza
- Categorización dinámica de pacientes
- Predicción de demanda y optimización

### **Integraciones**
- **HIS:** Sincronización automática de pacientes
- **Redmine:** Circuito de mantenimiento automático
- **Slack/Teams:** Notificaciones de alertas
- **SMS Gateway:** Alertas críticas
- **APIs REST:** Extensible para cualquier sistema

---

## 📖 Documentación

| Documento | Descripción |
|-----------|-------------|
| [KAIROS_ARQUITECTURA.md](docs/KAIROS_ARQUITECTURA.md) | Diseño técnico completo, estructura de datos, flujos |
| [CLIX_ARQUITECTURA_ESCALABLE.md](docs/CLIX_ARQUITECTURA_ESCALABLE.md) | Módulo de gestión de lechos, real-time, eventos |
| [GUIA_ROLES.md](docs/GUIA_ROLES.md) | Manual de usuario por cada rol |
| [API_INTEGRACIONES.md](docs/API_INTEGRACIONES.md) | Especificación de APIs, webhooks, ejemplos |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Guía para contribuidores |

---

## 🔧 Configuración

### Sin código (recomendado)
Si tienes `config.js`, úsalo para personalizar:

```javascript
const CONFIG = {
  proyecto: {
    nombre: 'KAIROS',
    empresa: 'Tu Institución',
    version: 'v2.0'
  },
  institucion: { nombre: 'Tu Centro Médico' }
};
```

### Con código
Edita variables CSS en cualquier HTML:

```css
:root {
  --bl: #0c447c;      /* Azul principal */
  --g: #15803d;       /* Verde success */
  --a: #b45309;       /* Naranja warning */
  --r: #ef4444;       /* Rojo error */
}
```

---

## 🔐 Roles Disponibles

| Rol | Acceso | Descripción |
|-----|:------:|-------------|
| 👨‍⚕️ Director | 6 pantallas | Jefatura, reportes, KPIs |
| 📋 Coordinador | 3 pantallas | Gestión de turno, requisitos |
| ⬡ Circulante | 2 pantallas | Registro en quirófano |
| 🚑 Camillero | 2 pantallas | Traslados de pacientes |
| 🏥 UCA | 1 pantalla | Recepción de pacientes |
| 👤 Paciente | 1 pantalla | Flujo prequirúrgico |
| ⚙️ Admin | 1 pantalla | Configuración del sistema |

Totalmente **configurable** — agregar/modificar roles sin código.

---

## 💻 Requisitos Técnicos

### Mínimo (Dev)
- Navegador moderno (Chrome, Firefox, Safari, Edge)
- JavaScript habilitado
- LocalStorage disponible

### Recomendado (Producción)
- Node.js 14+ (para servidor local)
- Servidor web (Apache, Nginx)
- HTTPS obligatorio
- PostgreSQL (si usas backend)

### Sin dependencias externas
- HTML5 puro
- CSS3 puro
- JavaScript Vanilla
- **0 frameworks** — código transparente y educativo

---

## 🚀 Deploy

### GitHub Pages (Gratuito)
```bash
git push origin main
# Settings → Pages → Source: main / root
# Tu sitio está en: https://usuario.github.io/kairos
```

### Firebase Hosting
```bash
npm install -g firebase-tools
firebase init hosting
firebase deploy
```

### Vercel / Netlify
Conecta tu repositorio GitHub, ¡automático!

---

## 🔌 Integraciones

### Conectar tu HIS
```javascript
// En tu backend
POST /api/v1/kairos/sync
{
  "paciente_id": "PAC-123",
  "datos": { ... }
}
```

### Conectar Redmine
```javascript
// Para crear issues de mantenimiento
POST /api/v1/redmine/issue
{
  "lecho_id": "P2-A1-C01",
  "tipo": "Rueda rota"
}
```

Ver [API_INTEGRACIONES.md](docs/API_INTEGRACIONES.md) para ejemplos completos.

---

## 📊 Analytics y Reportes

KAIROS genera automáticamente:

- Ocupación quirúrgica (% utilización)
- Tiempos de procedimiento
- Eficiencia de traslados
- Evaluación de limpieza
- KPIs operacionales
- Comparación histórica

Todo exportable a **CSV/PDF** para jefatura.

---

## 🆘 Troubleshooting

### Las pantallas no cargan
```bash
# ❌ No: Abre index.html directamente
# ✅ Sí: Usa servidor local
python3 -m http.server 8000
```

### El menú no se filtra
```javascript
// En DevTools Console
localStorage.clear()
location.reload()
```

### Problemas de CORS
```bash
# Usar servidor local en lugar de file://
npm install -g http-server
http-server
```

---

## 🤝 Contribuciones

¡Bienvenidas! Lee [CONTRIBUTING.md](CONTRIBUTING.md) para:

- Cómo reportar bugs
- Cómo proponer features
- Proceso de pull requests
- Guía de estilo

### Quick Start para devs
```bash
# Fork el repo
git clone https://github.com/tu-usuario/kairos.git
cd kairos

# Crear rama para tu feature
git checkout -b feature/mi-feature

# Hacer cambios y commit
git add .
git commit -m "feat: descripción clara"

# Push y crear Pull Request
git push origin feature/mi-feature
```

---

## 📋 Hoja de Ruta

### v2.0 (Actual) ✅
- [x] Sistema de roles modular
- [x] Flujo prequirúrgico completo
- [x] CLIX - Gestión de lechos
- [x] Dashboard de monitoreo
- [x] Arquitectura escalable

### v2.1 (Próximo) 📅
- [ ] WebSocket para real-time
- [ ] Notificaciones push
- [ ] App móvil nativa
- [ ] Integración Redmine completa

### v3.0 (Futuro) 🔮
- [ ] Machine Learning para predicciones
- [ ] Optimización automática
- [ ] Multi-hospital
- [ ] API pública para partners

---

## ⚠️ Consideraciones de Seguridad

### Estado Actual
**Prototipo de frontend** — ideal para:
- ✅ Pruebas y evaluaciones
- ✅ Integración con backend existente
- ✅ Proof of concept
- ✅ Educación y aprendizaje

### Para Producción necesitas
- Backend con validación en servidor
- Autenticación robusta (JWT/OAuth)
- Base de datos real (PostgreSQL)
- HTTPS obligatorio
- Auditoría de accesos
- Cumplimiento normativo (HIPAA, GDPR, etc.)

Consulta [KAIROS_ARQUITECTURA.md](docs/KAIROS_ARQUITECTURA.md) para especificaciones de seguridad.

---

## 📄 Licencia

Este proyecto está bajo licencia **MIT** — libre para usar, modificar y distribuir.

Ver [LICENSE](LICENSE) para detalles completos.

---

## 🙌 Agradecimientos

Desarrollado para mejorar la coordinación quirúrgica en instituciones de salud.

Inspirado en:
- Estándares de healthcare IT
- Mejores prácticas en quirófanos
- Feedback de equipos médicos
- Comunidad open-source healthcare

---

## 📞 Soporte

### Documentación
- [KAIROS_ARQUITECTURA.md](docs/KAIROS_ARQUITECTURA.md) — Especificación técnica
- [CLIX_ARQUITECTURA_ESCALABLE.md](docs/CLIX_ARQUITECTURA_ESCALABLE.md) — Gestión de lechos
- [GUIA_ROLES.md](docs/GUIA_ROLES.md) — Manual de usuario
- [API_INTEGRACIONES.md](docs/API_INTEGRACIONES.md) — Para desarrolladores

### Comunidad
- **Issues:** [GitHub Issues](https://github.com/usuario/kairos/issues)
- **Discussions:** [GitHub Discussions](https://github.com/usuario/kairos/discussions)
- **Email:** contacto@kairos.health (si aplicable)

---

## ✨ ¿Listo para comenzar?

### Usuarios finales
1. Descargá todos los archivos
2. Abre `index.html` en tu navegador
3. ¡Listo! Selecciona un rol y explora

### Desarrolladores
1. `git clone https://github.com/usuario/kairos.git`
2. `cd kairos`
3. `python3 -m http.server 8000`
4. Abre `http://localhost:8000`
5. Lee [CONTRIBUTING.md](CONTRIBUTING.md)

---

## 📊 Estadísticas del Proyecto

![GitHub stars](https://img.shields.io/github/stars/usuario/kairos?style=social)
![GitHub forks](https://img.shields.io/github/forks/usuario/kairos?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/usuario/kairos?style=social)

---

<div align="center">

**KAIROS** — Sistema de Trazabilidad Quirúrgica  
*Versión 2.0 · 2026*  
*Diseñado para la salud moderna*

[🏠 Sitio Web](#) · [📖 Documentación](docs/) · [🐛 Reportar Bug](https://github.com/usuario/kairos/issues) · [💡 Sugerir Feature](https://github.com/usuario/kairos/discussions)

</div>
