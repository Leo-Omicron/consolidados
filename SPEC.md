Perfecto 👌, aquí tienes el archivo **`SPEC.md`** actualizado, consistente con tu proyecto donde el archivo principal es **`index.html`**.

---

## 📄 SPEC.md

````markdown
# SPEC.md — Especificación Técnica del Proyecto

---

## 1. Objetivo del software

Facilitar a docentes y directivos el **análisis de desempeño académico** de estudiantes mediante la carga de archivos Excel, con visualizaciones y reportes que permitan detectar **áreas críticas y oportunidades de mejora**.

---

## 2. Usuarios y roles

- **Docentes:**  
  Suben notas de su curso, analizan rendimiento individual y de áreas.  

- **Directivos:**  
  Consolidan información de varios cursos, generan reportes globales y gráficos comparativos.  

---

## 3. Funcionalidades principales

1. **Carga de archivos Excel**
   - Dropzone para arrastrar o seleccionar uno o varios archivos.
   - Botón **“Procesar”** que inicia parsing y análisis bajo un overlay/loader.

2. **Procesamiento de datos**
   - Limpieza, parsing y consolidación de notas.
   - Pre-cálculo de estructuras aplanadas (`rowsArea`, `rowsAsignatura`) y KPIs globales.

3. **Dashboard con pestañas**
   - **Análisis:**  
     Tablas de **Áreas** y **Asignaturas** con filtros (curso, estudiante, área, estado).  
     Incluye paginación y KPIs de estado.  
   - **Gráficos:**  
     Visualizaciones dinámicas de KPIs, distribuciones y tendencias.  
   - **Consultas rápidas:**  
     Reportes automáticos: top perdidos, recuperables, riesgos, mejores estudiantes.  

---

## 4. Requisitos no funcionales

- **Performance:**  
  Navegación fluida; sin reprocesos al cambiar de pestaña. Solo se recalcula al cargar un nuevo Excel.  

- **Compatibilidad:**  
  HTML único (`index.html`), sin dependencias externas.  

- **Escalabilidad:**  
  Preparado para crecer con nuevos reportes, filtros y exportaciones.  

- **Usabilidad:**  
  Interfaz clara, feedback inmediato (overlay visible en procesos).  

---

## 5. Tecnologías y arquitectura

- **Archivo único:** `index.html`.  
- **JS embebido:** React con hooks (`useState`, `useMemo`, `useEffect`, etc.) dentro de `<script type="text/babel">`.  
- **CSS embebido:** Estilos integrados (Tailwind inline o reglas personalizadas).  
- **Visualización:** Tablas HTML y gráficos basados en Canvas, sin librerías externas.  

---

## 6. Modelo de datos (post-procesamiento)

### `rowsArea`
```json
{
  "id": "unique-id",
  "__course": "Curso A",
  "estudiante": "Juan Pérez",
  "area": "Matemáticas",
  "defP1": 3.2,
  "defP2": 4.1,
  "defP3": 3.8,
  "promActual": 3.7,
  "p4Min": 2.9,
  "estado": "En riesgo"
}
````

### `rowsAsignatura`

```json
{
  "id": "unique-id",
  "__course": "Curso A",
  "estudiante": "Juan Pérez",
  "area": "Matemáticas",
  "asignatura": "Álgebra",
  "p1": 3.5,
  "p2": 4.0,
  "p3": 3.6,
  "promActual": 3.7,
  "p4Min": 2.9,
  "estado": "Ganable"
}
```

### Índices y KPIs

* **Listas únicas:** `studentList`, `areaList`, `asigList`, `courseList`.
* **KPIs globales:**

  * `promGeneral`
  * `estadoCounts` (Perdido, En riesgo, Recuperable, Ganable, Ganado)
  * `areaRiesgo` (por área: en riesgo, reprobados, total)

---

## 7. Backlog técnico

* **Migración completa a derivados:** que todas las vistas (DashboardView, Charts, QuickReports) usen `derived` para evitar reprocesos.
* **KPIs con filtros:** recalcular solo desde arrays aplanados filtrados.
* **Exportación de reportes:** PDF y Excel.
* **Overlay con fases:** mensajes “Importando → Analizando → Consolidando”.
* **Optimización de tablas grandes:** paginación refinada, carga progresiva.
* **Accesibilidad:** roles ARIA y navegación por teclado.

---

## 8. Riesgos y mitigaciones

* **Bloqueo de UI:**
  Mitigado usando `useMemo`, `useTransition` y precálculo en `App`.

* **Archivos Excel corruptos o mal formateados:**
  Validación previa + mensajes claros en overlay.

* **Crecimiento del dataset:**
  Uso de paginación y filtrado eficiente sobre arrays ya aplanados.

---

## 8. Ubicación recomendada:  

/ (raíz del proyecto)
├── index.html         # Código principal (único archivo ejecutable)
├── GEMINI.md          # Guía de comportamiento del Agente IA + contexto del proyecto
├── SPEC.md            # Especificación técnica del software
└── README.md          # (opcional) Resumen breve para colegas

---