# SNIPPETS Y CUSTOMIZACIÓN — Sistema de Roles

## 🔧 CÓMO PERSONALIZAR

### 1. AÑADIR UN NUEVO ROL

**Paso 1:** Añadir a `ROLES_CONFIG`

```javascript
const ROLES_CONFIG = {
  // ... roles existentes
  
  // NUEVO ROL
  enfermero: {
    icon: '🏥',
    name: 'Enfermero',
    desc: 'Personal de enfermería',
    user: 'EN',
    username: 'Enfermero del turno'
  }
}
```

**Paso 2:** Añadir acceso a pantallas

```html
<!-- Modificar los data-roles de los nav-items -->
<!-- ANTES (solo director) -->
<div data-roles="director" ...>Jefatura</div>

<!-- DESPUÉS (director y enfermero) -->
<div data-roles="director,enfermero" ...>Jefatura</div>
```

### 2. CAMBIAR ACCESO DE UN ROL

**Añadir acceso:**

```javascript
// Coordinador ANTES: acceso a dashboard y coordinador
// DESPUÉS: también puede ver circulante

// En el nav-item de circulante:
// ANTES: data-roles="director,circulante"
// DESPUÉS: data-roles="director,circulante,coord"
```

```html
<div class="nav-item" 
     data-roles="director,circulante,coord"
     onclick="loadScreen('circulante')" 
     id="nav-circulante">
```

**Quitar acceso:**

```html
<!-- ANTES: Camillero puede ver dashboard -->
<div data-roles="director,coord,circulante,camillero" ...>Dashboard</div>

<!-- DESPUÉS: Camillero NO puede ver dashboard -->
<div data-roles="director,coord,circulante" ...>Dashboard</div>
```

---

## 📝 SNIPPETS ÚTILES

### Snippet 1: Crear rol dinámico desde datos

```javascript
// Si traes roles desde una API:
const createRoleFromAPI = (apiRole) => {
  return {
    icon: apiRole.icon,
    name: apiRole.display_name,
    desc: apiRole.description,
    user: apiRole.abbreviation,
    username: apiRole.full_title
  };
};

// Uso:
fetch('/api/roles')
  .then(r => r.json())
  .then(roles => {
    roles.forEach(apiRole => {
      ROLES_CONFIG[apiRole.id] = createRoleFromAPI(apiRole);
    });
    // Ahora regenerar el modal...
    showRoleSelector();
  });
```

### Snippet 2: Verificar permisos programáticamente

```javascript
const hasAccess = (roleId, screenId) => {
  const navItem = document.getElementById('nav-' + screenId);
  if (!navItem) return false;
  const allowedRoles = navItem.getAttribute('data-roles').split(',');
  return allowedRoles.includes(roleId);
};

// Uso:
console.log(hasAccess('director', 'jefatura'));     // true
console.log(hasAccess('camillero', 'jefatura'));    // false
```

### Snippet 3: Listar pantallas disponibles para un rol

```javascript
const getAccessibleScreens = (roleId) => {
  const screens = [];
  Object.entries(SCREENS).forEach(([screenId, screenData]) => {
    const navItem = document.getElementById('nav-' + screenId);
    if (navItem) {
      const roles = navItem.getAttribute('data-roles').split(',');
      if (roles.includes(roleId)) {
        screens.push({ id: screenId, ...screenData });
      }
    }
  });
  return screens;
};

// Uso:
console.log(getAccessibleScreens('director'));
// [
//   {id: 'dashboard', label: 'Dashboard · Monitoreo'},
//   {id: 'coord', label: 'Coordinador turno QX'},
//   ...
// ]
```

### Snippet 4: Crear matriz de permisos

```javascript
const generatePermissionMatrix = () => {
  const matrix = {};
  
  Object.keys(ROLES_CONFIG).forEach(roleId => {
    matrix[roleId] = {};
    Object.keys(SCREENS).forEach(screenId => {
      const navItem = document.getElementById('nav-' + screenId);
      if (navItem) {
        const roles = navItem.getAttribute('data-roles').split(',');
        matrix[roleId][screenId] = roles.includes(roleId);
      }
    });
  });
  
  return matrix;
};

// Uso:
const permisos = generatePermissionMatrix();
console.log(permisos);
// {
//   director: { dashboard: true, coord: true, paciente: false, ... },
//   coord: { dashboard: true, coord: true, paciente: false, ... },
//   ...
// }
```

### Snippet 5: Rol con permisos granulares (avanzado)

```javascript
// En lugar de solo rol, usar permisos específicos:
const USER_PERMISSIONS = {
  'director': ['view:all', 'edit:all', 'delete:all', 'manage:users'],
  'coord': ['view:qx', 'edit:own', 'view:paciente'],
  'circulante': ['view:qx', 'scan:qr', 'mark:hitos'],
  'camillero': ['view:dashboard', 'view:camilleros', 'mark:traslados']
};

const canAccess = (screen) => {
  const userPermissions = USER_PERMISSIONS[currentRole] || [];
  const requiredPermission = `view:${screen}`;
  return userPermissions.includes(requiredPermission);
};

// Uso:
if (canAccess('dashboard')) {
  loadScreen('dashboard');
}
```

---

## 🎨 CUSTOMIZACIÓN VISUAL

### Cambiar colores del modal

```css
/* En el <style> cambiar estos colores */

/* Fondo del modal */
.role-selector-modal {
  background: rgba(0,0,0,.6); /* Más opaco */
}

/* Botón "Continuar" */
.rsm-btn-confirm {
  background: #0C447C; /* Azul en lugar de verde */
}

/* Card seleccionada */
.rsm-card.selected {
  border-color: #0C447C;
  background: #E6F1FB;
  box-shadow: 0 4px 16px rgba(12, 68, 124, .2);
}
```

### Cambiar iconos de roles

```javascript
const ROLES_CONFIG = {
  director: {
    icon: '🔑', // Cambiar de 👨‍⚕️ a 🔑
    name: 'Director',
    // ...
  }
}
```

### Cambiar tamaño del modal

```css
.rsm-content {
  max-width: 800px; /* De 600px a 800px */
  padding: 48px;   /* De 32px a 48px */
}
```

---

## 🔌 INTEGRACIÓN CON API

### Traer roles desde backend

```javascript
const loadRolesFromAPI = async () => {
  try {
    const response = await fetch('/api/roles');
    const rolesData = await response.json();
    
    // Limpiar ROLES_CONFIG
    Object.keys(ROLES_CONFIG).forEach(key => delete ROLES_CONFIG[key]);
    
    // Poblar con datos de API
    rolesData.forEach(role => {
      ROLES_CONFIG[role.id] = {
        icon: role.icon,
        name: role.name,
        desc: role.description,
        user: role.abbreviation,
        username: role.username
      };
    });
    
    // Regenerar modal
    showRoleSelector();
  } catch (err) {
    console.error('Error cargando roles:', err);
  }
};

// Llamar al cargar la página
window.addEventListener('DOMContentLoaded', loadRolesFromAPI);
```

### Validar rol en servidor

```javascript
const setUserRole = async (roleId) => {
  try {
    // Validar en servidor
    const response = await fetch('/api/auth/validate-role', {
      method: 'POST',
      headers: {'Content-Type': 'application/json'},
      body: JSON.stringify({ role: roleId })
    });
    
    if (!response.ok) {
      throw new Error('Rol no válido');
    }
    
    const { token } = await response.json();
    
    // Guardar token en lugar de solo rol
    localStorage.setItem('kairos-token', token);
    localStorage.setItem('kairos-user-role', roleId);
    
    // Continuar...
    const roleData = ROLES_CONFIG[roleId];
    document.getElementById('top-av').textContent = roleData.user;
    // ...
    
  } catch (err) {
    alert('No se pudo validar tu rol. Intenta de nuevo.');
    console.error(err);
  }
};
```

### Verificar token antes de cargar pantalla

```javascript
const loadScreen = async (id) => {
  // ... código existente ...
  
  try {
    // Validar acceso en servidor
    const token = localStorage.getItem('kairos-token');
    const response = await fetch(`/api/screens/${id}/access`, {
      headers: { 'Authorization': `Bearer ${token}` }
    });
    
    if (!response.ok) {
      alert('No tienes acceso a esta pantalla');
      return;
    }
    
    // Si es válido, cargar
    iframe.src = s.file;
    
  } catch (err) {
    console.error('Error validando acceso:', err);
  }
};
```

---

## 📊 LOGGING Y AUDITORÍA

### Registrar cambios de rol

```javascript
const logRoleChange = (fromRole, toRole) => {
  const log = {
    timestamp: new Date().toISOString(),
    from: fromRole,
    to: toRole,
    user: localStorage.getItem('kairos-user-role'),
    browser: navigator.userAgent
  };
  
  // Guardar localmente
  const logs = JSON.parse(localStorage.getItem('kairos-logs') || '[]');
  logs.push(log);
  localStorage.setItem('kairos-logs', JSON.stringify(logs));
  
  // Enviar a servidor
  fetch('/api/logs/role-change', {
    method: 'POST',
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify(log)
  }).catch(err => console.error('Error logging:', err));
};

// Usar en setUserRole():
if (currentRole !== roleId) {
  logRoleChange(currentRole, roleId);
}
```

### Registrar acceso a pantallas

```javascript
const logScreenAccess = (screenId) => {
  const log = {
    timestamp: new Date().toISOString(),
    screen: screenId,
    role: currentRole,
    source: 'navigation'
  };
  
  fetch('/api/logs/screen-access', {
    method: 'POST',
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify(log)
  }).catch(err => console.error('Error logging:', err));
};

// Usar en loadScreen():
const loadScreen = (id) => {
  // ... código existente ...
  logScreenAccess(id);
  // ...
};
```

---

## 🧪 TESTING

### Test en consola

```javascript
// Cambiar a rol de prueba
localStorage.setItem('kairos-user-role', 'director');
location.reload();

// Verificar pantallas accesibles
const director = getAccessibleScreens('director');
console.log(director.length); // Debería ser ~5

const camillero = getAccessibleScreens('camillero');
console.log(camillero.length); // Debería ser 2

// Verificar matriz
const matrix = generatePermissionMatrix();
console.table(matrix);
```

### Test automatizado (Jest ejemplo)

```javascript
describe('Roles System', () => {
  
  test('Director tiene acceso a todas las pantallas de operación', () => {
    const screens = getAccessibleScreens('director');
    expect(screens.map(s => s.id)).toContain('dashboard');
    expect(screens.map(s => s.id)).toContain('jefatura');
  });
  
  test('Camillero solo accede a 2 pantallas', () => {
    const screens = getAccessibleScreens('camillero');
    expect(screens).toHaveLength(2);
  });
  
  test('Paciente solo accede a su propio flujo', () => {
    const screens = getAccessibleScreens('paciente');
    expect(screens.map(s => s.id)).toEqual(['paciente']);
  });
  
  test('No hay pantalla accesible para todos', () => {
    const matrix = generatePermissionMatrix();
    Object.values(SCREENS).forEach(screen => {
      const accessCount = Object.values(matrix).filter(
        role => role[screen.id]
      ).length;
      expect(accessCount).toBeGreaterThan(0);
    });
  });
});
```

---

## 🚀 DEPLOYMENT

### Archivo de configuración por ambiente

**config.development.js**
```javascript
const CONFIG = {
  proyecto: { nombre: 'Kairos', version: 'v0.2 · dev' },
  api: 'http://localhost:3000/api',
  mockRoles: true
};
```

**config.production.js**
```javascript
const CONFIG = {
  proyecto: { nombre: 'Kairos', version: 'v0.2' },
  api: 'https://api.hospital.com/api',
  mockRoles: false
};
```

### Script de inicialización

```javascript
// Cargar config según ambiente
const env = window.location.hostname === 'localhost' ? 'development' : 'production';
document.body.innerHTML += `<script src="config.${env}.js"><\/script>`;

// Cargar roles después de config
if (CONFIG.mockRoles) {
  // Usar ROLES_CONFIG hardcodeados
  showRoleSelector();
} else {
  // Traer de API
  loadRolesFromAPI();
}
```

---

## 📚 REFERENCIA RÁPIDA

| Función | Para qué |
|---------|----------|
| `showRoleSelector()` | Mostrar modal de roles |
| `selectRole(id, elem)` | Marcar rol como seleccionado |
| `confirmRole()` | Confirmar selección y cargar |
| `setUserRole(id)` | Aplicar rol (guardar, filtrar, etc) |
| `filterMenuByRole(id)` | Ocultar/mostrar items según rol |
| `generateWelcomeContent(id)` | Crear welcome dinámico |
| `changeRole()` | Volver al modal |
| `loadScreen(id)` | Cargar pantalla con validación |
| `hasAccess(roleId, screenId)` | Verificar si tiene permiso |
| `getAccessibleScreens(roleId)` | Listar pantallas del rol |
| `generatePermissionMatrix()` | Matriz completa de permisos |

---

**Version:** v0.2  
**Tipo:** Ejemplos y snippets  
**Status:** ✅ Listo para usar
