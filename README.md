# Dashboard Académico - IE El Carmen

![Escudo IE El Carmen](escudo-el-carmen.jpg)

## Descripción

Este proyecto es un **Dashboard Académico Institucional** interactivo diseñado para facilitar el análisis y la visualización de las notas de los estudiantes de la Institución Educativa El Carmen. La aplicación permite a los docentes y directivos cargar un archivo de Excel con las calificaciones y obtener de forma inmediata un panorama completo del rendimiento académico.

La herramienta está construida como una aplicación web de una sola página (`Single Page Application`) y se ejecuta completamente en el navegador, sin necesidad de un servidor o conexión a internet una vez cargada.

## Características Principales

- **Carga de Archivos:** Soporta la carga de archivos de Excel (`.xlsx`, `.xls`) y CSV.
- **Análisis Multi-hoja:** Cada hoja de cálculo en el archivo de Excel se importa como un "curso" independiente, permitiendo consolidar datos de múltiples grupos.
- **Visualización de Datos:**
    - **Tablas Detalladas:** Muestra las notas por estudiante, asignatura y área, con filtros dinámicos.
    - **Gráficos Interactivos:** Incluye gráficos de barras, pastel y radar para visualizar distribuciones y promedios.
    - **KPIs (Indicadores Clave):** Presenta resúmenes del promedio general, distribución de estados académicos (Ganado, En Riesgo, Perdido, etc.) y áreas con mayor dificultad.
- **Cálculos Automáticos:**
    - Calcula el promedio actual de los estudiantes.
    - Proyecta la nota mínima requerida en el último periodo para aprobar.
    - Asigna un "estado académico" a cada estudiante para una fácil identificación.
- **Reportes Rápidos:** Genera listas automáticas para identificar:
    - Estudiantes con promedios más bajos.
    - Estudiantes con más áreas perdidas o en riesgo.
    - Mejores y peores desempeños globales.
- **Persistencia de Datos:** Guarda los datos cargados en la memoria del navegador (`localStorage`) para que la información esté disponible en futuras visitas sin necesidad de volver a cargar el archivo.
- **Interfaz Moderna:** Desarrollada con un diseño limpio y responsivo, accesible desde computadoras de escritorio y dispositivos móviles.

## Tecnologías Utilizadas

- **HTML5**
- **CSS3** con **Tailwind CSS** para un diseño rápido y moderno.
- **JavaScript (ES6+)**
- **React.js** para la construcción de la interfaz de usuario interactiva.
- **Chart.js** para la generación de gráficos dinámicos.
- **SheetJS (xlsx)** para la lectura y procesamiento de archivos de Excel.

## ¿Cómo Utilizar?

1.  Abre el archivo `index.html` en un navegador web moderno (como Google Chrome, Firefox, o Edge).
2.  Arrastra y suelta el archivo de Excel con las notas en el área indicada, o haz clic en "Seleccionar archivo".
3.  Una vez procesado, el dashboard mostrará automáticamente los análisis y gráficos.
4.  Utiliza los filtros y las pestañas para explorar los datos en detalle.

## Autor

Desarrollado para la **IE El Carmen** como una herramienta de apoyo a la gestión académica.
