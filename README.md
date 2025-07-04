# Proyecto: Predicción del Costo Marginal en el Sistema Eléctrico Chileno

Estudiantes: Fernando Sepúlveda - Víctor Canejan

## Definición del problema

El sistema eléctrico chileno opera bajo un modelo de mercado en el que los costos marginales representan el precio de generar una unidad adicional de energía. Estos costos varían cada 15 minutos y están influenciados por factores como el tipo de generación, la hora, el clima y la cantidad de energía inyectada al sistema.

El objetivo de este proyecto es predecir el costo marginal del sistema eléctrico utilizando como variables los datos de generación eléctrica por tipo de fuente. Una predicción precisa permitiría anticipar variaciones de precio y apoyar decisiones operativas y comerciales.

## Plan de acción

Descripción del dataset:

El dataset fue creado a partir de información del Coordinador Eléctrico Nacional de Chile. Contiene datos del costo marginal cada 15 minutos, el nombre de la barra y el tipo de generación (hidráulica, solar, térmica, eólica, entre otras).

Estructura de la base:

- periodo
- día
- hora
- minuto
- nombre de la barra
- tipo de generación
- valor del costo marginal

Modelo seleccionado:

Se usará regresión lineal múltiple, ya que permite analizar la relación entre distintas variables. Nos interesa analizar: 

- ¿Podemos asociar el costo margianl a al tipo de generación? ¿Qué tipo de generación está asociado a mayores o menores costos?
  x = precio marginal de una barra  y = tipo de generación

- ¿Hay patrones horarios? ¿El costo es más alto en horas punta?
  x = periodo  y = costo marginal

- ¿Los cambios bruscos se relacionan con ciertos tipos de generación entrando o saliendo del sistema?
  x = variación del costo marginal (∆ costo marginal) y = tipo de generación predominante

- ¿El comportamiento es distinto los fines de semana?
  x = día de la semana  y = costo marginal
  
- ¿Hay zonas del sistema donde el costo marginal es más alto?
  x = nombre de la barra (ubicación)  y = costo marginal


 Este modelo fue elegido por su simplicidad, buena interpretación de resultados y bajo costo computacional.

## Estrategia de evaluación

Las métricas que se utilizarán para evaluar el modelo son:

- MAE (Mean Absolute Error)
- RMSE (Root Mean Squared Error)
- R² (Coeficiente de determinación)

La división entre entrenamiento y prueba respetará el orden temporal de los datos.
