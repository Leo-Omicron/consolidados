# Conocimientos Consolidados - Dashboard Académico IE El Carmen

## 📋 Información General del Proyecto

### Descripción
Dashboard web para análisis de notas académicas del IE El Carmen. Permite importar archivos Excel multi-hoja, procesar datos de estudiantes y generar visualizaciones interactivas con métricas académicas en tiempo real.

### Tecnologías Principales
- **Frontend**: React 18.2.0 (UMD), HTML5, CSS3, JavaScript ES6+
- **Estilos**: Tailwind CSS con dark mode
- **Gráficos**: Chart.js 4.4.4 (barras, donut, radar)
- **Procesamiento**: SheetJS/XLSX 0.18.5
- **Transpilación**: Babel Standalone
- **Arquitectura**: SPA monolítica en un solo archivo HTML

### Estructura del Proyecto
```
consolidados/
├── index.html          # Aplicación completa (3000+ líneas)
├── conocimientos.md    # Este archivo
├── README.md           # Documentación principal
├── SPEC.md            # Especificaciones técnicas
└── escudo-el-carmen.jpg # Logo institucional
```

## 🚀 Funcionalidades Principales

### Sistema de Importación
- **Multi-formato**: Soporte para .xlsx, .xls, .csv
- **Multi-hoja**: Cada hoja Excel se importa como curso independiente
- **Validación robusta**: 
  - Tamaño máximo: 15MB
  - Validación de tipos MIME y extensiones
  - Verificación de estructura de datos
- **Procesamiento inteligente**:
  - Normalización automática de encabezados
  - Forward-fill para áreas y asignaturas
  - Síntesis de DEF para áreas unitarias
  - Manejo de notas fuera de rango (0-5)

### Análisis de Datos
- **Cálculos automáticos**:
  - Promedio actual por estudiante/área/asignatura
  - P4 mínima para aprobar (regla: 12 - suma(P1+P2+P3))
  - Estados académicos: Perdido, En riesgo, Recuperable, Ganable, Ganado
- **Métricas avanzadas**:
  - Promedio general institucional
  - Distribución de estados por porcentaje
  - Áreas con mayor riesgo académico
  - Análisis comparativo por cursos

### Visualizaciones Interactivas
- **Gráficos modernos**:
  - Barras: Distribución de estados académicos
  - Donut: Proporción de estudiantes por estado
  - Radar: Promedio por área académica
- **Tablas dinámicas**:
  - Análisis por área (vista DEF consolidada)
  - Análisis por asignatura (vista detallada P1/P2/P3)
  - Paginación automática (50 filas por página)
  - Ordenamiento y filtrado avanzado

### Sistema de Filtros Avanzados
- **Filtros persistentes** (localStorage):
  - Por curso (multi-curso)
  - Por estudiante (búsqueda + selección)
  - Por área académica
  - Por asignatura específica
  - Por estado académico
- **Búsqueda inteligente**:
  - Debounced inputs (300ms)
  - Normalización de texto (sin acentos)
  - Búsqueda parcial case-insensitive

### Sistema de Temas
- **Dark/Light mode**:
  - Toggle visual en header (sol/luna)
  - Persistencia en localStorage
  - Transiciones suaves entre temas
  - Soporte completo en gráficos Chart.js
  - Modo responsivo para móviles

## 🔧 Características Técnicas Avanzadas

### Optimización de Performance
- **React.memo** en componentes pesados:
  - `DashboardCharts`: Comparación granular de props
  - `QuickReportsView`: Memoización de cálculos
  - `AsignaturaTableRow` / `AreaTableRow`: Optimización de renders
- **Estado derivado pre-calculado**:
  - `buildDerived()`: Procesa datos una vez, reutiliza múltiples veces
  - Índices normalizados para búsquedas rápidas
  - KPIs globales cached

### Gestión de Estado
- **Persistencia completa**:
  - Cursos cargados en `localStorage`
  - Filtros aplicados
  - Configuraciones de UI (pestañas, tema, etc.)
- **Estado elevado (Lifted State)**:
  - Filtros compartidos entre componentes
  - Sincronización de gráficos opcional
  - Navegación de pestañas persistente

### Manejo de Errores Robusto
- **ErrorBoundary con reintento suave**:
  - Captura errores de render React
  - UI de recuperación sin reload completo
  - Logging condicional en modo desarrollo
- **Filtrado de ruido externo**:
  - Silencia errores de extensiones del navegador
  - Configurable por usuario
  - Conserva errores reales de la aplicación

### Accesibilidad (A11y)
- **Navegación por teclado**:
  - Tabs: ←/→ para navegar, Home/End para ir a extremos
  - Enter/Space para activar
- **ARIA completo**:
  - `role="tab"`, `role="tabpanel"`
  - `aria-selected`, `aria-controls`, `aria-labelledby`
  - `aria-live` para actualizaciones dinámicas
- **Elementos semánticos**:
  - `<main>`, `<section>`, `<caption>` en tablas
  - Labels descriptivos en formularios

### Sistema de Exportación
- **Múltiples formatos**:
  - **CSV**: Tablas filtradas con columnas seleccionables
  - **PNG**: Gráficos de Chart.js en alta resolución
  - **JSON**: Backup completo del estado (datos + configuración)
- **Nombres automáticos**: Incluyen fecha ISO y contexto
- **Restauración completa**: Desde archivos JSON de backup

## 📊 Estructura de Datos

### Formato de Entrada (Excel)
```
Fila 1 (Áreas):     [No, Nombre, MATEMATICAS, MATEMATICAS, ..., INGLES, INFORMATICA]
Fila 2 (Asignaturas): [No, Nombre, ALGEBRA, GEOMETRIA, ..., INGLES, INFORMATICA]  
Fila 3 (Componentes): [No, Nombre, P1, P2, P3, P1, P2, P3, ..., P1, P2, P3]
Fila 4+ (Datos):    [1, "ESTUDIANTE A", 4.5, 4.0, 3.8, 3.9, ...]
```

### Estructura Interna Procesada
```javascript
// Estudiante procesado
{
  id: "1",
  name: "ESTUDIANTE A", 
  CURSO: "GRADO_11A",
  areas: {
    "MATEMATICAS": {
      DEF: { P1: 4.2, P2: 4.1, P3: 4.0 },
      areaStats: { 
        promedioActual: 4.10, 
        p4Min: 0.70, 
        estado: { text: "Ganado", color: "green" }
      },
      asignaturas: {
        "ALGEBRA": { P1: 4.5, P2: 4.0, P3: 3.8, promedioActual: 4.10, p4Min: 0.70, estado: {...} },
        "GEOMETRIA": { P1: 3.9, P2: 3.8, P3: 3.7, promedioActual: 3.80, p4Min: 1.40, estado: {...} }
      }
    }
  }
}
```

## 🎯 Patrones de Desarrollo

### Componentes Principales
```javascript
// Contenedor principal con gestión de estado
<DashboardTabs> 
  ├── <DashboardView>     // Tablas de análisis
  ├── <DashboardCharts>   // Visualizaciones 
  └── <QuickReportsView>  // Reportes rápidos

// Componentes optimizados para tablas grandes
<AsignaturaTableRow>  // Memoizado por fila individual
<AreaTableRow>        // Comparación optimizada de props
```

### Hooks Personalizados Clave
```javascript
// Debounced input para búsquedas
const DebouncedInput = ({ value, onChange, wait = 300 }) => {
  const [localValue, setLocalValue] = useState(value);
  const debouncedOnChange = useMemo(() => debounce(onChange, wait), [onChange, wait]);
  // ...
};

// Sistema de tooltips informativos
const Tooltip = ({ children, content, position = 'top' }) => {
  const [isVisible, setIsVisible] = useState(false);
  // ...
};
```

### Utilidades de Procesamiento
```javascript
// Normalización de notas (manejo de 0.0)
function notaFromCell(v) {
  if (v === null || v === undefined) return 0.0;
  // Convierte texto a número, valida rango 0-5
  const n = parseFloat(String(v).replace(',', '.'));
  return Number.isFinite(n) ? Math.max(0, Math.min(5, n)) : null;
}

// Cálculo de estado académico
const getStatus = (p4Min) => {
  if (p4Min >= 5.0) return { text: 'Perdido', color: 'red' };
  if (p4Min >= 4.0) return { text: 'En riesgo', color: 'yellow' };
  if (p4Min >= 3.0) return { text: 'Recuperable', color: 'blue' };
  if (p4Min >= 1.0) return { text: 'Ganable', color: 'cyan' };
  return { text: 'Ganado', color: 'green' };
};
```

## 🔒 Seguridad y Validación

### Validación de Archivos
- **Tamaño**: Máximo 15MB
- **Tipos**: .xlsx, .xls, .csv únicamente
- **Estructura**: Verificación de 3 filas de encabezados + datos
- **Contenido**: Validación de rangos de notas (0-5)

### Manejo Seguro de Datos
- **Sanitización**: Normalización de texto y caracteres especiales
- **Validación de tipos**: Verificación de numbers vs strings
- **Manejo de nulos**: Tratamiento específico de celdas vacías
- **Escape de CSV**: Manejo correcto de comillas y separadores

## 📱 Responsividad y UX

### Breakpoints
- **Móvil**: < 768px (sm:)
- **Tablet**: 768px - 1024px (md:)  
- **Desktop**: > 1024px (lg:)

### Adaptaciones Móviles
- **Tablas**: Scroll horizontal automático
- **Filtros**: Stack vertical en móvil
- **Gráficos**: Redimensionamiento automático
- **Loading**: Overlays adaptados al tamaño de pantalla

## 🚀 Despliegue y Configuración

### Modo Desarrollo vs Producción
```javascript
// Control por URL params
?mode=dev   // Fuerza desarrollo
?mode=prod  // Fuerza producción

// O por variable global
window.__PROD__ = true/false;
window.__DASH_DEV__ = true;  // Debug adicional
```

### GitHub Pages
- **URL**: https://leo-omicron.github.io/consolidados/
- **Rama**: Main/DEV según configuración
- **Build**: Automático al push
- **CDNs**: URLs fijas versionadas para estabilidad

### Variables de Entorno
```javascript
const CONFIG = {
  MODE: window.__PROD__ ? 'production' : 'development',
  DEBUG: !window.__PROD__ && window.__DASH_DEV__,
  VERSION: '2.1.0',
  CDN_TIMEOUT: 10000
};
```

## 🔄 Flujo de Trabajo Recomendado

### Desarrollo Local
1. **Live Server**: http://127.0.0.1:5500/index.html
2. **Modo debug**: `window.__DASH_DEV__ = true` en console
3. **Hot reload**: Cambios en tiempo real
4. **Testing**: Archivos Excel de muestra

### Control de Versiones
```bash
# Ramas principales
main    # Producción estable
DEV     # Desarrollo activo
REV     # Revisiones y features

# Flujo sugerido
git checkout DEV
# ... hacer cambios
git add . && git commit -m "feat: nueva funcionalidad"
git push origin DEV

# Para promocionar a producción
git checkout main
git merge DEV
git push origin main
```

### Testing Manual
- **Archivos grandes**: >1000 estudiantes
- **Múltiples hojas**: 3+ cursos simultáneos
- **Datos edge case**: Notas nulas, fuera de rango
- **Performance**: Filtros con datasets grandes
- **Navegadores**: Chrome, Firefox, Safari, Edge

## 🐛 Troubleshooting Común

### Problemas de Carga
```javascript
// Error: "Tailwind no se aplicó"
// Solución: Verificar CDN o usar fallback
const fallbackCSS = `
  .hidden { display: none !important; }
  .p-4 { padding: 1rem; }
  // ... estilos críticos
`;
```

### Errores de Datos
```javascript
// Error: "Nota fuera de rango"
// Causa: Valores > 5.0 o < 0.0 en Excel
// Solución: notaFromCell() normaliza automáticamente

// Error: "Estudiante duplicado"  
// Causa: Mismo nombre en múltiples filas
// Solución: Se procesa pero genera warning
```

### Performance Issues
```javascript
// Síntoma: Lag en filtros
// Solución: Activar debouncing
wait = 500; // ms para inputs pesados

// Síntoma: Renders excesivos
// Verificar: React DevTools Profiler
// Solución: Más React.memo específicos
```

## 📈 Métricas y Monitoreo

### KPIs Principales
- **Promedio general**: Media aritmética de todas las áreas DEF
- **Distribución de estados**: % de estudiantes por categoría
- **Áreas de riesgo**: Top áreas con mayor reprobación
- **Tendencias**: Comparación P1 vs P2 vs P3

### Logging
```javascript
// Desarrollo
console.time('render:ComponentName');
console.timeEnd('render:ComponentName');

// Producción
window.__DASH_DEV__ && console.log('[DEBUG]', data);
```

## 📚 Referencias y Documentación

### APIs Externas
- [React 18 Docs](https://react.dev/)
- [Chart.js Documentation](https://www.chartjs.org/docs/)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [SheetJS Community Edition](https://docs.sheetjs.com/)

### Patrones Implementados
- **Compound Components**: Tabs + TabPanels
- **Render Props**: StatusBadge con lógica de color
- **Higher-Order Components**: React.memo wrappers
- **Custom Hooks**: useDebounce, useLocalStorage (implícito)

### Estándares de Código
- **Naming**: camelCase para variables, PascalCase para componentes
- **Comments**: JSDoc para funciones complejas
- **File Structure**: Componentes arriba, utilities abajo
- **Performance**: React.memo obligatorio para listas grandes

---

**Última actualización**: Enero 2025  
**Versión del proyecto**: 2.1.0  
**Compatibilidad**: Navegadores modernos (ES6+ support)