# Sistema de Roles Funcional — Kairos v0.2

## 🎯 RESUMEN

Creé una versión **completamente funcional** del index que:

1. **✅ Muestra un modal al cargar** pidiendo que selecciones tu rol
2. **✅ Guarda la selección** en localStorage (persiste entre sesiones)
3. **✅ Filtra el menú** según el rol seleccionado
4. **✅ Genera el welcome dinámico** mostrando solo pantallas accesibles
5. **✅ Permite cambiar de rol** en cualquier momento
6. **✅ Controla acceso a pantallas** por rol

---

## 🚀 CÓMO FUNCIONA

### 1️⃣ **Primer acceso: Modal de selección**

Cuando cargas el index por primera vez, aparece un modal elegante con 7 roles:

```
┌─────────────────────────────────┐
│ Bienvenido a Kairos             │
│ Selecciona tu rol...            │
│                                 │
│ [👨‍⚕️] [📋] [⬡] [🚑]             │
│ Director Coord. Circulante Camillero │
│                                 │
│ [🏥] [👤] [⚙️]                   │
│ UCA Patient Admin               │
│                                 │
│ [Saltar] [Continuar como...]    │
└─────────────────────────────────┘
```

### 2️⃣ **Después de seleccionar**

- El rol se **guarda en localStorage**
- El menú se **filtra automáticamente** (solo muestra pantallas accesibles)
- El welcome muestra **solo tarjetas disponibles** para ese rol
- El topbar muestra **el nombre del usuario** asociado al rol

### 3️⃣ **Cambiar de rol**

En cualquier momento puedes:
- Hacer click en **"Cambiar rol"** en el sidebar
- Usar el **menú de usuario** en el topbar
- O limpiar la sesión completamente

---

## 🔐 ESTRUCTURA DE ROLES Y ACCESO

### Roles Definidos

```javascript
const ROLES_CONFIG = {
  director:    { icon: '👨‍⚕️', name: 'Director' },
  coord:       { icon: '📋', name: 'Coordinador' },
  circulante:  { icon: '⬡', name: 'Circulante' },
  camillero:   { icon: '🚑', name: 'Camillero' },
  uca:         { icon: '🏥', name: 'Recepcionista UCA' },
  paciente:    { icon: '👤', name: 'Paciente' },
  admin:       { icon: '⚙️', name: 'Administrador' }
}
```

### Acceso por Rol

| Rol | Dashboard | Coordinador | Circulante | Camilleros | Paciente | UCA | Jefatura | Roles |
|-----|:---------:|:-----------:|:----------:|:----------:|:--------:|:---:|:--------:|:-----:|
| **Director** | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ | ✅ | ❌ |
| **Coordinador** | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Circulante** | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Camillero** | ✅ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| **UCA** | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Paciente** | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| **Admin** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |

### Definición en HTML

Cada item del menú tiene un atributo `data-roles`:

```html
<div class="nav-item" 
     onclick="loadScreen('dashboard')" 
     id="nav-dashboard" 
     data-roles="director,coord,circulante,camillero">
```

---

## 💾 LOCALSTORAGE

### Qué se guarda

```javascript
localStorage.setItem('kairos-user-role', 'director');
```

### Recuperación al cargar

```javascript
const savedRole = localStorage.getItem('kairos-user-role');
if (savedRole && ROLES_CONFIG[savedRole]) {
  setUserRole(savedRole);
} else {
  showRoleSelector(); // Muestra modal si no hay rol guardado
}
```

---

## 🎨 COMPONENTES NUEVOS/MEJORADOS

### 1. Modal de Selección de Roles

```html
<div class="role-selector-modal" id="role-selector-modal">
  <div class="rsm-content">
    <div class="rsm-header">...</div>
    <div class="rsm-grid" id="role-grid">
      <!-- Generado dinámicamente -->
    </div>
    <div class="rsm-footer">
      <button class="rsm-btn rsm-btn-cancel">Saltar</button>
      <button class="rsm-btn rsm-btn-confirm">Continuar</button>
    </div>
  </div>
</div>
```

**CSS classes:**
- `.role-selector-modal` — Container del modal
- `.rsm-card` — Cada opción de rol
- `.rsm-card.selected` — Rol seleccionado (azul)
- `.rsm-btn` — Botones

### 2. Menú de Usuario (Topbar)

```html
<div class="gt-user" id="top-user" onclick="toggleUserMenu()">
  <div class="gt-av" id="top-av">—</div>
  <span id="top-username">Seleccioná un rol</span>
</div>
<div class="gt-user-menu" id="user-menu">
  <div class="gum-item" onclick="changeRole()">Cambiar rol</div>
  <div class="gum-item" onclick="loadScreen('roles')">Configurar</div>
  <div class="gum-item" onclick="clearStorage()">Limpiar sesión</div>
</div>
```

### 3. Opción en Sidebar

```html
<div class="nf-change-role" onclick="changeRole()">↻ Cambiar rol</div>
```

---

## 📊 FLUJO DE LA APLICACIÓN

```
┌─ App carga ──┐
│              ▼
│       ¿Hay rol en localStorage?
│       ▲              ▼
│   SÍ │         NO → Mostrar modal
│       │              de selección
│       │              │
│       │              ▼
│       │         Usuario selecciona rol
│       │         │
│       └─────────┤
│                 ▼
│         setUserRole(roleId)
│         ├─ Guardar en localStorage
│         ├─ Actualizar topbar
│         ├─ Filtrar menú (filterMenuByRole)
│         ├─ Generar welcome dinámico
│         └─ Ir a home (goHome)
│
└─ Usuario ve menú filtrado ──────┐
                                   ▼
                    Hace click en pantalla
                             │
                             ▼
                   ¿Tiene acceso (rol)?
                   ▲              ▼
              SÍ  │        NO → Alert + bloqueo
                  │
                  ▼
              Carga iframe
```

---

## 🔧 FUNCIONES PRINCIPALES

### `showRoleSelector()`
Muestra el modal de selección de roles. Se llama si no hay rol guardado.

### `selectRole(roleId, element)`
Marca un rol como seleccionado en el modal. Habilita el botón "Continuar".

### `confirmRole()`
Confirma la selección y llama a `setUserRole()`.

### `setUserRole(roleId)`
- Guarda en localStorage
- Actualiza topbar
- Filtra menú
- Genera welcome dinámico
- Oculta modal

### `filterMenuByRole(roleId)`
Itera cada nav-item, verifica si el rol está en `data-roles`, y añade/quita clase `hidden`.

### `generateWelcomeContent(roleId)`
Crea el contenido dinámico del welcome mostrando solo las pantallas accesibles.

### `changeRole()`
Limpia localStorage y recarga la página para volver a mostrar el modal.

### `loadScreen(id)`
Ahora verifica que el rol tiene acceso ANTES de cargar:
```javascript
const navItem = document.getElementById('nav-' + id);
if (!navItem || navItem.classList.contains('hidden')) {
  alert('No tienes acceso a esta pantalla con tu rol actual.');
  return;
}
```

### `toggleUserMenu()`
Abre/cierra el menú de usuario en el topbar.

---

## 🎯 EJEMPLO DE USO

### Escenario 1: Usuario Director

```
1. Carga index.html
2. Ve modal con 7 roles
3. Selecciona "Director"
4. Click en "Continuar como Director"
5. Ve menú con:
   - Dashboard ✅
   - Coordinador ✅
   - Circulante ✅
   - Tablero camilleros ✅
   - Jefatura ✅
   - Panel de roles ❌ (Hidden)
6. Puede hacer click en cualquier pantalla permitida
7. Si intenta acceder a "Paciente" → Bloqueado
```

### Escenario 2: Usuario Camillero

```
1. Carga index.html
2. Ve modal con 7 roles
3. Selecciona "Camillero"
4. Click en "Continuar como Camillero"
5. Ve menú con:
   - Dashboard ✅
   - Tablero camilleros ✅
   - Todos los demás ❌ (Hidden)
6. Welcome solo muestra estas 2 opciones
7. Si intenta cargar "coordinador" → Bloqueado
```

---

## 🔄 PERSONALIZAR ROLES Y ACCESO

### Para añadir un nuevo rol:

**1. En ROLES_CONFIG:**
```javascript
const ROLES_CONFIG = {
  // ... otros roles
  enfermero: {
    icon: '🏥',
    name: 'Enfermero',
    desc: 'Personal de enfermería',
    user: 'EN',
    username: 'Enfermero del turno'
  }
}
```

**2. En los nav-items:**
```html
<div class="nav-item" 
     data-roles="director,coord,enfermero">
```

### Para cambiar acceso de un rol:

Simplemente editar el `data-roles` en cada nav-item:

```html
<!-- Antes: solo director tenía acceso a jefatura -->
<div data-roles="director">

<!-- Después: director y coordinador -->
<div data-roles="director,coord">
```

---

## 🎨 ESTILOS NUEVOS

```css
/* Modal */
.role-selector-modal       /* Backdrop con blur */
.rsm-content              /* Container interno */
.rsm-card                 /* Tarjeta de rol */
.rsm-card.selected        /* Rol seleccionado */
.rsm-btn                  /* Botones */

/* Usuario Menu */
.gt-user                  /* Botón usuario en topbar */
.gt-user-menu             /* Dropdown menu */
.gt-user-menu.visible     /* Menu visible */
.gum-item                 /* Items del menu */

/* Menú lateral */
.nav-item.hidden          /* Oculta items no accesibles */
.nf-change-role           /* Link "Cambiar rol" en footer */
```

---

## 🔒 SEGURIDAD

⚠️ **IMPORTANTE**: Este es un **prototipo frontend**. La seguridad real requiere:

1. **Backend validation**: Verificar en servidor que el usuario tiene acceso
2. **JWT/Tokens**: No confiar solo en localStorage
3. **Session management**: Validar sesión en cada request
4. **RBAC server-side**: Role-Based Access Control en la API

Este index es para **demostración de UX**. Para producción:
- Validar rol en backend
- Usar sesiones seguidas
- Implementar JWT tokens
- Auditar acceso a datos

---

## ✅ CHECKLIST

- [x] Modal de selección al cargar
- [x] 7 roles diferentes con iconos
- [x] localStorage para persistencia
- [x] Menú filtrado por rol
- [x] Welcome dinámico
- [x] Topbar actualizado
- [x] Menú de usuario (cambiar rol, config, limpiar)
- [x] Link en sidebar para cambiar rol
- [x] Control de acceso en loadScreen()
- [x] Todos los nav-items con data-roles

---

## 📝 NOTAS

### localStorage debugging

En consola del navegador:
```javascript
// Ver rol guardado
localStorage.getItem('kairos-user-role')

// Simular otro rol
localStorage.setItem('kairos-user-role', 'camillero')
location.reload()

// Limpiar todo
localStorage.clear()
location.reload()
```

### Modificar acceso en vivo

```javascript
// En consola, dar acceso a una pantalla
document.getElementById('nav-jefatura').removeAttribute('data-roles')

// O restringir
document.getElementById('nav-dashboard').setAttribute('data-roles', 'admin')
```

---

## 🚀 PRÓXIMAS MEJORAS

1. **Guardos de preferencias**: Guardar pantalla favorita por rol
2. **Historial de acceso**: Log quién accedió a qué
3. **Permisos granulares**: No solo rol, sino permisos específicos
4. **Integración con API**: Traer roles desde backend
5. **LDAP/SSO**: Autenticación empresarial
6. **Auditoría**: Registrar cambios de rol

---

**Archivo:** `index_funcional.html`  
**Versión:** v0.2  
**Tipo:** Completamente funcional  
**Status:** ✅ Listo para usar
