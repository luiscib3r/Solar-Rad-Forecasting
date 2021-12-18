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

<br><br>

# English Version

# Solar Radiation Prediction with Neural Networks

In these notebooks the entire research and implementation process carried out for the construction of various machine learning models based on neural networks that are capable of predicting levels of solar radiation is captured given a set of historical data taken by meteorological stations.

## Neural Networks Architecture

### LSTM and GRU

LSTM and GRU networks are a type of recurrent neural networks specially designed for time series analysis. Initially, two models were implemented each one using one of these networks to evaluate the performance of each one performing the objective task of this work.
In the training carried out, both models obtained similar results. However, GRU networks have less computational complexity than LSTM networks, allowing training cycles to be completed in less time. One of the objectives of this project was “In addition to obtaining good results, keeping training costs relatively low, whether in terms of time or money”. For this reason, the GRU network was chosen to continue the research and develop the following models.

### Convolution with GRU in regression

In the field of image processing, it is very common to apply convolutions to them using preset filters that allow extraction of the characteristics of said image. For several years this filter selection process has been automated with the introduction of convolutional neural networks, this type of networks are capable of automatically adjusting the parameters of the filters that must be applied to the images to obtain the necessary characteristics. to carry out the task entrusted to them.
On the other hand, in the field of signal processing, it is also very common to apply various convolution operations to the signal that is being processed in order to reduce noise, smooth the signal curve and extract significant characteristics.
On this basis it was decided to implement a model that combines a convolutional layer with a GRU layer. Better results were obtained with this new model and also decreased the number of recurring GRU cells, which also caused the computational complexity of the model to decrease by reducing the number of parameters.

### Convolution with GRU in classification

Analyzing the practical application of the previous model, it was discovered that normally in this type of study it is not necessary to predict an exact value for the radiation level, but instead what is wanted is to determine if the radiation level is at a specified interval. Based on this, the data set was transformed so that the output values were a class vector, each class corresponds to a radiation interval, in this particular case eleven intervals were selected for a range from 0 to 1000 possible radiation levels. , obtaining the intervals of 0-100, 101-200, ..., more than 1000.
This operation means that the model used is no longer trained to solve a regression problem and instead is trained to solve a classification problem, where the output of the model is a vector that contains the probabilities that the real value that you want to predict it is in some of the selected intervals.
The only change made with respect to the previous model is in the activation function used in the last output layer and in the cost function used for training the model.

### NOTE

* The models have been developed and trained using [Tensorflow](https://www.tensorflow.org/)
