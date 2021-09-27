# Madrid_Rooftops

A Mask R-CNN project for Madrid Rooftops Image Segmentation

Ana Blanco Delgado | Septiembre de 2021

---
[Enlace a informe PDF con información ampliada](https://github.com/casiopa/Madrid_Rooftops/blob/70d9bf0643b51750a7df19e985a75e2ca316e09b/Madrid%20Rooftop%20Segmentation%20-%20Resume.pdf)

Este proyecto lo he realizado para el Bootcamp de Data Science en The Bridge en septiembre de 2021, como trabajo individual de Machine Learning. Mi background relacionado con la imagen y el vídeo me ha arrastrado a tareas de Computer Vision, y la idea de este proyecto me aterrizó tras escuchar un muy interesante podcast de Data Stand-Up! con el entrevistado David Rey (Chief Data Officer en Idealista). En la entrevista se menciona el proyecto de Idealista Energy que ofrece información sobre los tejados y su posible aprovechamiento para la instalación de paneles solares (área del tejado, número de paneles solares a instalar, coste aproximado de su instalación, cálculo de ahorro posterior en el consumo energético...).

El objetivo del proyecto es acercarme a este servicio de Idealista Energy y detectar tejados residenciales, piscinas y áreas deportivas, en imágenes aéreas de la Comunidad de Madrid. Para ello he utilizado el framework Mask R-CNN (Mask Region Convolutional Neural Network) para la detección, clasificación y segmentación de imágenes. El framework elegido además, nos permite partir de una red ResNet101 preentrenada con el dataset de imágenes MS COCO.

### Dataset
He descargado 91 imágenes de Google Maps con un zoom fijo de 19, y las he etiqueté en con el software VGG Imagen Annotator (VIA) qu permite seleccionar instancias con polígonos y asignarles una clase. En las 91 imágenes generé un total de 2.033 polígonos.

Para ver información más detallada sobre el dataset revisar el notebook: [/notebooks/inspect_data.ipynb](https://github.com/casiopa/Madrid_Rooftops/blob/main/notebooks/inspect_data.ipynb)

### Entrenamiento
Una vez heredadas las clases necesarias para cargar el dataset y configurar el modelo según especificaciones de Mask R-CNN, entrené las 69 imágenes con sus 1.488 máscaras durante 80 epochs. Evalué con el Mean Average Precision (mAP@IoU=50) cada epoch resultando el módelo del epoch 60 el mejor con los siguientes valores:

Evaluación modelo epoch 60:
- Train_set mAP@50: 0.720 
- Val_set   mAP@50: 0.527

Estos valores sugieren seguir entrenando el modelo, posiblemente con un dataset mayor. 

Para ver información más detallada sobre el modelo seleccionado revisar el notebook: [/notebooks/inspect_model.ipynb](https://github.com/casiopa/Madrid_Rooftops/blob/main/notebooks/inspect_model.ipynb)

Para comprender mejor los resultados revisé las predicciones del modelo con el dataset de validación porque tenía la intuición de que el modelo tiene un buen desempeño para la segmentación de residencias aisladas pero no de adosados o edificios. A continuación muestro ambos casos:



