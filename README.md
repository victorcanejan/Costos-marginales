# Proyecto de Predicción de Precios de Electricidad en EE.UU.
## Estudiantes: Fernando Sepúlveda - Víctor Canejan

## Descripción
Este proyecto implementa un modelo de regresión lineal para predecir precios de electricidad utilizando datos históricos de EE.UU. (2001-2024). El análisis incluye EDA, preprocesamiento y evaluación del modelo.

## Dataset
**Archivo:** `us_electricity_prices.csv`  
**Variables relevantes:**
- `year`, `month`: Variables temporales
- `stateDescription`: Estado (categórica)
- `sectorName`: Sector de consumo (categórica) 
- `price`: Variable objetivo (precio por kWh)
- `sales`, `revenue`: Variables numéricas

## Metodología

### 1. Análisis Exploratorio
- Distribución de precios por estado y sector
- Análisis de valores faltantes y atípicos
- Matriz de correlación entre variables

### 2. Preprocesamiento
- Codificación one-hot para variables categóricas
- Creación de variable estacional (verano/invierno)
- Normalización de features numéricas

### 3. Modelado
**Algoritmo:** Regresión Lineal  
**Validación:** 
- Split 70-30 (train-test)
- 5-fold cross validation

## Resultados

### Métricas de Rendimiento
| Métrica | Valor |
|---------|-------|
| RMSE | 1.85 |
| MAE | 1.42 |
| R² | 0.76 |

### Hallazgos Clave
- Coeficiente positivo para meses de verano (+0.15)
- Sector residencial con mayor impacto en precio
- Hawaii muestra el coeficiente estatal más alto

## Conclusiones
El modelo de regresión lineal explica el 76% de la varianza en los precios (R²=0.76). Los resultados muestran patrones esperados como precios más altos en verano y variaciones significativas entre estados.

## Ejecución
```bash
pip install -r requirements.txt
jupyter notebook analysis.ipynb
