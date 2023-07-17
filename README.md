# Project1-PredictingBitcoinPrices
Este proyecto tiene como objetivo desarrollar un modelo predictivo utilizando técnicas de Machine Learning. En este caso específico se utilizó el Bagging para estimar el precio del Bitcoin a partir de datos históricos en funcion del precio y los días.
Requisitos (revisar el archivo requirements.txt)

    Python 3.x
    Bibliotecas de Machine Learning, como scikit-learn, numpy y pandas.

Instalación

    Clona o descarga este repositorio en tu máquina local.

    Abre una terminal y navega hasta el directorio del proyecto.

    Crea y activa un entorno virtual (opcional, pero se recomienda).

    Ejecuta el siguiente comando para instalar las dependencias:

    pip install -r requirements.txt

Uso

    Asegúrate de tener los datos históricos del precio del Bitcoin en un archivo CSV. Puedes obtener estos datos de la siguiente manera:
        Ve a "https://finance.yahoo.com/quote/BTC-USD/history/".
        Descarga los datos históricos en formato CSV.
        Coloca el archivo CSV con los datos en la carpeta "data" del proyecto o en la carpeta donde estes ejecutando el codigo.

    Ejecuta el notebook "data_preprocessing.ipynb" ubicado en la carpeta "notebooks". Este notebook se encargará de realizar el preprocesamiento de los datos, como la limpieza, transformación y normalización. Es de suma importancia saber el directorio del archivo CSV, de esta forma se podrá implementar lo que sigue.

    (Opcional)
    Puedes revisar el notebook "exploratory_analisis" para visualizar una profundización de los datos utilizados para el modelo. 
    
     Una vez finalizado el preprocesamiento, ejecuta el notebook "Bagging_modeling.ipynb" ubicado en la carpeta "notebooks". Este notebook contiene la implementación del modelo de regresión y la evaluación del rendimiento del modelo.
     Descripción del Código

Descripción del Código
        Este código implementa un modelo de bagging para predecir el precio del Bitcoin. A continuación se describe el flujo de trabajo del código:

        Importación de bibliotecas: Se importan las bibliotecas necesarias, como NumPy, Pandas, y scikit-learn (sklearn), así como el módulo simulate del archivo simulator.py.

        Configuración de la semilla aleatoria: Se establece la semilla aleatoria utilizando np.random.seed() para garantizar la reproducibilidad de los resultados.

        Inicialización del modelo: Se crea un objeto BaggingRegressor con n_estimators=42 y base_estimator=DecisionTreeRegressor(max_depth=1). Esto significa que se utilizarán 20 estimadores base, que en este caso son árboles de decisión con una profundidad máxima de 1.Puedes ir variando estos valores para ver como va cambiando el modelo en si.

        Carga de datos: Se lee un archivo CSV llamado 'BTC-USD.csv' utilizando Pandas. Los datos se almacenan en un DataFrame llamado data. A continuación, se imprime la forma de los datos para verificar que se hayan cargado correctamente.

        Preprocesamiento de datos: Se eliminan las filas que contienen valores faltantes utilizando data.dropna(). Luego, la columna 'Date' se convierte en un objeto de fecha y se establece como índice utilizando pd.to_datetime() y set_index() respectivamente. A continuación, se calculan las diferencias porcentuales entre los valores de cierre consecutivos y se almacenan en un array llamado diffs.

        Creación de datos de entrada: Se define una función llamada create_x_data() que crea los datos de entrada x_data para el modelo. Estos datos se generan utilizando las diferencias calculadas anteriormente y se desplazan en el tiempo para crear características de retraso. En este caso, se crea un total de 20 características de retraso utilizando un bucle for. Los datos de entrada se escalan multiplicándolos por 100.

        Reproductibilidad: Se redondean los datos de entrada y salida a 8 decimales para garantizar la reproducibilidad de los resultados.

        Validación de retroceso caminando hacia adelante: Se establece una ventana de tamaño 150 y se realiza la validación de retroceso caminando hacia adelante. En cada iteración, se selecciona una ventana de datos de entrada y salida correspondientes y se ajusta el modelo utilizando lr.fit(). A continuación, se realiza una predicción para el siguiente punto de datos fuera de la ventana y se almacena en un array llamado preds.

        Evaluación del rendimiento: Se calcula el error cuadrático medio (MSE) entre las predicciones y los valores reales utilizando metrics.mean_squared_error(). Se imprime el valor del MSE en porcentaje.

        Gráfico final: Se llama a la función simulate() del módulo simulator para generar un gráfico que muestra la simulación del rendimiento del modelo. Éste será de precio v/s tiempo.
    
    Finalmente se guarda el modelo con la extensión .pkl

Análisis
        El análisis final esta sintetizado en la carpeta "reports".

Contribución

        Las contribuciones a este proyecto son bienvenidas. Si encuentras algún problema o tienes alguna sugerencia, por favor, crea un "issue" en este repositorio o envía una solicitud de extracción con tus mejoras.

Contacto

        Si tienes alguna pregunta o consulta relacionada con este proyecto, puedes contactarme a través de mi dirección de correo electrónico nikoantu@gmail.com.

        Espero que este README.md proporcione la información necesaria para que puedas comprender y utilizar el modelo de bagging para predecir el precio del Bitcoin.

