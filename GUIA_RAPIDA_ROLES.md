# GUÍA RÁPIDA — Sistema de Roles Funcional

## 🎬 FLUJO VISUAL

### 1. PRIMER ACCESO
```
┌──────────────────────────────────────────┐
│                                          │
│     KAIROS                               │
│     ──────────────────────────────────   │
│     Bienvenido a Kairos                  │
│     Selecciona tu rol...                 │
│                                          │
│     👨‍⚕️ 📋 ⬡ 🚑                        │
│  Director Coord Circulante Camillero     │
│                                          │
│     🏥 👤 ⚙️                             │
│  UCA Paciente Admin                      │
│                                          │
│  [Saltar]  [Continuar como...]           │
│                                          │
└──────────────────────────────────────────┘
```

### 2. DESPUÉS DE SELECCIONAR DIRECTOR

```
Antes (todos los roles):              Después (filtrado):
┌──────────────────────────────┐     ┌──────────────────────────────┐
│ OPERACIONES QUIRÚRGICAS      │     │ OPERACIONES QUIRÚRGICAS      │
│ ├─ Dashboard                 │     │ ├─ Dashboard                 │
│ ├─ Coordinador turno         │     │ ├─ Coordinador turno        │
│ ├─ Circulante / Anestesia    │     │ ├─ Circulante / Anestesia   │
│ ├─ Tablero camilleros        │     │ ├─ Tablero camilleros       │
│                              │     │                              │
│ FLUJOS DE PACIENTES          │     │ ADMINISTRACIÓN               │
│ ├─ Flujo del paciente        │     │ ├─ Jefatura · Analítica     │
│ ├─ Recepcionista UCA         │     │ └─ Panel de roles           │
│                              │     │                              │
│ ADMINISTRACIÓN               │     │ (Cambiar rol ↻)             │
│ ├─ Jefatura · Analítica      │     │                              │
│ └─ Panel de roles            │     └──────────────────────────────┘
│                              │
│ (Cambiar rol ↻)             │
└──────────────────────────────┘
```

### 3. TOPBAR ACTUALIZADO

```
Antes (sin seleccionar):                 Después (como Director):

┌────────────────────────────────────┐  ┌────────────────────────────────────┐
│ Kairos  Zenoxia  │ Trazab... │      │  │ Kairos  Zenoxia  │ Trazab... │ DR │
│         v0.2  [—] Selecciona un rol│  │         v0.2  [—] Díaz Ruiz, Adriana│
└────────────────────────────────────┘  └────────────────────────────────────┘

                                        Al hacer click en "DR":
                                        ┌──────────────────────┐
                                        │ Cambiar rol          │
                                        │ ────────────────     │
                                        │ Configurar acceso    │
                                        │ Limpiar sesión       │
                                        └──────────────────────┘
```

---

## 🔄 MATRIZ DE ACCESO

### Director
```
✅ Dashboard
✅ Coordinador turno
✅ Circulante / Anestesia
✅ Tablero camilleros
✅ Jefatura · Analítica
❌ Flujo del paciente
❌ Recepcionista UCA
❌ Panel de roles
```

### Coordinador
```
✅ Dashboard
✅ Coordinador turno
✅ Tablero camilleros
❌ Circulante / Anestesia
❌ Jefatura · Analítica
❌ Flujo del paciente
❌ Recepcionista UCA
❌ Panel de roles
```

### Circulante
```
✅ Dashboard
✅ Circulante / Anestesia
❌ Coordinador turno
❌ Tablero camilleros
❌ Jefatura · Analítica
❌ Flujo del paciente
❌ Recepcionista UCA
❌ Panel de roles
```

### Camillero
```
✅ Dashboard
✅ Tablero camilleros
❌ Coordinador turno
❌ Circulante / Anestesia
❌ Jefatura · Analítica
❌ Flujo del paciente
❌ Recepcionista UCA
❌ Panel de roles
```

### Recepcionista UCA
```
✅ Recepcionista UCA
❌ Dashboard
❌ Coordinador turno
❌ Circulante / Anestesia
❌ Tablero camilleros
❌ Jefatura · Analítica
❌ Flujo del paciente
❌ Panel de roles
```

### Paciente
```
✅ Flujo del paciente
❌ Dashboard
❌ Coordinador turno
❌ Circulante / Anestesia
❌ Tablero camilleros
❌ Jefatura · Analítica
❌ Recepcionista UCA
❌ Panel de roles
```

### Administrador
```
✅ Panel de roles
❌ Todos los demás
```

---

## 💾 ALMACENAMIENTO

### Qué se guarda en localStorage

```javascript
{
  "kairos-user-role": "director"
}
```

### Cómo se usa

**Primer acceso:**
- localStorage está vacío
- Se muestra modal
- Usuario selecciona rol
- Se guarda: `localStorage.setItem('kairos-user-role', 'director')`

**Acceso posterior:**
- localStorage tiene rol
- Se salta modal
- Se aplica rol automáticamente

**Limpiar:**
- Click en "Limpiar sesión"
- Se borra: `localStorage.removeItem('kairos-user-role')`
- Recarga página
- Vuelve a mostrar modal

---

## 🎮 INTERACCIONES DEL USUARIO

### Opción 1: Menú de usuario (topbar)
```
Hace click en [DR] Díaz Ruiz...
         ↓
Aparece dropdown con 3 opciones:
  1. Cambiar rol          → Vuelve a modal
  2. Configurar acceso    → Abre Panel de roles
  3. Limpiar sesión       → Borra localStorage y recarga
```

### Opción 2: Cambiar rol en sidebar
```
Hace click en "↻ Cambiar rol"
         ↓
Se borra localStorage
         ↓
Se recarga página
         ↓
Vuelve a mostrar modal de selección
```

### Opción 3: Intentar acceso no autorizado
```
Está como Camillero
         ↓
Intenta hacer click en "Jefatura · Analítica"
         ↓
Sistema verifica: ¿Camillero puede acceder?
         ↓
No está en data-roles="director"
         ↓
Alert: "No tienes acceso a esta pantalla con tu rol actual."
         ↓
No carga la pantalla
```

---

## 📊 EJEMPLO: DIRECTOR vs CAMILLERO

### Vista de DIRECTOR
```
┌─────────────────────────────────────────────────┐
│ KAIROS    Zenoxia    │ Trazab...  │ DR (Díaz R.)│
├─────────────────────────────────────────────────┤
│                                                 │
│ Operaciones Quirúrgicas                        │
│ ├─ 📊 Dashboard              [4]              │
│ ├─ 📋 Coordinador turno      [2]              │
│ ├─ ⬡ Circulante / Anestesia                   │
│ └─ 🚑 Tablero camilleros     [✓]              │
│                                                 │
│ Administración                                  │
│ └─ 📈 Jefatura · Analítica                     │
│ └─ ⚙️ Panel de roles                            │
│                                                 │
│ ↻ Cambiar rol                                   │
│                                                 │
└─────────────────────────────────────────────────┘

WELCOME mostrará 4 pantallas:
├─ Dashboard
├─ Coordinador
├─ Circulante
├─ Tablero camilleros
└─ Jefatura
```

### Vista de CAMILLERO
```
┌─────────────────────────────────────────────────┐
│ KAIROS    Zenoxia    │ Trazab...  │ CA (Sistema)│
├─────────────────────────────────────────────────┤
│                                                 │
│ Operaciones Quirúrgicas                        │
│ ├─ 📊 Dashboard                               │
│ └─ 🚑 Tablero camilleros     [✓]              │
│                                                 │
│                                                 │
│ ↻ Cambiar rol                                   │
│                                                 │
└─────────────────────────────────────────────────┘

WELCOME mostrará 2 pantallas:
├─ Dashboard
└─ Tablero camilleros
```

---

## 🔌 DATOS EN HTML

### Definición de Roles

```html
<!-- En ROLES_CONFIG (JavaScript) -->
const ROLES_CONFIG = {
  director: {
    icon: '👨‍⚕️',
    name: 'Director',
    desc: 'Jefatura del área quirúrgica',
    user: 'DR',
    username: 'Dr. Díaz Ruiz, Adriana'
  },
  // ... más roles
}
```

### Asignación de Acceso

```html
<!-- En cada nav-item -->
<div class="nav-item" 
     data-roles="director,coord,circulante,camillero"
     onclick="loadScreen('dashboard')" 
     id="nav-dashboard">
  <!-- Este item es visible para estos 4 roles -->
</div>

<div class="nav-item" 
     data-roles="director"
     onclick="loadScreen('jefatura')" 
     id="nav-jefatura">
  <!-- Este solo para Director -->
</div>
```

---

## 🚨 ALERTAS Y BLOQUEOS

### Si intentas acceder sin rol
```
❌ No hay rol
❌ localStorage vacío
✅ Modal se muestra automáticamente
```

### Si intentas acceder a pantalla no autorizada
```
✅ Hay rol
✅ localStorage tiene 'director'
✅ Pero intenta navegar a 'panel_roles' (admin only)
❌ Alert: "No tienes acceso a esta pantalla"
❌ No carga iframe
```

---

## 📋 CHECKLIST DE USO

### Primer uso (productor)
- [ ] Abre index.html
- [ ] Ve el modal
- [ ] Selecciona su rol (ej: "Coordinador")
- [ ] Click en "Continuar como Coordinador"
- [ ] Ve menú filtrado
- [ ] Navega a "Coordinador turno"
- [ ] Puede usar todas sus pantallas
- [ ] Al volver mañana, el rol se recuerda

### Cambio de usuario
- [ ] Usuario A estaba como "Director"
- [ ] Hace click en "Cambiar rol"
- [ ] Se muestra modal
- [ ] Usuario B selecciona "Camillero"
- [ ] Vuelve al menú filtrado para Camillero

### Administrador
- [ ] Entra como "Director" o "Admin"
- [ ] Accede a "Panel de roles"
- [ ] Puede configurar accesos
- [ ] Los cambios se guardan (en servidor, en v1.0)

---

## 🎯 PRÓXIMOS PASOS

1. **Backend integration**: Traer roles desde API
2. **JWT tokens**: Validar en servidor
3. **Audit logging**: Registrar accesos
4. **Permisos granulares**: Más control que solo rol
5. **SSO**: Integrar con LDAP/Azure AD
6. **Mobile responsive**: Adaptar modal para móvil

---

**Estado:** ✅ **COMPLETAMENTE FUNCIONAL**
**Archivo:** `index_funcional.html`
**Versión:** v0.2
**Última actualización:** Abril 2026
