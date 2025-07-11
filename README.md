# Proyecto: Clasificación del Tipo de Generación en el Sistema Eléctrico Chileno basado en Costo Marginal

**Estudiantes**: Fernando Sepúlveda - Víctor Canejan

## Definición del problema

El sistema eléctrico chileno opera bajo un modelo marginalista donde el **costo marginal** refleja el precio de generar una unidad adicional de energía en un nodo específico del sistema. Estos valores se calculan cada 15 minutos y están estrechamente relacionados con el tipo de generación que está operando en cada instante.

El objetivo de este proyecto es **clasificar el tipo de generación eléctrica** `tipo_gen` que está operando en una barra específica en un momento dado, utilizando como principal variable predictora el costo marginal `cmg_peso_kwh` junto con otras características operacionales y temporales.

Esta clasificación permitiría identificar patrones de operación de las centrales eléctricas, entender qué tecnologías están fijando el precio marginal en diferentes momentos, y apoyar análisis de despacho económico del sistema.

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

## Enfoque del modelo:

Se implementaron y compararon tres algoritmos de clasificación:

1. K-Nearest Neighbors (KNN)
    - Ventajas: Simple, no paramétrico, captura relaciones locales
    - Configuración: Optimización del parámetro k mediante validación cruzada
    - Resultados: Buen desempeño inicial pero sensible a escala de datos

2. Árbol de Decisión
    - Ventajas: Interpretable, maneja bien variables categóricas
    - Configuración: Control de profundidad máxima para evitar overfitting
    - Resultados: Proporciona reglas claras pero puede ser inestable

3. Random Forest
    - Ventajas: Combina múltiples árboles, robusto a overfitting
    - Configuración: 100 estimadores, profundidad máxima optimizada
    - Resultados: Mejor desempeño general, captura relaciones no lineales

## Estrategia de evaluación

Se utilizarán las siguientes métricas de desempeño para evaluar los modelos:

- **Accuracy** (Exactitud)
- **Precision**, **Recall** y **F1-score** por clase
- **Matriz de confusión**
- **ROC-AUC** (para modelos probabilísticos)

Se implementará validación cruzada estratificada para asegurar que cada fold mantenga la distribución de clases, y se reservará un conjunto de prueba temporalmente separado para evaluar el desempeño en condiciones realistas.

## Datos

Este repositorio utiliza un archivo de datos CSV que no está incluido directamente por su gran tamaño (1.2 GB).

Puedes descargarlo desde el siguiente enlace:

[Descargar cmg_gen_barra.csv desde Google Drive](https://drive.google.com/file/d/12zpRUrAQpB0F_ImRnaWG7Qui3_kEM61p/view?usp=drive_link)

Una vez descargado, colócalo en la raíz del proyecto (misma carpeta que este README).

## Resultados:
### Classification Report - KNN

| Clase                  | Precision | Recall | F1-score | Support  |
|------------------------|-----------|--------|----------|----------|
| Fotovoltaico           | 0.69      | 0.76   | 0.72     | 551,775  |
| Hidroeléctrica embalse | 0.45      | 0.34   | 0.39     | 23,823   |
| Hidroeléctrica pasada  | 0.58      | 0.49   | 0.53     | 236,725  |
| Térmica                | 0.56      | 0.54   | 0.55     | 288,083  |

|                        | Precision | Recall | F1-score | Support   |
|------------------------|-----------|--------|----------|-----------|
| Accuracy               |           |        | 0.63     | 1,100,406 |
| Macro avg              | 0.57      | 0.53   | 0.55     | 1,100,406 |
| Weighted avg           | 0.63      | 0.63   | 0.63     | 1,100,406 |

### Decision Tree sin PCA
| Clase                  | Precision | Recall | F1-score | Support |
| ---------------------- | --------- | ------ | -------- | ------- |
| Fotovoltaico           | 0.74      | 0.73   | 0.74     | 551,775 |
| Hidroeléctrica embalse | 0.36      | 0.35   | 0.35     | 23,823  |
| Hidroeléctrica pasada  | 0.54      | 0.51   | 0.53     | 236,725 |
| Térmica                | 0.63      | 0.63   | 0.63     | 288,083 |

|              | Precision | Recall | F1-score | Support   |
| ------------ | --------- | ------ | -------- | --------- |
| Accuracy     |           |        | 0.65     | 1,100,406 |
| Macro avg    | 0.56      | 0.56   | 0.56     | 1,100,406 |
| Weighted avg | 0.65      | 0.65   | 0.65     | 1,100,406 |


## Conclusiones:
Se aplicaron dos modelos de clasificación para predecir el tipo de generación eléctrica: KNN y árbol de decisión. Ambos entregaron resultados similares, aunque el árbol de decisión mostró un rendimiento levemente mejor.

El modelo KNN alcanzó un accuracy del 63%, mientras que el árbol de decisión logró un 65%. En ambos casos, la clase con mejor desempeño fue “fotovoltaico”, lo que sugiere que esta fuente tiene patrones más marcados o diferenciables. Por otro lado, “hidroeléctrica embalse” fue la clase más difícil de predecir, probablemente por la baja cantidad de ejemplos.

El árbol de decisión tuvo mejores métricas generales (precision, recall y F1-score), lo que indica que logró una mejor separación entre clases. A pesar de eso, los dos modelos son útiles como primera aproximación y permiten entender qué tipos de generación son más distinguibles a partir de los datos disponibles.

En ambos casos la precisión no supera el 70%, por lo que, a pesar de lograr clasificar de manera correcta una cantidad significativa de veces, los resultados aún dejan espacio para mejoras. Esto sugiere que podría ser útil probar con modelos más complejos o incorporar nuevas variables que capturen mejor las diferencias entre los tipos de generación. También sería interesante evaluar el impacto del desbalance de clases y aplicar técnicas de balanceo para mejorar el rendimiento en las categorías menos representadas.

*Este proyecto representa una aplicación práctica de análisis predictivo en el contexto del mercado eléctrico chileno, con base en datos abiertos y una problemática de alto impacto operativo y económico.*
