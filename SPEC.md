# SPEC.md## 3) Funcionalidades

-   **Carga Inteligente:** Dropzone + botón **Procesar** con overlay por fases y validación robusta
-   **Estados Derivados:** Precálculo optimizado de `rowsArea` y `rowsAsignatura` para navegación sin reprocesos
-   **Filtros Persistentes:** Configuraciones guardadas en localStorage con sincronización automática
-   **KPIs Dinámicos:** Indicadores que responden a filtros aplicados en tiempo real
-   **Tablas Optimizadas:** Filtros/paginación con normalización de texto y búsqueda fuzzy
-   **Gráficos Sincronizables:** Chart.js con toggle "Sincronizar con filtros" y exportación PNG
-   **Consultas Rápidas:** Reportes automáticos (top áreas perdidas, estudiantes en riesgo, etc.)
-   **Backup/Restore:** Sistema completo de exportación/importación JSON de estado completo
-   **Exportación Multi-formato:** CSV (tablas), PNG (gráficos), JSON (backups)
-   **Validación de Calidad:** Log detallado de problemas de datos con descarga JSONecificación Téc## 6) Datos derivados
-   **`rowsArea` y `rowsAsignatura`** pre-calculados para performance óptima:
    -   **Campos crudos:** CURSO, AREA, ASIGNATURA, ESTUDIANTE, P1, P2, P3, DEF
    -   **Campos normalizados:** `CURSO_NORM`, `AREA_NORM`, `ASIG_NORM`, `EST_NORM` para filtros fuzzy
    -   **Estados calculados:** promedio actual, P4 mínima, estado académico con colores
-   **Normalización de Notas:** `notaFromCell()` - vacías → **0.0**, no numéricas → `null` → "-"
-   **Render Consistente:** `formatNota(n)` → formato "0.00" para todas las visualizaciones
-   **Síntesis DEF:** Para áreas unitarias, DEF se deriva automáticamente de la asignatura principal
-   **Validación de Rangos:** Notas fuera de [0,5] → `null` con log de calidad
-   **Log de Calidad:** Registro detallado de problemas de datos con descarga JSON

## 1) Objetivo

Analizar calificaciones desde archivos Excel multi-hoja y presentar KPIs, tablas filtrables y gráficos para docentes/directivos, en una SPA de **un único archivo (`index.html`)**.

## 2) Usuarios

-   Docentes: análisis por estudiante/área/asignatura.
-   Directivos: visión global por cursos, riesgos y tendencias.

## 3) Funcionalidades

-   Carga (dropzone) y botón **Procesar** con overlay por fases.
-   Precálculo de derivados (`rowsArea`, `rowsAsignatura`) y navegación sin reprocesos.
-   KPIs, tablas filtrables/paginadas y gráficos (Chart.js).
-   Consultas rápidas (top áreas perdidas, estudiantes en riesgo, etc.).
-   Toggle en **Gráficos**: “Sincronizar con filtros”.

## 4) Requisitos no funcionales

-   Rendimiento: overlay visible, tablas paginadas, navegación sobre derivados.
-   Portabilidad: **un único `index.html`**, sin proceso de build obligatorio.
-   Estabilidad: consola limpia en prod; logs/tiempos solo en modo dev.

## 5) Arquitectura/Stack

-   **SPA Monolítica:** Todo en `index.html` con `<script type="text/babel">` y React UMD (18.2.0)
-   **Librerías Fijas:** Chart.js 4.4.4, SheetJS/XLSX 0.18.5, Tailwind CSS via CDN
-   **Switch Dev/Prod:** Carga UMD síncrona con `document.write` - React/ReactDOM antes de Babel
-   **Sistema de Estados:** Lifted state con persistencia localStorage y derivados optimizados
-   **ResourceGuard:** Banner discreto si falla CDN (CORS/SRI/conectividad)
-   **ErrorBoundary:** Captura fallos de render con reintento suave sin reload
-   **A11y Completo:** Navegación con ←/→, Home/End y roles ARIA apropiados
-   **Filtro de Ruido:** Silencia automáticamente errores de extensiones externas
-   **Profiling Inteligente:** Console.time dev-only con evitación de "Timer already exists"
-   **Modos Deterministas:** `?mode=prod/dev` con señales CSS/JS y control de console noise

## 6) Datos derivados

-   `rowsArea` y `rowsAsignatura` incluyen:
    -   Campos crudos: CURSO, AREA, ASIGNATURA, ESTUDIANTE, P1, P2, P3, DEF, etc.
    -   Campos normalizados para filtros: `CURSO_NORM`, `AREA_NORM`, `ASIG_NORM`, `EST_NORM`.
-   Notas vacías → **0.0** (numérico). No numéricos reales → `null` → “-”.
-   Render numérico consistente con `formatNota(n)` → `0.00`.

## 7) Reglas de cálculo

-   Promedio actual = `((P1??0)+(P2??0)+(P3??0))/3` (2 decimales).
-   P4 mínima = `max(0, 12 - (P1??0 + P2??0 + P3??0))`.
-   Estados/KPIs usan los derivados y respetan filtros (si el toggle de Gráficos está ON).

## 8) Criterios de calidad

-   **Correctitud**: KPIs/tablas = derivados; gráficos sincronizables con filtros.
-   **UX**: overlay por fases (“Importando…”, “Analizando…”, “Consolidando…”).
-   **Estabilidad**: sin errores en consola en prod; en dev, métricas con `__DASH_DEV__=true`.
-   **Seguridad**: versiones fijas en CDNs; Tailwind sin `crossorigin`.

## 9) Roadmap actualizado (post-implementación)

### 🔒 **Seguridad y Robustez (Corto plazo)**

1. **SRI (Subresource Integrity)** en CDNs principales para verificar integridad
2. **Validación de esquemas** más estricta para archivos Excel importados
3. **Rate limiting** para procesamiento de archivos grandes

### 🚀 **Performance y Escalabilidad (Mediano plazo)**

1. **Web Workers** para procesamiento de archivos grandes sin bloquear UI
2. **Virtualización de tablas** para datasets con miles de registros
3. **IndexedDB** como alternativa a localStorage para datasets grandes
4. **Compresión** de datos en localStorage usando LZ-string

### 🎨 **Experiencia de Usuario (Mediano plazo)**

1. **Temas visuales** (modo oscuro/claro) con persistencia
2. **Configuraciones avanzadas** de filtros (rangos de fechas, operadores AND/OR)
3. **Drag & Drop** para reordenar columnas en tablas
4. **Dashboards personalizables** con widgets movibles

### 📊 **Análisis Avanzado (Largo plazo)**

1. **Análisis de tendencias** temporales entre períodos
2. **Predicciones de rendimiento** usando ML básico
3. **Comparativas entre cursos** con visualizaciones avanzadas
4. **Alertas automáticas** de estudiantes en riesgo crítico

### 🔌 **Integración y Exportación (Largo plazo)**

1. **Exportación PDF** con reportes formateados profesionalmente
2. **API endpoints** para integración con otros sistemas escolares
3. **Conectores directos** a Google Sheets/Microsoft Excel Online
4. **Plugins** para LMS (Learning Management Systems)
