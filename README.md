# Clasificación Morfológica de Galaxias con Redes Neuronales

Este repositorio contiene el código y la experimentación de un modelo de *Deep Learning* diseñado para automatizar la clasificación morfológica de galaxias. El proyecto distingue entre galaxias de tipo temprano (elípticas) y tardío (espirales e irregulares) utilizando imágenes astronómicas.

Desarrollado como proyecto final para la materia de Introducción a Redes Neuronales en el Instituto de Astronomía de la Universidad Nacional Autónoma de México (UNAM).

## Descripción del Proyecto

La clasificación visual de galaxias según la secuencia de Hubble es un proceso fundamental en astrofísica, pero resulta inviable manualmente dado el inmenso volumen de datos astronómicos actuales y los problemas de baja resolución. 

Este proyecto implementa una Red Neuronal Convolucional (CNN) en Python utilizando TensorFlow/Keras para abordar este problema, logrando discriminar características estructurales complejas a partir de un conjunto de datos de más de 5,600 imágenes.

## Arquitectura del Modelo

El modelo base consiste en una red CNN secuencial optimizada para la extracción de características morfológicas:
* **Capas Convolucionales (Conv2D):** Dos capas con filtros de 32 y 64 para capturar patrones espaciales (como brazos espirales o halos elípticos).
* **Pooling (MaxPooling2D):** Reducción de dimensionalidad para mejorar la eficiencia computacional.
* **Capas Densas (Dense):** Capa oculta de 64 neuronas con activación ReLU.
* **Regularización (Dropout):** Tasa del 50% para mitigar el sobreajuste (*overfitting*).
* **Salida:** Activación Sigmoide para la clasificación binaria (Tempranas vs. Tardías).

## Requisitos y Dependencias

Para ejecutar este código, necesitas un entorno con Python y las siguientes librerías instaladas:
* `tensorflow` / `keras`
* `pandas`
* `numpy`
* `matplotlib`
* `seaborn`
* `scikit-learn`

## Resultados Destacados

Durante la fase de validación y prueba, el modelo demostró un rendimiento sólido:
* **Accuracy (Exactitud):** ~81% en el conjunto de pruebas.
* **AUC ROC:** 0.90, lo que indica una alta capacidad de discriminación entre verdaderos positivos y falsos positivos.
* **Gestión de Sesgos:** El análisis de la Matriz de Confusión permitió identificar áreas de mejora específica en el *recall* de las galaxias tempranas, estableciendo una base clara para futuras iteraciones y ajustes de hiperparámetros.

## Estructura de Datos

El script espera un archivo `galaxias.csv` que contiene los metadatos espectrales y morfológicos (Type, Bars, Tidal, g-i) y un directorio de imágenes asociadas. Las clases se generan dinámicamente:
* `Type <= 0` : Galaxias Tempranas (Label 0)
* `Type > 0` : Galaxias Tardías (Label 1)

## Autor
**Luis Ángel Quiroz López**  
*Universidad Nacional Autónoma de México*
