# coipo_gestion_flota_vehiculos — Maqueta del Sistema Nacional de Gestión de Flota

Maqueta de validación del sistema que reemplazará a GESAD para administrar el pool de
vehículos de CONAF: solicitud y autorización de salidas a terreno, asignación de patente
y conductor, control de caución y licencia (Decreto Ley N° 799), mantenciones,
vencimientos legales y combustible. Requerimiento de la Sección Servicios Generales
(GEFA), elaborado por la Unidad de Información y Análisis (UIA).

**Ver la maqueta:** https://alvarozvjac.github.io/coipo_gestion_flota_vehiculos/

> Demostración no operacional. Los vehículos y sus vencimientos son datos reales de
> Oficina Central (planilla de mantenciones al 28-09-2026), con los números de motor y
> chasis enmascarados. Personas, RUT, pólizas y cargas de combustible son ficticios
> (fecha simulada: 22-10-2026) y nada se envía a un servidor. La maqueta sirve para
> validar el flujo y el alcance con la contraparte y el Departamento de Informática.

## Cómo probarla

El selector **«Ver como»** de la cabecera cambia entre los cinco perfiles del ERS. Desde la versión 0.3 la navegación se ordena por tareas y no por las pantallas de GESAD: cada perfil ve sólo lo que usa, y el detalle de una salida, un vehículo o un conductor se abre en un panel lateral.

| Perfil | Menú | Qué se puede probar |
|---|---|---|
| Funcionario solicitante | Nueva solicitud · Mis salidas | Solicitud con revisión automática (días inhábiles DL 799, relevo sobre 400 km diarios, capacidad, conductor habilitado) y seguimiento |
| Jefatura directa | Por aprobar · Salidas de mi equipo | Definir la imputación presupuestaria (folio) y aprobar, observar o rechazar con comentario; historial del equipo |
| Encargado de vehículos | Hoy · Salidas · Flota · Conductores · Combustible y gastos · Reportes | Ver detalle abajo |
| Conductor | Mis viajes | Registrar la salida y el regreso del vehículo, con odómetro, combustible e inventario |
| Administrador nacional | Lo mismo que el encargado, más Configuración | Catálogos, usuarios y accesos, cierre mensual, calidad de datos, traspasos y auditoría |

Lo que ve el encargado de vehículos, y qué función de GESAD reemplaza cada parte:

| Menú | Contenido | Reemplaza en GESAD |
|---|---|---|
| Hoy | Pendientes del día (asignar, entregar, recibir, novedades mecánicas), próximos vencimientos y **cierre de jornada del libro de guardia** | Salidas del día, Guarde de vehículos, Movimiento diario |
| Salidas | Lista única con filtros (por asignar, próximas, en terreno, finalizadas) o vista de calendario. Desde el detalle se asigna, se entrega y se recibe el vehículo, con **inventario de accesorios** al entregar y al recibir | Ingreso de solicitudes, Consulta de salidas, Consulta por conductor y por pasajeros |
| Flota | **Hoja de vida** de cada vehículo: documentos, mantención (órdenes de trabajo y cierre con factura), combustible, gastos, **accidentes**, inventario, libro de guardia y salidas | Ficha de vehículos, Seguros, Accidentes de tránsito, Ubicación, Mantenciones, Ficha de taller, Orden de trabajo |
| Conductores | Padrón con caución y licencia; los bloqueados no aparecen en las asignaciones | Conductores, Ficha de conductores |
| Combustible y gastos | Cargas, **importación validada del archivo COPEC**, compras a granel y gastos por documento (factura o boleta) | Carga archivo Copec, Ingreso combustible en efectivo, Compra a granel, Ingreso de gastos |
| Reportes | Kilómetros y costos, **Tesorería** (Excel mensual o anual), operatividad mensual, rendimiento de combustible y gastos por vehículo | Reportes de consumo, rendimiento, gastos y operatividad mensual |

Para ver el flujo completo: en **Hoy**, asigne la solicitud **OC-2026-000410** (el camión FXHB-90 queda descartado por su revisión técnica vencida). Luego entregue **OC-2026-000408** en «Salidas → Próximas» desmarcando un accesorio y recíbala marcando «Hubo un accidente»: se abre el registro del accidente en la hoja de vida del vehículo.

## Análisis de GESAD

Antes de diseñar el nuevo sistema, la UIA analizó GESAD, el sistema que hoy registra las salidas de vehículos y que dejará de operar a fines de 2026. El análisis se hizo con la base de datos, el código fuente y el menú que entregó el Departamento de Informática en respuesta al Memorándum N° 5772/2026.

- [Análisis de GESAD](docs/gesad/analisis-gesad.md): uso real del sistema, dependencias con otros sistemas, datos sensibles, calidad de datos, funciones que el ERS no menciona, antecedentes pendientes y el reporte para Tesorería que reemplaza la conexión con viáticos.
- [Diccionario de datos](docs/gesad/diccionario-datos.md): 77 tablas con columnas, tipos, claves y número de filas, sin registros.
- [Inventario de programas](docs/gesad/inventario-programas.md): menú del sistema y los 108 formularios y reportes, con las tablas que usa cada uno.
- [Lector del respaldo](herramientas/README.md): script que convierte el respaldo Oracle a CSV.

> El respaldo de la base de datos y los datos extraídos contienen datos personales y no se publican en este repositorio.

## Contenido del repositorio

- `index.html`: la maqueta completa en un solo archivo (código y estilos incluidos). Es
  la versión publicada en GitHub Pages (v0.3, navegación por tareas).
- `banner-gefa.jpg` y `banner-gefa-corto.jpg`: banners de la Gerencia de Finanzas y
  Administración, tomados de `identidad/` de coipo_master_produccion.
- `.nojekyll`: indica a GitHub Pages que publique los archivos sin procesarlos.
- `docs/gesad/`: análisis de GESAD (ver sección anterior).
- `herramientas/`: script lector del respaldo de GESAD.
- `.gitignore`: impide versionar el respaldo y los CSV con datos personales.

Documento de referencia: Informe Técnico y Especificación de Requerimientos de Software
INF-LOG-TI-2026-V1 (Departamento de Servicios y Logística, 15-10-2026), con el Prototipo
Pool de Vehículos V7 y los comprobantes de salida de GESAD. Estándar de interfaz:
`identidad/ESTANDAR_UI.md` de coipo_master_produccion.
