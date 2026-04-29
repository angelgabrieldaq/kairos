# Kairos

**Sistema de Trazabilidad Quirúrgica en Tiempo Real**

Herramienta de código abierto para mejorar visibilidad y coordinación en quirófanos. Nace de observar problemas reales en el terreno operatorio y buscar cómo resolverlos con tecnología.

---

## 🎯 El Problema

En quirófanos reales existe un patrón repetido:

- **Fragmentación de información:** Cirujano, anestesia, enfermería y administración cada uno maneja su propia información. No hay un registro únificado.
- **Tiempos invisibles:** Existen franjas de tiempo importante entre etapas (pre-quirófano → entrada, cirugía → recuperación) que nadie mide efectivamente
- **Falta de trazabilidad:** ¿Exactamente a qué hora entró el paciente? ¿Cuándo comenzó anestesia? ¿Cuándo se realizó el primer corte? Estos datos no están centralizados
- **Comunicación ad-hoc:** Se depende de llamadas, mensajes, notas en papeles. Sin registro de cambios
- **Visibilidad limitada:** Si necesitas saber dónde está un paciente o qué sucedió con uno específico, hay que preguntar a múltiples personas
- **Sin métrica de eficiencia:** Los quirófanos no saben realmente cuánto tiempo pierden en transiciones, limpieza, preparación

---

## 📋 Qué es Kairos

Una plataforma web que implementa:

- **Sistema de roles granular:** perfiles predefinidos con permisos específicos
- **Trazabilidad completa:** Registro de cada fase del paciente (pre-quirófano, anestesia, cirugía, recuperación)
- **Medición de tiempos:** Captura de cuándo ocurre cada evento
- **Interfaz por rol:** Cada usuario ve solo lo que autoriza su rol
- **8 pantallas funcionales:** Dashboard, quirófanos, agendas, pacientes, equipo, reportes, configuración, acta operatoria
- **Acceso inmediato:** Se descarga, abre en navegador, funciona

---

## 🚀 Por Qué Existe

1. **El problema es real** — Estos cuellos de botella existen en quirófanos que operan hoy
2. **Es resoluble ahora** — No necesita infraestructura futurista. Tecnología web estándar podría adaptarse para mejor visualización y toma de decisiones
3. **Debe ser abierto** — Múltiples perspectivas (médicas, técnicas, de procesos) mejoran la solución
4. **El beneficio es medible** — Mejoras en tiempos de quirófano = eficiencia = menos costos + eficiencia en gestión de recursos y mejor experiencia de paciente

---

## 🎯 Los Roles actuales y Sus Permisos (En fase de idea)

| Rol | Responsabilidad | Qué Ve |
|-----|-----------------|--------|
| **Director Quirúrgico** | Supervisión total, auditoría, control de permisos | Todo: pacientes, quirófanos, equipo, reportes completos, historial |
| **Coordinador** | Agendar quirófanos, asignar equipo y personal | Disponibilidad de quirófanos, agendas, asignaciones del día |
| **Circulante** | Información en tiempo real de lo que sucede en quirófano | Paciente en quirófano, timeline de eventos, novedades operatorias |
| **Camillero** | Trasladar pacientes, registrar movimientos | Ubicación de pacientes, destinos, cambios de zona |
| **UCA (Anestesia)** | Registrar parámetros anestésicos y cambios | Paciente actual, parámetros vitales, timeline anestésico |
| **Paciente** | Información de su propio proceso | Su información médica, fase actual, estimaciones de tiempo |
| **Administrador** | Gestión de usuarios, asignación de roles, control de permisos | Panel administrativo completo |

---

## 📊 Las Pantallas

### 1. Dashboard
Resumen en tiempo real: estado de quirófanos, próximo paciente, alertas críticas.

### 2. Quirófanos
Estado de cada quirófano: libre, en uso, mantenimiento. Equipo asignado, tiempo transcurrido.

### 3. Agendas
Reservar quirófanos. Filtrar por especialidad, fecha, cirujano. Visualizar disponibilidad.

### 4. Pacientes
Registro centralizado: datos demográficos, antecedentes, intervenciones previas, alergias.

### 5. Equipo
Disponibilidad de personal: cirujanos, anestesistas, enfermeros, tecnólogos. Horarios y especialidades.

### 6. Reportes
Auditoría completa: tiempos por quirófano, eficiencia, análisis de cuellos de botella, utilización.

### 7. Configuración (Admin)
Crear/editar usuarios, asignar roles, modificar permisos según política institucional.

### 8. Acta Operatoria
Registro quirúrgico detallado: descripción, incidentes, tiempos exactos de cada fase, resultado.

---

## 🏗️ Estructura del Proyecto

```
kairos/
├── index.html              # Punto de entrada
├── css/
│   ├── styles.css         # Estilos globales
│   └── roles.css          # Estilos por rol
├── js/
│   ├── app.js             # Lógica principal
│   ├── roles.js           # Definición de roles y permisos
│   ├── auth.js            # Control de acceso
│   └── data.js            # Datos de ejemplo
├── pages/
│   ├── dashboard.html     # Vista principal
│   ├── quirofanos.html    # Gestión de quirófanos
│   ├── agendas.html       # Agendamiento
│   ├── pacientes.html     # Registro de pacientes
│   ├── equipo.html        # Gestión de personal
│   ├── reportes.html      # Auditoría y análisis
│   ├── admin.html         # Panel administrativo
│   └── acta.html          # Acta operatoria
└── README.md              # Este archivo
```

---

## 💻 Tech Stack

- **Frontend:** HTML5, CSS3, JavaScript vanilla
- **Storage:** LocalStorage (versión actual)
- **Diseño:** Responsive, mobile-first
- **Compatibilidad:** Chrome, Firefox, Safari, Edge (versiones recientes)

---

## 🔐 Seguridad: Estado Actual y Necesidades

**Versión 0.2 (Actual):**
- Datos en LocalStorage del navegador
- Roles de demostración (sin autenticación real)
- Ideal para pilotos, demostraciones, evaluación de concepto

**Para uso en producción con datos reales se requiere:**
- Backend con API segura
- Autenticación real (LDAP, OAuth, o credenciales)
- Base de datos encriptada
- HTTPS obligatorio
- Cumplimiento normativo (HIPAA, GDPR, legislación local)
- Auditoría de accesos y cambios

---

## ❓ Preguntas Frecuentes

### ¿Está terminado?
No. Es un prototipo en desarrollo por lo que evoluciona constantemente.

### ¿Encontré un bug, qué hago?
Abre un issue en GitHub describiendo el problema. O arréglalo y abre un pull request. (Gracias!)

### ¿Puedo modificar para mis necesidades específicas?
Sí. AGPL v3 permite modificaciones. Las mejoras genéricas que benefician a otros: considera contribuirlas al proyecto principal.

---

## 📈 Hoja de Ruta

**Corto plazo (inmediato):**
- [ ] Exportar reportes a PDF
- [ ] Integración con calendario del sistema operativo
- [ ] Notificaciones en tiempo real
- [ ] Mejoras de UX basadas en feedback

**Mediano plazo:**
- [ ] Backend + API REST
- [ ] Autenticación real
- [ ] Base de datos
- [ ] Sincronización entre dispositivos
- [ ] Analítica avanzada de tiempos

**Largo plazo:**
- [ ] Integración con HIS existentes
- [ ] Módulo de recursos
- [ ] Predicción de tiempos (ML)
- [ ] Soporte multiidioma
- [ ] Apps móviles nativas

---

## 🤝 Cómo Contribuir

Si esto resuena con lo que ves en tu institución:

**Feedback médico/quirúrgico:**
- "En mi institución el flujo real es..."
- "Esto no funciona porque..."
- "Nos haría falta..."

**Feedback técnico:**
- "El código aquí debería ser..."
- "La arquitectura podría..."
- "Este bug ocurre cuando..."

**Contribuciones de código:**
1. Fork el repositorio
2. Crea rama con tu feature (`git checkout -b feature/nombre`)
3. Commit cambios (`git commit -m 'Descripción clara'`)
4. Push a la rama
5. Abre Pull Request con descripción de qué y por qué

**Contribuciones de procesos:**
- Documentar cómo funciona realmente el flujo en tu institución
- Identificar casos edge que no se cubren
- Proponer nuevos roles o pantallas basado en necesidades reales

---

## 📜 Licencia: AGPL v3

**Kairos está bajo AGPL v3** — Affero General Public License v3.

Esta es la licencia de salud pública para software de salud. Garantiza que el código abierto permanece abierto, especialmente cuando se usa como servicio.

### ¿Qué Puedes Hacer? (Libertades)

✅ **Usar:** Comercial, académico, personal, sin restricción
✅ **Modificar:** Adapta el código para tus necesidades
✅ **Distribuir:** Comparte copias del original o modificado
✅ **Ganar dinero:** Ofrece servicios, hosting, soporte basado en Kairos

### ¿Cuál Es La Obligación? (La Clave)

⚠️ **Si usas Kairos como servicio web/app** (usuarios acceden remotamente):

1. **Debes proporcionar código fuente** a tus usuarios
2. **Incluyendo tus modificaciones**
3. **Bajo la misma licencia AGPL v3**
4. **Gratuitamente**

Esto significa: si mejoras Kairos esas mejoras vuelven a la comunidad.

### Incumplimiento

Si alguien:
- Usa Kairos como servicio pero no libera código
- Cambia la licencia a propietaria
- Remueve atribución

**Es violación de AGPL v3:**
- Puedes exigir cumplimiento
- Puedes iniciar acción legal
- La comunidad puede reportar

---

## 📄 Licencia Completa

Ver archivo `LICENSE` en el repositorio para el texto completo de AGPL v3.

En resumen: **Libertad de usar, modificar y distribuir. Obligación de compartir mejoras cuando se usa como servicio.**

---

## 📞 Contacto y Comunidad

- **GitHub Issues:** Reporta bugs y propón mejoras
- **GitHub Discussions:** Conversaciones sobre arquitectura, procesos, ideas
- **Pull Requests:** Contribuciones de código
- **Email:** angel.acua@gmaill.com
- **LinkedIn:** https://www.linkedin.com/in/angel-acu%C3%B1a-b22a20159/

---

## 🎓 Aprendizajes Iniciales

Este proyecto demuestra que:

- Problemas reales en procesos hospitalarios **pueden resolverse con tecnología accesible**
- El flujo de información en quirófanos puede mejorar **sin infraestructura futurista**
- Perspectivas diversas (médicas, técnicas, de procesos) **generan soluciones mejores**
- Código abierto en healthcare **acelera innovación** mientras protege IP del creador

---

**Kairos: Porque los quirófanos merecen visibilidad, y eso es resoluble hoy.**

*Última actualización: 29 Abril 2026*
*Versión: 0.2 (Beta activo)*
*Licencia: AGPL v3*
*Copyright © 2026 angelgabrieldaq*
