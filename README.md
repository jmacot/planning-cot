# Analizador de Planning COT

Herramienta para analizar el planning mensual del servicio de COT, desglosando actividades, estadisticas y retribucion por cirujano.

## Acceso directo
[Abrir la aplicacion](https://jmacot.github.io/planning-cot/)

## Funcionalidades
- Sube el archivo del planning (Excel, ODS, CSV) y analiza automaticamente
- Calendario mensual con etiquetas de actividad por dia
- Festivos oficiales de Andalucia y Sevilla 2026 marcados con gradiente
- Separacion visual entre actividades de manana y tarde
- Resumen de actividades con toggle Mes actual / Total
- Contaje de turnos semanal y mensual
- 9 categorias: Guardia, Saliente, Localizado, Quirofano M/T, Consulta M/T, Diferida, Gestion, RUCOT
- Dashboard de graficos: distribucion agregada, comparador por unidad, rankings
- Grafico radar: perfil del cirujano vs media del servicio (mensual y total)
- Grafico Manana vs Tarde: porcentaje de actividad matutina vs vespertina por cirujano
- Grafico Festivos Trabajados: festivos oficiales y fines de semana trabajados
- Percentiles del cirujano respecto a todos y respecto a su unidad (10 metricas) con tooltips explicativos
- Rankings de guardias, localizados, gestion y turnos totales
- Retribucion: contaje, bruto y neto de guardias y localizados (17h/24h)
- Enlace directo a Calculadora de Guardias con datos pre-rellenados
- Exportar calendario .ics (mes actual o todos los meses) compatible con Google Calendar, Apple Calendar y Outlook
- Exportar PDF programatico con calendario visual, listado dia a dia y estadisticas completas
- Modo oscuro automatico
- Responsive para movil

## Tecnologia
- HTML5, CSS3 y JavaScript puro
- Chart.js 4.4.7 para graficos
- jsPDF 2.5.1 para exportacion PDF
- Tipografias: Inter, Lora (Google Fonts)
- SheetJS (xlsx.js) para parseo de archivos
- Sin frameworks, sin dependencias adicionales

## Licencia
MIT
