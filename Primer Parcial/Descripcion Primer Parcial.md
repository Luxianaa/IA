
### Objetivo
Como objetivo principal es constriur modelo que sea capaz de predecir la temperatura maxima diaria en Seattle.
Con el uso de datos historicos y usando la red neuronal MLp"Multilayer Perceptron".

### Descripcion del Dataset "WETHER PREDICTION"
 URL del Dataset: https://www.kaggle.com/datasets/ananthr1/weather-prediction
 Es un dataset de datos meteorologicos  de la ciudad de Seattle, con datos  que sonb abarcados desde  Enero de 2012 hasta Diciembre de 2015.
 Cada fila representa un dia diferente, tiene columnas las cuales abaracan. **`[fecha,precipitacion,temperatura maxima,temperatura minima, viento y tipo de clima]`**.
 EL dataset contiene **1462** filas(datos) con 6 columnas de variables.
### Desarrollo
Como variable objetivo se tomo la temperatura maxima **`temp_max`** Para poder utilizar las variables de entrada se uspo **Lag** , una tecninca que se usa para "Forescasting" en MLP.
Esta tecninca facilita la prediccion de dias anteriores , el valor futuro depende de los dias pasados.
Se uso esta tecnica, ya que el la red neuronal MLP no es capaz de guardar datos no tiene memoria, por loq ue hay que crear un patron el cual le "haga recuerdo.

### Division de datos
Se dividio el dataset en datos de entrenamiento con un 80% y para validacion 20%, es la tecnica comun para construir  un modelo firme y estructurado.
**Train** -> Para que el modelo aprenda patrones
**Val** -> es la prueba del modelo, se le presenta valores o datos nunca antes vistos.

### Heramientas Pytorch
Se utilizo librerias que manipulan el dataset  y lo acoplan al tipo de manejo de datos que tiene PyTorch. 
`TempDataset` -> clase del codigo
Para poder utilizar batches se uso `DataLoader`, que organiza y gestiona los datos en batches.
Un batch es procesar x cantidad de datos a la vez, esto ayuda a trabajar los datos mas rapido.

### Modelo
Se uso modelo MLP con una capa de entrada que recibe el tamano del ``lag`` o `W` (El tamano de la matriz)
La primera capa oculta se conecta con todas las entradas por la funcion **`nn.Linear()`**, con 64 neuronas trabaja y con funcion de activacion **`nn.ReLU()`**
La segunda capa oculta se conecta con todas las entradas por la funcion `nn.Linear()`, de misma manera con 64 batches y usa la reactivacion.
La capa de salida se conecta con la segunda capa oculta y tierne como valor final la `temperatura_maxima`=D_Out=1(una salida, un dato).
Se utilizo este modelo porque  el MLP es capaz de capturar relaciones lineales y patrones que son complejos de deducir.
### Entrenamiento
Se trabajo con 100 epocas  de entrenamiento y se calculo la perdida en cada una, la de validacion  y prediccion.
Se utilizo el optimizador SGD y tambien se probo con Adam, con mejor resultado SGD por la  cantidad  de datos usados.

### Evaluacion
se utilizo:
```
MSE -> (error cuadratico medio)
MAE -> (error absoluto medio)
R**2 -> (coeficiente de determinacion)
```
Los cuales ayudan a mostrar que el modelo varia entre 2 grados centigrados (MAE), pero muestra  que llego  a comprender  un 83%  los datos de la tempreratura maxima.

### Prediccion para los 30 dias
Se uso recursividad para esto, cada prediccion es la entrada para el proximo valor , se grafico  como se comporta  la prediccion  para cada dia de los 30.
