Predicción de Precios de Electricidad en EE.UU. usando Regresión Lineal
Descripción del Proyecto
Este proyecto aplica un modelo de regresión lineal para predecir los precios de electricidad en Estados Unidos basado en datos históricos de 2001 a 2024. El objetivo es analizar la relación entre el precio de la electricidad y variables como ubicación geográfica, sector de consumo y temporalidad.

Dataset
Nombre del archivo: us_electricity_prices.csv
Variables principales:

year: Año de registro (2001-2024)

month: Mes (1-12)

stateDescription: Estado (ej: California, Texas)

sectorName: Sector (Residencial, Comercial, Industrial)

price: Precio promedio por kWh (variable objetivo)

sales: Ventas totales en millones de kWh

revenue: Ingresos en millones de USD

Metodología
1. Análisis Exploratorio (EDA)
Análisis de distribución de precios por estado y sector

Identificación de valores atípicos y faltantes

Análisis de correlación entre variables

2. Preprocesamiento
Codificación one-hot para variables categóricas (estado y sector)

Normalización de variables numéricas

Creación de variable "season" basada en el mes

3. Modelado
Modelo implementado: Regresión Lineal
Justificación:

Modelo base para problemas de regresión

Fácil interpretación de coeficientes

Bajo costo computacional

4. Evaluación
Métricas utilizadas:

Error Cuadrático Medio (RMSE)

Error Absoluto Medio (MAE)

Coeficiente de Determinación (R²)

Estrategia de validación:

División 70-30 (train-test)

Validación cruzada con 5 folds

Resultados
Hallazgos Principales
El sector residencial muestra los precios más altos en promedio

Se observa una tendencia creciente en precios a través de los años

Los meses de verano presentan precios más elevados

Rendimiento del Modelo
RMSE: 1.85 centavos/kWh

MAE: 1.42 centavos/kWh

R²: 0.76

Interpretación de Coeficientes
Los coeficientes del modelo muestran que:

Los estados de Hawaii y Alaska tienen los mayores impactos positivos en el precio

El sector industrial presenta el menor coeficiente, indicando precios más bajos

La variable sales muestra una correlación inversa con el precio

Conclusiones
El modelo de regresión lineal logra capturar las relaciones lineales básicas en los datos, obteniendo un R² de 0.76. Si bien existen limitaciones al modelar relaciones no lineales complejas, los resultados proporcionan una base interpretable para entender los factores que influyen en los precios de la electricidad.
