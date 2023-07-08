# T_DATOS
 
Decidi usar lsa arquitectura CNN por la capacidad de aprendizaje que tiene, pues medida que se alimenta a la red con un conjunto de imágenes etiquetadas, la red ajusta sus pesos y parámetros internos y por la detección de caracteres especiales permite a la red detectar características específicas en diferentes partes de la imagen, como bordes, texturas o formas, lo que resulta en un análisis de imágenes con mejor precisión.

Importar las siguintes librerias, que se utilizan para trabajar con el sistema operativo y el procesamiento de imágenes.
import os
import cv2

Variables para especificar las ubicaciones de las carpetas que contienen los conjuntos de datos de entrenamiento y prueba.
train_folder = 'DATASET/train'
test_folder = 'DATASET/test'

almacenar imágenes de entrenamiento
train_images = []
train_labels = []
train_labels1 = []

División del conjunto de entrenamiento en entrenamiento y validación utilizando train_test_split de sklearn.model_selection.

Contar el numero de archivos del directorio y si no hay archivos le asigno en la lista

for label in os.listdir(train_folder):
    label_folder = os.path.join(train_folder, label)
    list = os.listdir(label_folder) # dir is your directory path
    number_files = len(list)
    if (number_files) > 0:
        for filename in os.listdir(label_folder):
            img_path = os.path.join(label_folder, filename)
            img = cv2.imread(img_path)
            train_images.append(img)
            train_labels.append(label)
            train_labels1.append(label)
            
            
Normalización de los datos de las imágenes en las listas train_images y val_images dividiéndolos por 255.0 y convirtiéndolos al tipo de dato 'float32'. 

Se utiliza un modelo secuencial (Sequential) de tensorflow.keras.models.
Se agregan capas convolucionales (Conv2D) con activación ReLU y capas de agrupamiento (MaxPooling2D).

se realiza una predicción utilizando un modelo (model) sobre un conjunto de imágenes de prueba (test_images). Luego, se obtienen las etiquetas predichas (predicted_labels) a partir de las salidas del modelo utilizando np.argmax() para obtener el índice del valor máximo a lo largo del eje 1.


Calculo de la matriz de confusión del modelo utilizando la función confusion_matrix de alguna biblioteca o módulo que no especificaste. La matriz de confusión es una herramienta útil para evaluar el rendimiento de un modelo de clasificación al mostrar la cantidad de muestras que se clasificaron correctamente e incorrectamente en cada clase.


Calculo e impresion la matriz de confusión del error en el conjunto de entrenamiento. Se realiza una predicción en las imágenes de entrenamiento (train_images) utilizando el modelo (model), se obtienen las etiquetas predichas (train_predicted_labels), y luego se calcula la matriz de confusión comparando las etiquetas reales (train_labels_encoded) con las etiquetas predichas.

train_predictions = model.predict(train_images)
train_predicted_labels = np.argmax(train_predictions, axis=1)
train_confusion = confusion_matrix(train_labels_encoded, train_predicted_labels)
print('Matriz de confusión del error en entrenamiento:')
print(train_confusion)


En el código que proporcionaste, se realiza la predicción sobre las imágenes de prueba (test_images) utilizando el modelo (model). Luego, se obtienen las etiquetas predichas (test_predicted_labels) utilizando la función np.argmax() y se calcula la matriz de confusión del error en la prueba comparando las etiquetas reales codificadas (test_labels_encoded) con las etiquetas predichas.

Aquí tienes un ejemplo de cómo podrías calcular y mostrar la matriz de confusión del error en la prueba:

python
Copy code
from sklearn.metrics import confusion_matrix

Realizar predicciones en las imágenes de prueba

test_predictions = model.predict(test_images)
Obtener las etiquetas predichas en el conjunto de prueba
test_predicted_labels = np.argmax(test_predictions, axis=1)

Calcular la matriz de confusión del error en prueba
test_confusion = confusion_matrix(test_labels_encoded, test_predicted_labels)

Mostrar la matriz de confusión del error en prueba
print('Matriz de confusión del error en prueba:')
print(test_confusion)
(test_images), las etiquetas reales codificadas (test_labels_encoded), y un modelo previamente entrenado (model). Utilizamos las mismas funciones y enfoques mencionados anteriormente.

Luego, realizamos las predicciones sobre las imágenes de prueba utilizando model.predict(), obtenemos las etiquetas predichas utilizando np.argmax(), y calculamos la matriz de confusión utilizando confusion_matrix().

Se imprime la matriz de confusión del error en la prueba con print(test_confusion)
