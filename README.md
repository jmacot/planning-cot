# Analizador de Planning COT

Herramienta para analizar el planning mensual del servicio de COT, desglosando actividades, estadisticas y retribucion por cirujano.

![HTML5](https://img.shields.io/badge/HTML5-single--file-E34F26?logo=html5&logoColor=white)
![D3.js](https://img.shields.io/badge/D3.js-v7-f9a03c?logo=d3dotjs&logoColor=white)
![Sin dependencias](https://img.shields.io/badge/dependencias-ninguna-grey)

---

## Acceso directo

[Abrir la aplicacion](https://jmacot.github.io/planning-cot/)

No requiere instalacion. Funciona en cualquier navegador, incluyendo movil y tablet.

---

## Funcionalidades

- **Sube el archivo del planning** (Excel, ODS, CSV) y analiza automaticamente
- **Calendario mensual** con etiquetas de actividad por dia y separacion visual manana/tarde
- **Festivos oficiales** de Andalucia y Sevilla 2026 marcados con gradiente
- **Resumen de actividades** con toggle Mes actual / Total
- **Contaje de turnos** semanal y mensual, descontando festivos de los turnos esperados
- **9 categorias**: Guardia, Saliente, Localizado, Quirofano M/T, Consulta M/T, Diferida, Gestion, RUCOT
- **Dashboard de graficos D3.js**: distribucion agregada, comparador por unidad, rankings
- **Comparador Interactivo**: slope chart y barras agrupadas para comparar cirujanos entre periodos
- **Grafico radar**: perfil del cirujano vs media del servicio (mensual y total)
- **Grafico Manana vs Tarde**: porcentaje de actividad matutina vs vespertina por cirujano
- **Grafico Festivos Trabajados**: festivos oficiales y fines de semana trabajados
- **Percentiles** del cirujano respecto a todos y respecto a su unidad (10 metricas) con tooltips explicativos
- **Rankings** de guardias, localizados, gestion y turnos totales
- **Retribucion**: contaje, bruto y neto de guardias y localizados (17h/24h)
- **Enlace directo** a Calculadora de Guardias con datos pre-rellenados via URL params
- **Exportar calendario .ics** (mes actual o todos los meses) compatible con Google Calendar, Apple Calendar y Outlook
- **Exportar PDF** programatico con calendario visual, listado dia a dia y estadisticas completas
- **Tap-to-expand**: calendario y graficas se expanden al pulsar en movil
- **Modo oscuro automatico** con deteccion por hora y sistema
- **Responsive** para movil con controles segmentados estilo iOS

---

## Tecnologia

- HTML5, CSS3 y JavaScript puro
- **D3.js v7** para graficos (barras horizontales/verticales, radar, apiladas, slope chart)
- jsPDF 2.5.1 para exportacion PDF
- Tipografias: Inter, Lora (Google Fonts)
- SheetJS (xlsx.js) para parseo de archivos
- Sin frameworks, sin dependencias adicionales

---

## Estructura del proyecto

```
planning-cot/
├── index.html        ← aplicacion principal
├── icon.png          ← icono de la app
├── .gitignore
├── LICENSE           ← MIT
└── README.md         ← este archivo
```

---

## Licencia

MIT
