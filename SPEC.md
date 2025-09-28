# SPEC.md — Especificación Técnica

## 1) Objetivo
Analizar calificaciones desde archivos Excel multi-hoja y presentar KPIs, tablas filtrables y gráficos para docentes/directivos, en una SPA de **un único archivo (`index.html`)**.

## 2) Usuarios
- Docentes: análisis por estudiante/área/asignatura.
- Directivos: visión global por cursos, riesgos y tendencias.

## 3) Funcionalidades
- Carga (dropzone) y botón **Procesar** con overlay por fases.
- Precálculo de derivados (`rowsArea`, `rowsAsignatura`) y navegación sin reprocesos.
- KPIs, tablas filtrables/paginadas y gráficos (Chart.js).
- Consultas rápidas (top áreas perdidas, estudiantes en riesgo, etc.).
- Toggle en **Gráficos**: “Sincronizar con filtros”.

## 4) Requisitos no funcionales
- Rendimiento: overlay visible, tablas paginadas, navegación sobre derivados.
- Portabilidad: **un único `index.html`**, sin proceso de build obligatorio.
- Estabilidad: consola limpia en prod; logs/tiempos solo en modo dev.

## 5) Arquitectura/Stack
- SPA en `index.html` con `<script type="text/babel">` y React UMD (18.2).
- Chart.js 4.4.4 para gráficos; SheetJS/XLSX 0.18.5 para lectura Excel.
- **Switch Dev/Prod** (carga UMD síncrona con `document.write`): React y ReactDOM se cargan antes de Babel.
- **Versiones fijas** en CDNs (React/ReactDOM/Chart.js/XLSX).
- **ResourceGuard**: banner discreto si falla un CDN (CORS/SRI/conectividad).
- **ErrorBoundary**: captura fallos de render y ofrece reintento.
- **A11y tabs**: navegación con ←/→ y Home/End.

## 6) Datos derivados
- `rowsArea` y `rowsAsignatura` incluyen:
  - Campos crudos: CURSO, AREA, ASIGNATURA, ESTUDIANTE, P1, P2, P3, DEF, etc.
  - Campos normalizados para filtros: `CURSO_NORM`, `AREA_NORM`, `ASIG_NORM`, `EST_NORM`.
- Notas vacías → **0.0** (numérico). No numéricos reales → `null` → “-”.
- Render numérico consistente con `formatNota(n)` → `0.00`.

## 7) Reglas de cálculo
- Promedio actual = `((P1??0)+(P2??0)+(P3??0))/3` (2 decimales).
- P4 mínima = `max(0, 12 - (P1??0 + P2??0 + P3??0))`.
- Estados/KPIs usan los derivados y respetan filtros (si el toggle de Gráficos está ON).

## 8) Criterios de calidad
- **Correctitud**: KPIs/tablas = derivados; gráficos sincronizables con filtros.
- **UX**: overlay por fases (“Importando…”, “Analizando…”, “Consolidando…”).
- **Estabilidad**: sin errores en consola en prod; en dev, métricas con `__DASH_DEV__=true`.
- **Seguridad**: versiones fijas en CDNs; Tailwind sin `crossorigin`.

## 9) Roadmap corto
1) SRI en CDNs (excepto Tailwind CDN script sin `crossorigin`).
2) Exportaciones (Excel/PDF).
3) Optimización en datasets grandes (mejoras de filtro/render).
