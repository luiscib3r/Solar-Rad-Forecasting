# Predicción de Radiación Solar con Redes Neuronales

En estos notebooks queda plasmado todo el proceso de investigación e implementación realizado para la construcción de varios modelos de aprendizaje automático basados en redes neuronales que sean capaces de predecir niveles de radiación solar dado un conjunto de datos históricos tomados por estaciones meteorológicas.

## Arquitectura de redes neuronales

### LSTM y GRU
Las redes LSTM y GRU son un tipo de redes neuronales recurrentes especialmente diseñadas para el análisis de series temporales. Inicialmente se implementaron dos modelo  cada uno utilizando una de estas redes para evaluar el rendimiento de cada una realizando la tarea objetivo de este trabajo.
En los entrenamiento realizados ambos modelos obtuvieron resultados similares. Sin embargo las redes GRU tienen una menor complejidad computacional que las LSTM, permitiendo completar los ciclos de entrenamiento en un tiempo menor. Uno de los objetivos de este proyecto fué “además de obtener buenos resultados mantener los costos de entrenamiento ya sea en función de tiempo o de dinero relativamente bajos” . Por este motivo se escogió la red GRU para continuar con la investigación y desarrollar los siguientes modelos.

### Convolución con GRU en regresión
En el campo del procesamiento de imágenes es muy común aplicar convoluciones a las mismas utilizando filtros preestablecidos que permiten realizar extracción de las caracteríticas de dicha imágen. Desde hace varios años este procesos de selección de los filtros se automatizó con la introducción de la redes neuronales convolucionales, este tipo de redes son capaces de ajustar de manera automática los parámetros de los filtros que deben ser aplicados a las imágenes para obtener las características necesarias para realizar la tarea que se les encomiende.
Por otro lado en el campo del procesamiento de señales también es muy común aplicar varias operaciones de convolución a la señal que se esté procesando con el objetivo de reducir ruido, suavizar la curva de la señal y extraer características significativas.
Sobre esta base se decidió implementar un modelo que combina una capa convolucional con una capa GRU. Se logró obtener mejores resultados con este nuevo modelo y además desminuier el número de celdas recurrentes GRU, lo cuál también provocó que disminuyera la complejidad computacional del modelo reduciendo la cantidad de parámetros.

### Convolución con GRU en clasificación
Analizando la aplicación práctica del modelo anterior se descubrió que normalmente en este tipo de estudios no se hace necesario predecir un valor exacto para el nivel de radiación, sino que en lugar de esto lo que se quiere es determinar si el nivel de radiación se encuentra en un intervalo determinado. Basado en esto se transformó el conjunto de datos para que los valores de salida fueran un vector de clases, cada clase corresponde a un intervalo de radiación, en este caso en paticular se seleccionaron once intervalos para un rango de 0 a 1000 niveles de radiación posibles, obteniendo los intervalos de 0-100, 101-200, …, más de 1000. 
Esta operación hace el que el modelo empleado ya no se entrene para resolver un problema de regresión y en lugar de esto se entrene para resolver un problema de clasificación, donde la salida del modelo es un vector que contiene las probabilidades de que el valor real que se desea predecir se encuentre en algunos de los intervalos seleccionados. 
El único cambio realizado con respecto al modelo anterior está en la función de activación utilizada en la última capa de salida y en la función de costo utilizada para el entrenamiento del modelo.

### NOTAS:

* Los modelos han sido desarrollados y entrenados utilizando [Tensorflow](https://www.tensorflow.org/)
