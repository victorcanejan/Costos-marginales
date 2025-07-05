# Proyecto: Predicción del Costo Marginal en el Sistema Eléctrico Chileno

**Estudiantes**: Fernando Sepúlveda - Víctor Canejan

## Definición del problema

El sistema eléctrico chileno opera bajo un modelo marginalista donde el **costo marginal** refleja el precio de generar una unidad adicional de energía en un nodo específico del sistema. Estos valores se calculan cada 15 minutos y dependen de múltiples factores, como el tipo de generación, la hora, el clima y la cantidad de energía inyectada al sistema.

El objetivo de este proyecto es **predecir el costo marginal** de una barra del sistema eléctrico en un instante dado, utilizando como variables los datos de generación eléctrica por tipo de fuente.

Una predicción precisa permitiría anticipar variaciones de precio, facilitar la toma de decisiones operativas y evaluar estrategias de planificación energética.

## Descripción del dataset

El dataset fue construido a partir de información publicada por el **Coordinaro Eléctrico Nacional de Chile**, y estructurado mediante una base de datos relacional mantenida por la empresa **Antumanque Consultores**, a la cual se accedió para el desarrollo de este proyecto.

Cada registro corresponde a una observación en un intervalo de 15 minutos e incluye las siguientes variables:

- `periodo`: año y mes del dato (formato `AAAA-MM-01`)
- `día`: día del mes
- `hora`: hora del día (0 a 23)
- `minuto`: minuto del intervalo (0, 15, 30, 45)
- `nombre_barra`: nombre de la barra eléctrica
- `generacion_kwh`: energía generada en esa barra en el intervalo (kWh)
- `cmg_peso_kwh`: costo marginal de esa barra en ese instante ($/kWh)
- `tipo_gen`: Etiqueta que clasifica según el tipo de central que está generando en esa barra en ese instante

Este dataset representa una vista concentrada del comportamiento horario del sistema eléctrico y permite correlacionar variables operacionales con el costo marginal observado.

## Modelo seleccionado:

Se aplicará un enfoque de **regresión supervisada**, comenzando con **regresión lineal múltiple** para establecer una línea base. Posteriormente se evaluará el desempeño de modelos más complejos como **KNN** y **Random Forest**, con el objetivo de capturar posibles no linealidades en los datos.

Preguntas guías para el análisis:

- ¿Podemos asociar el costo margianl al tipo de generación? ¿Qué tipo de generación está asociado a mayores o menores costos?
  x = precio marginal de una barra  y = tipo de generación

- ¿Hay patrones horarios? ¿El costo es más alto en horas punta?
  x = periodo  y = costo marginal

- ¿Los cambios bruscos se relacionan con ciertos tipos de generación entrando o saliendo del sistema?
  x = variación del costo marginal (∆ costo marginal) y = tipo de generación predominante

- ¿El comportamiento es distinto los fines de semana?
  x = día de la semana  y = costo marginal
  
- ¿Hay zonas del sistema donde el costo marginal es más alto?
  x = nombre de la barra (ubicación)  y = costo marginal

> El uso de regresión lineal permite una interpretación directa de la influencia de cada variable y un bajo costo computacional, ideal para una primera aproximación al problema.

## Estrategia de evaluación

Se utilizarán las siguientes métricas de desempeño para evaluar los modelos:

- **MAE** (Mean Absolute Error)
- **RMSE** (Root Mean Squared Error)
- **R²** (Coeficiente de determinación)

Además, se mantendrá una separación temporal entre datos de entrenamiento y prueba, evitando el uso de validación aleatoria, con el fin de simular un escenario real de predicción futura basada en datos históricos.

## Datos

Este repositorio utiliza un archivo de datos CSV que no está incluido directamente por su gran tamaño (1.2 GB).

Puedes descargarlo desde el siguiente enlace:

[Descargar cmg_gen_barra.csv desde Google Drive](https://drive.google.com/file/d/12zpRUrAQpB0F_ImRnaWG7Qui3_kEM61p/view?usp=drive_link)

Una vez descargado, colócalo en la raíz del proyecto (misma carpeta que este README).
---

*Este proyecto representa una aplicación práctica de análisis predictivo en el contexto del mercado eléctrico chileno, con base en datos abiertos y una problemática de alto impacto operativo y económico.*