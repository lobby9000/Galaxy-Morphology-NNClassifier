# Clasificación morfológica de galaxias con redes neuronales

[English version](README.md)

Este repositorio contiene el código y la experimentación de un modelo de *Deep Learning* diseñado para automatizar la clasificación morfológica de galaxias. El proyecto distingue entre galaxias de tipo temprano (elípticas) y tardío (espirales e irregulares) utilizando imágenes astronómicas.

Desarrollado como proyecto final para la materia de Introducción a Redes Neuronales en el Instituto de Astronomía de la Universidad Nacional Autónoma de México (UNAM).

## Descripción del proyecto

La clasificación visual de galaxias según la secuencia de Hubble es un proceso fundamental en astrofísica, pero resulta inviable manualmente dado el inmenso volumen de datos astronómicos actuales y los problemas de baja resolución. 

Este proyecto implementa una Red Neuronal Convolucional (CNN) en Python utilizando TensorFlow/Keras para abordar este problema, usando un conjunto de 5,608 imágenes, disponibles en https://drive.google.com/drive/folders/1KO-0zXPLNNWNANdyPr38_gdFL9sT0Ovb?usp=sharing.

## Arquitectura del modelo base

El modelo base consiste en una red CNN secuencial optimizada para la extracción de características morfológicas:
* **Capas Convolucionales (Conv2D):** Dos capas con filtros de 32 y 64 para capturar patrones espaciales (como brazos espirales o halos elípticos).
* **Pooling (MaxPooling2D):** Reducción de dimensionalidad para mejorar la eficiencia computacional.
* **Capas Densas (Dense):** Capa oculta de 64 neuronas con activación ReLU.
* **Regularización (Dropout):** Tasa del 50% para mitigar el sobreajuste (*overfitting*).
* **Salida:** Activación Sigmoide para la clasificación binaria (Tempranas vs. Tardías).

## Requisitos y dependencias

Para ejecutar este código, necesitas un entorno con Python y las siguientes librerías instaladas:
* `tensorflow` / `keras`
* `pandas`
* `numpy`
* `matplotlib`
* `seaborn`
* `scikit-learn`

## Resultados destacados

* **Datos:** 5,608 imágenes divididas 70/15/15 (3,924 entrenamiento, 842 validación, 842 prueba).
* **CNN base:** 81.0% de accuracy en prueba, con *recall* de solo 0.68 en galaxias tardías.
* **CNN más profunda** (3 bloques convolucionales, Adam con lr = 1e-4, *early stopping* restaurando los mejores pesos): **86.3%** de accuracy en prueba.
* **InceptionV3** (transfer learning con base congelada de ImageNet): 85.9% de accuracy con *recall* equilibrado (0.86 en ambas clases).
* **Pendiente:** el experimento con InceptionV3 define un generador con aumento de datos que no quedó conectado al entrenamiento; conectarlo es el siguiente paso.

## Estructura de datos

El script espera un archivo `galaxias.csv` que contiene los metadatos espectrales y morfológicos (Type, Bars, Tidal, g-i) y un directorio de imágenes asociadas. Las clases se generan dinámicamente:
* `Type <= 0` : Galaxias Tempranas (Label 0)
* `Type > 0` : Galaxias Tardías (Label 1)

## Autor
**Luis Ángel Quiroz López**  
*Universidad Nacional Autónoma de México*

## Licencia

Código bajo [licencia MIT](LICENSE).
