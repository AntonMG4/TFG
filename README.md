# Desarrollo de un Sistema Asistente de Música Basado en Aprendizaje Automático y Procesamiento del Lenguaje Natural con Modelos de Lenguaje Generativos
Este repositorio contiene los códigos fuente utilizados para desarrollar el asistente musical basado en aprendizaje automático, con la capacidad de interpretar las intenciones del usuario mediante un chatbot conversacional. El proyecto incluye la implementación, entrenamiento, ajuste y evaluación de los modelos generativos LLaMA y Falcon, así como la implementación del chatbot.

## Estructura del Proyecto

El repositorio está dividido en dos carpetas principales: `googleColab` y `ChatWidget`. A continuación, se detalla la organización de cada una de ellas.

### 1. Carpeta `googleColab`

Esta carpeta contiene el código que se ejecuta en Google Colab y está relacionada con el entrenamiento, ajuste y evaluación de los modelos.

- **`DataSplit.ipynb`**: Este cuaderno contiene el código necesario para dividir el conjunto de datos original en tres subconjuntos: entrenamiento, validación y test.
  
- **`FinetuningFalcon.ipynb`**: En este cuaderno se lleva a cabo el proceso de ajuste de hiperparámetros y el entrenamiento del modelo **Falcon**. Durante el entrenamiento, los modelos se guardan periódicamente, y una vez finalizado el proceso, el modelo se guarda con su configuración LoRA y se registran las medidas de evaluación.

- **`FinetuningLlama.ipynb`**: Similar al cuaderno anterior, pero para el modelo **LLaMA**. Aquí también se lleva a cabo el ajuste de hiperparámetros, el entrenamiento y el almacenamiento de los modelos entrenados junto con sus evaluaciones.

- **`EvalLossPlot.ipynb`**: Este cuaderno genera una gráfica a partir de los datos de `eval_loss` proporcionados durante el entrenamiento mediante TensorBoard. La gráfica muestra la evolución de la pérdida de validación y entrenamiento a lo largo de las épocas.

- **`MergeModels.ipynb`**: Este cuaderno carga y guarda los modelos entrenados en su forma completa (sin la configuración LoRA de PEFT), lo que permite la utilización de los modelos para la implementación del chatbot.

- **`ft_falcon_model/`** y **`ft_llama_model/`**: Estas subcarpetas contienen los resultados de las métricas de evaluación de los modelos ya entrenados, junto con los archivos de los modelos.

- **`final_model/`**: Esta subcarpeta contiene el modelo final entrenado con la configuración LoRA, la gráfica generada de la evolución de `eval_loss`, y los archivos `apiFalcon.ipynb` y `apiLlama.ipynb`. Estos archivos permiten cargar los modelos en su forma completa (sin LoRA) y subirlos a la API. Además, se crea un túnel local, y la URL generada permite la comunicación con el entorno local.

### 2. Carpeta `ChatWidget`

Esta carpeta contiene el código para implementar el chatbot y la interacción con la base de datos musical.

- **`music_recommender.py`**: Este archivo contiene el proceso de comunicación entre el usuario y el chatbot. Se encarga de la predicción de las intenciones del usuario, la clasificación de comandos (como añadir, eliminar, ver o limpiar canciones) y la actuación sobre la base de datos musical (agregar o eliminar canciones de la lista de reproducción).

### Ejecución del Sistema

Para inicializar el chatbot y poner en funcionamiento el sistema, sigue estos pasos:

1. **Sustituir la URL en `music_recommender.py`**:
   - En la función `predict_intent` del código `music_recommender.py`, sustituye la URL establecida por la URL proporcionada tras ejecutar el archivo `apiFalcon.ipynb` o `apiLlama.ipynb` desde Google Colab.

2. **Iniciar el servidor web**:
   - Abre una terminal en la carpeta del programa y ejecuta el siguiente comando:
   ```bash npm start```
   Esto iniciará el servidor que sirve la interfaz del chatbot en el navegador.

3. **Ejecutar el programa principal**:
   - En otra terminal dentro de la carpeta principal, ejecuta:
   ```bash start ./music_recommender.py```
   Esto abrirá una nueva pestaña en el navegador con el chatbot en funcionamiento. Ahora podrás interactuar con el asistente musical, utilizando los modelos entrenados en Google Colab.
