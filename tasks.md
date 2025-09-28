# tasks.md — Guía de Prompts Atómicos para el Agente (VS Code)

## Reglas para el Agente
- Cambios **solo** en `index.html`.
- Una instrucción a la vez; esperar confirmación humana.
- Mantener comentarios de trazabilidad (`[Fix-CURSO]`, `[NotesZero]`, `[ChartsSync]`, `[A11yTabs]`, `[OverlayPhase]`, `[ErrorBoundary]`, `[SafeProcess]`, `[ResourceGuard]`).
- No introducir nuevas dependencias ni crear archivos (salvo actualizar este `tasks.md` si procede).

---

## HITO 1 – Estabilidad base (completado)
### A — Hotfix spread del selector de cursos (si aparece)
**Prompt:**  
> Abre `index.html` y reemplaza cualquier `['ALL', .Array.from(` por `['ALL', ...Array.from(` sin tocar nada más.

### B — Flag DEV + DBG + profiling seguro
**Prompt:**  
> Inserta al inicio del primer `<script type="text/babel">` el bloque que define `window.__DASH_DEV__`, `DBG(...)` y el parche de `console.time/timeEnd` seguro. No modifiques otras partes.

---

## HITO 2 – Dev/Prod + versiones fijas (parcial)
### C — Switch Dev/Prod síncrono
**Prompt:**  
> En `<head>`, antes de Babel, inyecta React/ReactDOM UMD de forma **sincrónica** con `document.write`, derivando URLs `production.min.js` cuando `?mode=prod` o `window.__PROD__=true`. Deja los `<script>` originales comentados como backup.

### C2 — Modo global determinista
**Prompt:**  
> En `<head>`, añade script que fija `window.__PROD__` desde `?mode=prod|dev` y setea `data-mode` en `<html>`.

### D — Versiones fijas y CORS
**Prompt:**  
> Fija versiones en React/ReactDOM/Chart.js/XLSX. Añade `crossorigin="anonymous"` a los CDNs que lo soporten; **no** añadir `crossorigin` a `cdn.tailwindcss.com`.

---

## HITO 3 – UX Gráficos (completado)
### E1 — Toggle “Sincronizar con filtros”
**Prompt:**  
> Añade `syncChartsWithFilters` con persistencia en `localStorage`, el checkbox en la pestaña **Gráficos** y pasa `rowsArea/rowsAsignatura` filtrados cuando está activo.

### E2 — Texto de ayuda alineado a la derecha
**Prompt:**  
> Bajo el toggle, añade `<p className="mt-2 text-xs text-gray-600 text-right max-w-md ml-auto">...</p>`.

---

## HITO 4 – Rendimiento & A11y (completado)
### F1 — Normalización de filtros
**Prompt:**  
> Declara `normTxt` (lowercase+sin tildes) y úsala en filtros.

### F2 — Campos `*_NORM` precomputados
**Prompt:**  
> En el `map` de aplanado, agrega `CURSO_NORM/AREA_NORM/ASIG_NORM/EST_NORM`.

### F3 — Usar `*_NORM` en filtros
**Prompt:**  
> Cambia predicados para usar `*_NORM`; normaliza entradas del usuario solo una vez.

### G — A11y en tabs (teclado)
**Prompt:**  
> Añade handler de teclas en `tablist` (←/→, Home/End) y `tabIndex` controlado en cada tab.

---

## Salvaguardas (implementadas)
### ErrorBoundary
**Prompt:**  
> Declara `<AppErrorBoundary>` y envuelve `<App />` en el render raíz.

### Safe Process
**Prompt:**  
> Envuelve el flujo de `Procesar` en `try/catch/finally`; asegura `setProcessingPhase('')` y ocultar overlay siempre, con banner ante errores.

### ResourceGuard
**Prompt:**  
> Inserta script en `<head>` para registrar fallos de recursos y mostrar aviso discreto.

---

## Próximos hitos sugeridos
- **SRI**: añadir `integrity` donde los CDNs lo soporten (mantener Tailwind sin `crossorigin`).
- **Exportaciones**: CSV/Excel/PDF desde los derivados (sin librerías nuevas).
- **Rendimiento**: memoización de cálculos y/o virtualización de tablas en datasets muy grandes.

## Rollback rápido
- Revertir el último commit de la rama `DEV` o restaurar bloques previos comentados (carga React, etc.).
- Mantener un PR por bloque (release train) a `main`.
