# Business Data Analytics Applied Lab #1 — Restaurant Analytics (Semana 2)

**Asignatura:** Data Analytics (Código: 43390860)
**Tema:** Perfil del analista, modelo relacional y trabajo reproducible

## Objetivo

Consolidar cuatro fuentes de datos independientes de una cadena de restaurantes (productos, clientes y ventas de dos semanas) para construir indicadores que apoyen decisiones sobre el menú y la fidelización de clientes. El análisis se centra en **ingresos, frecuencia de compra y recurrencia de clientes**, ya que los archivos disponibles no contienen costos, cantidades ni descuentos y por tanto no permiten calcular rentabilidad, utilidad o margen.

## Archivos utilizados

```text
lab-restaurant/
│
├── data/
│   ├── Restaurant-Foods.csv          # Catálogo de productos y precios
│   ├── Restaurant-Customers.csv      # Información de clientes
│   ├── Restaurant-Week1-Sales.csv    # Registros de venta - semana 1
│   └── Restaurant-Week2-Sales.csv    # Registros de venta - semana 2
│
├── lab_Sem2_DA.ipynb                 # Notebook ejecutado con el análisis
└── README.md
```

**Relaciones entre tablas:**
- `Food ID` conecta `foods` con los registros de venta (1 producto : N ventas).
- `Customer ID` / `ID` conecta `customers` con los registros de venta (1 cliente : N ventas).
- Cada registro de venta referencia un único cliente y un único producto.

> Por privacidad, el archivo de clientes y los nombres de clientes no deben publicarse en un repositorio público.

## Instrucciones de ejecución

1. Clonar o descargar el repositorio y ubicar los cuatro archivos CSV dentro de la carpeta `data/`.
2. Abrir `lab_Sem2_DA.ipynb` en Jupyter Notebook, JupyterLab o Google Colab.
3. Instalar/verificar las dependencias necesarias: `pandas`, `sqlite3` (incluida en la librería estándar de Python) y `matplotlib`.
4. Ejecutar el notebook de principio a fin, en orden, sin modificar el código manualmente (salvo la carga inicial de archivos si se trabaja en Google Colab).
5. El notebook realiza, en orden:
   - Carga y unificación de las ventas de ambas semanas.
   - Validación de claves únicas y de referencias entre tablas.
   - Consolidación (`merge`) de ventas con productos y clientes usando `validate='many_to_one'`.
   - Cálculo de KPIs: ingresos totales, resumen semanal, frecuencia de compra y ranking de productos por ingresos.
   - Verificación cruzada de resultados con Pandas y con SQL (SQLite en memoria).
   - Generación de tres visualizaciones: frecuencia de compra vs. ingresos por producto, ingresos por semana, y una comparación combinada frecuencia/ingresos.
   - Cálculo de la tasa de recurrencia de clientes entre semanas e ingresos agregados por ocupación.

## Hallazgos principales

- **Popularidad vs. ingresos:** el producto con mayor frecuencia de compra es el **Burrito** (57 registros de venta), pero el que genera más ingresos es el **Steak** (1249.50), lo que muestra que ambas métricas deben analizarse por separado.
- **Comparación semanal:** el número de registros de venta se mantuvo estable (250 en cada semana), pero los ingresos totales bajaron levemente de 1962.68 (semana 1) a 1923.88 (semana 2), y el ingreso promedio por registro cayó de 7.85 a 7.70.
- **Recurrencia de clientes:** solo el **20.8 %** de los clientes de la semana 1 volvió a comprar en la semana 2, lo que indica una base de clientes mayormente ocasional.
- **Ocupaciones con mayor gasto acumulado:** Compensation Analyst (116.68), Sales Representative (104.18), Marketing Manager (99.40), Cost Accountant (80.21) y Assistant Media Planner (72.69).
- **Limitación de los datos:** con solo dos semanas de información y sin datos de cantidades, costos o descuentos, no es posible establecer causalidad ni hablar de rentabilidad; los hallazgos describen asociaciones observadas, no relaciones causa-efecto.
- **Recomendación priorizada:** implementar una estrategia de seguimiento o incentivo (p. ej., cupón de regreso o programa de fidelización) dirigida a los clientes de la semana 2, para aumentar la tasa de recurrencia y generar datos suficientes para futuras mediciones.
