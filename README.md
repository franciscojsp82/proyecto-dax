# Proyecto DAX — Modo Oscuro (Power BI)

Reporte de ventas en Power BI construido sobre el dataset de ejemplo **Contoso**, con un tema oscuro personalizado y un set de medidas DAX que cubre agregaciones, `CALCULATE`, inteligencia de tiempo (YTD, MTD, año anterior, mes anterior), rankings con `RANKX` y títulos dinámicos.

> Los datos de ventas corresponden a los años **2019, 2020 y 2021** (el calendario cubre 2017–2023).

## Estructura del repositorio

Este proyecto está guardado en formato **Power BI Project (PBIP)**: todo es texto (TMDL + JSON), así que los cambios se pueden revisar en GitHub línea por línea.

```
├── ProyectoDAX.pbip                  ← abrir este archivo con Power BI Desktop
├── ProyectoDAX.Report/               ← reporte (páginas, visuales, marcadores, tema ModoOscuro)
├── ProyectoDAX.SemanticModel/        ← modelo semántico en TMDL
│   └── definition/
│       ├── tables/                   ← una tabla por archivo (columnas, medidas DAX, consultas M)
│       ├── relationships.tmdl
│       └── expressions.tmdl          ← parámetro RutaDatos
└── data/                             ← datos fuente
    ├── DimCalendar.csv
    ├── DimChannel.csv
    ├── DimProduct.csv
    ├── DimPromotion.csv
    ├── DimStores.csv
    └── FactSales.parquet             ← 2,28 millones de filas
```

## Páginas

La primera página, **Resumen General**, muestra los KPIs principales (ingresos, año anterior, variación, órdenes y % de devoluciones), la tendencia mensual frente al año anterior, los ingresos por categoría, continente y canal, y el ranking de tiendas. Las demás páginas desarrollan cada grupo de medidas DAX y terminan en **Comparativa LY**.

## Modelo de datos

Esquema estrella con `FactSales` al centro y las dimensiones `DimCalendar` (marcada como tabla de fechas), `DimChannel`, `DimProduct`, `DimPromotion` y `DimStores`. Todas las medidas están en la tabla `Medidas DAX`.

| Grupo | Medidas |
|---|---|
| Cantidades | Cantidad Ventas, Cantidad Devoluciones, Cantidad Total, Ratio Devoluciones |
| Conteos | Total Ordenes, Total Ordenes Devueltas, Cantidad Tiendas, Cantidad Regiones… |
| Ingresos | Total Ingresos, Total Ingresos AD (antes de descuento), PU Promedio |
| Inteligencia de tiempo | YTD Ingresos, MTD Ingresos, Total Ingresos LY, Total Ingresos LM, Total Ingresos Var LY |
| Rankings | Rank Ingresos Tiendas, Rank Ingresos Stores, Rank Ingresos Tiendas Cat (⭐) |
| Títulos dinámicos | Título Ingresos, Título Devoluciones, Título Filtros, Título Ingresos Var LY |

## Cómo abrirlo

1. Clona o descarga el repositorio, por ejemplo en `C:\ProyectoDAX`.
2. Abre `ProyectoDAX.pbip` con Power BI Desktop (versión reciente).
3. Si clonaste en otra carpeta: **Transformar datos → Editar parámetros → RutaDatos** y escribe la ruta a la carpeta `data` (ej. `D:\repos\ProyectoDAX\data`).
4. Clic en **Actualizar** para cargar los datos.

> Si Power BI Desktop pide habilitar el formato TMDL, actívalo en *Archivo → Opciones → Características de vista previa → "Almacenar el modelo semántico usando el formato TMDL"*.

Para obtener un `.pbix`, usa **Archivo → Guardar como** después de actualizar.
