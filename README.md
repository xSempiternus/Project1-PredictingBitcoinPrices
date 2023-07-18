# Project1-PredictingBitcoinPrices
Este proyecto tiene como objetivo desarrollar un modelo predictivo utilizando técnicas de Machine Learning. En este caso específico se utilizó el Bagging para estimar el precio del Bitcoin a partir de datos históricos en funcion del precio y los días.

# Requisitos (revisar el archivo requirements.txt)

Python 3.x
Bibliotecas de Machine Learning, como scikit-learn, numpy y pandas.

**Instalación**

Clona o descarga este repositorio en tu máquina local.

Abre una terminal y navega hasta el directorio del proyecto.

Crea y activa un entorno virtual (opcional, pero se recomienda).

Ejecuta el siguiente comando para instalar las dependencias:

pip install -r requirements.txt

**Uso**

Asegúrate de tener los datos históricos del precio del Bitcoin en un archivo CSV. Puedes obtener estos datos de la siguiente manera:
Ve a "https://finance.yahoo.com/quote/BTC-USD/history/".
Descarga los datos históricos en formato CSV.
Coloca el archivo CSV con los datos en la carpeta "data" del proyecto o en la carpeta donde estes ejecutando el codigo.

Ejecuta el notebook "data_preprocessing.ipynb" ubicado en la carpeta "notebooks". Este notebook se encargará de realizar el preprocesamiento de los datos, como la limpieza, transformación y normalización. Es de suma importancia saber el directorio del archivo CSV, de esta forma se podrá implementar lo que sigue.

(Opcional)
Puedes revisar el notebook "exploratory_analisis" para visualizar una profundización de los datos utilizados para el modelo. 
    
Una vez finalizado el preprocesamiento, ejecuta el notebook "Bagging_modeling.ipynb" ubicado en la carpeta "notebooks". Este notebook contiene la implementación del modelo de regresión y la evaluación del rendimiento del modelo.


**Descripción del Código**

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


**Análisis y conclusiones**


Notamos que el precio irá variando en funcion del tiempo y va a subir a su punto máximo en el rango entre 100 y 150. A partir de estos resultados se genera la variación de ganancias(gráfico profit). Por lo que el periodo de mayor ganancia se encuentra justamente en el rango anteriormente mencionado.

El modelo con max_depth= 2 tiene un MSE ligeramente menor (5.69) en comparación con el modelo con max_depth= 3 (5.75). En términos de precisión de la predicción, un MSE más bajo indica un mejor ajuste del modelo a los datos de entrenamiento.

En cuanto a la variable Sharpe , el modelo con max_depth=2 tiene un índice de Sharpe más alto (1.18) en comparación con el modelo con max_depth=3 (0.49). Un índice de Sharpe más alto indica un mejor rendimiento ajustado al riesgo de la inversión o estrategia

Al comparar los resultados del modelo con max_depth=2 y max_depth=3, podemos observar que el modelo con max_depth=3 tiene un MAE ligeramente más alto (1.75) en comparación con el modelo con max_depth=2 (1.72). Esto indica que, en promedio, el modelo con max_depth=3 tiene un error de aproximadamente 1.75 unidades, mientras que el modelo con max_depth=2 tiene un error de aproximadamente 1.72 unidades. Por lo tanto, en términos de la magnitud promedio de los errores, el modelo con max_depth=2 parece tener un rendimiento ligeramente mejor.

En cuanto al RMSE el modelo con max_depth=3 también tiene un valor ligeramente más alto (2.40) en comparación con el modelo con max_depth=2 (2.39). Esto indica que, en promedio, el modelo con max_depth=3 tiene una diferencia de aproximadamente 2.40 unidades entre las predicciones y los valores reales, mientras que el modelo con max_depth=2 tiene una diferencia de aproximadamente 2.39 unidades. Similar al MAE, esto sugiere que el modelo con max_depth=2 tiene un rendimiento ligeramente mejor en términos de la magnitud promedio de los errores.
A partir del análisis de estas variables es recomendable usar el modelo con max_depth=2, ya que es un modelo ligeramente mejor. Sin embargo, los resultados son bastante cercanos por lo que será decision de cada uno el utilizar un modelo u otro.

Un análisis más detallado esta en la carpeta "reports".


**Contribución**

Las contribuciones a este proyecto son bienvenidas. Si encuentras algún problema o tienes alguna sugerencia, por favor, crea un "issue" en este repositorio.

**Contacto**

Si tienes alguna pregunta o consulta relacionada con este proyecto, puedes contactarme a través de mi dirección de correo electrónico nikoantu@gmail.com.

