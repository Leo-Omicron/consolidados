# Dashboard Académico - IE El Carmen

![Escudo IE El Carmen](escudo-el-carmen.jpg)

## Descripción

Este proyecto es un **Dashboard Académico Institucional** interactivo diseñado para facilitar el análisis y la visualización de las notas de los estudiantes de la Institución Educativa El Carmen. La aplicación permite a los docentes y directivos cargar un archivo de Excel con las calificaciones y obtener de forma inmediata un panorama completo del rendimiento académico.

La herramienta está construida como una aplicación web de una sola página (`Single Page Application`) y se ejecuta completamente en el navegador, sin necesidad de un servidor o conexión a internet una vez cargada.

## 🆕 **Sistema de Informes por Periodos** *(NUEVO)*

### 📊 **Funcionalidad Destacada**
El dashboard ahora incluye un **Sistema Completo de Informes de Rendimiento Escolar por Periodos** que permite:

- **📈 Análisis por Periodos**: Evaluación detallada de P1, P2, P3, P4 individual y acumulativa
- **📊 Múltiples Tipos de Informes**: Rendimiento estudiantil, bajo rendimiento, análisis comparativo y estadísticas consolidadas
- **📤 Exportación Profesional**: CSV, XLSX, PDF y JSON con plantillas institucionales
- **🧪 Sistema de Validación**: Diagnósticos automáticos y pruebas de integridad completas
- **⚡ Optimización Avanzada**: Algoritmos optimizados con indicadores de progreso en tiempo real
- **🎨 Interfaz Moderna**: Diseño intuitivo con filtros avanzados y visualización profesional

### 🚀 **Acceso Rápido**
1. Ir a la pestaña **"📊 Informes"** en la navegación superior
2. Seleccionar tipo de reporte deseado
3. Aplicar filtros según necesidades
4. Generar y exportar resultados

📋 **Documentación Completa**: [DOCUMENTACION_SISTEMA_INFORMES.md](DOCUMENTACION_SISTEMA_INFORMES.md)  
⚡ **Guía Rápida**: [GUIA_RAPIDA_INFORMES.md](GUIA_RAPIDA_INFORMES.md)

## Características Principales

### 🎯 **Gestión de Datos Avanzada**

-   **Carga Multi-formato:** Soporta Excel (`.xlsx`, `.xls`) y CSV con validación robusta
-   **Análisis Multi-hoja:** Procesamiento inteligente de múltiples hojas como cursos independientes
-   **Normalización Automática:** Sistema de limpieza y estructuración de datos con log de calidad
-   **Estados Derivados:** Pre-cálculo optimizado de `rowsArea` y `rowsAsignatura` para performance

### 📊 **Visualización y Análisis**

-   **Tablas Inteligentes:** Filtros dinámicos con persistencia y paginación optimizada
-   **Gráficos Interactivos:** Chart.js con exportación PNG y sincronización con filtros
-   **KPIs Dinámicos:** Indicadores en tiempo real que responden a filtros aplicados
-   **Sistema de Estados:** Clasificación automática (Ganado, Ganable, Recuperable, En Riesgo, Perdido)
-   **📊 Informes por Periodos:** Sistema completo de análisis académico temporal **(NUEVO)**

### 🔧 **Funcionalidades Avanzadas**

-   **Backup/Restore:** Sistema completo de exportación/importación JSON de estado
-   **Exportación Multi-formato:** CSV para tablas, PNG para gráficos, JSON para backups
-   **📤 Exportación Profesional:** Sistema avanzado de informes con plantillas institucionales **(NUEVO)**
-   **Modo Desarrollo/Producción:** Switch automático con `?mode=dev/prod`
-   **Filtros Persistentes:** Configuraciones guardadas en localStorage
-   **Consultas Rápidas:** Reportes automáticos para identificación de riesgos académicos
-   **🧪 Sistema de Validación:** Diagnósticos automáticos y herramientas de debugging **(NUEVO)**

### ♿ **Accesibilidad y UX**

-   **Navegación Accesible:** Soporte completo de teclado y ARIA
-   **Responsive Design:** Optimizado para escritorio, tablet y móvil
-   **Loading Inteligente:** Fases de procesamiento con feedback visual
-   **⚡ Indicadores de Progreso:** Barras de progreso en tiempo real para operaciones largas **(NUEVO)**
-   **Error Boundaries:** Recuperación automática de errores sin pérdida de datos
-   **Filtros de Ruido:** Silencia errores de extensiones externas automáticamente

## Tecnologías Utilizadas

-   **HTML5** con arquitectura SPA (Single Page Application)
-   **CSS3** con **Tailwind CSS** para diseño responsivo y moderno
-   **JavaScript (ES6+)** con módulos ES y programación funcional
-   **React.js 18.2.0** para interfaz de usuario reactiva con hooks avanzados
-   **Chart.js 4.4.4** para gráficos interactivos con exportación PNG
-   **SheetJS (xlsx) 0.18.5** para procesamiento robusto de archivos Excel y exportación avanzada
-   **Babel Standalone** para transpilación JSX en tiempo real
-   **Sistema de Estados Derivados** para optimización de performance
-   **Persistencia en localStorage** para mantener configuraciones del usuario

## ¿Cómo Utilizar?

1.  Abre el archivo `index.html` en un navegador web moderno (como Google Chrome, Firefox, o Edge).
2.  Arrastra y suelta el archivo de Excel con las notas en el área indicada, o haz clic en "Seleccionar archivo".
3.  Una vez procesado, el dashboard mostrará automáticamente los análisis y gráficos.
4.  Utiliza los filtros y las pestañas para explorar los datos en detalle.

## Autor

Desarrollado para la **IE El Carmen** como una herramienta de apoyo a la gestión académica.
