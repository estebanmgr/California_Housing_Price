# California_Housing_Price
*	Predecir el valor medio de una vivienda en el área de California tomando en cuenta varios datos significativos de la zona (Ingreso medio de la población cercana, número de habitaciones, número de baños, edad de la vivienda, etc.).
* Analizar los datos para hacer una limpieza de los mismos con el finde ordenarlos y que ayuden a trabajar mejor los distintos modelos de regresión.
* Utilizar y entrenar distintos modelos de regresión (Lineal, Árbol de decisiones, Support Vector Machine, Random Forest, K neigbors y gradient boosting) para luego poder contrastar los resultados con una parte de los datos que no han sido utilizarlos y así medir su eficacia.
* Evaluar el modelo con el mejor porcentaje de eficacia para luego probarlo con un conjunto de evaluación ya depurado.

## Recursos y código utilizado 
**Versión de Python:** 3.7  
**Paquetes:** pandas, numpy, sklearn, matplotlib, seaborn   
**Artículo del dataset utilizado:**@article{scikit-learn,
 title={Scikit-learn: Machine Learning in {P}ython},
 author={Pedregosa, F. and Varoquaux, G. and Gramfort, A. and Michel, V.
         and Thirion, B. and Grisel, O. and Blondel, M. and Prettenhofer, P.
         and Weiss, R. and Dubourg, V. and Vanderplas, J. and Passos, A. and
         Cournapeau, D. and Brucher, M. and Perrot, M. and Duchesnay, E.},
 journal={Journal of Machine Learning Research},
 volume={12},
 pages={2825--2830},
 year={2011}
}

# Explicación de datos utilizados
El dataset consta de 20640 filas y 10 columnas (o variables):

longitude: Valor que determina que tan al Oeste está a vivienda; un número mayor significaría estar más al Oeste   
latitude: Valor que determina que tan al Norte está la vivienda; un número mayor significaría estar más al Norte    
housingMedianAge: Edad media de una casa, un menor número indicaría una propiedad más nueva   
totalRooms: Número total de habitaciones   
totalBedrooms: Número total de dormitorios   
population: Número total de población viviendo en el la urbanización    
households: Total número de familias o grupo de personas viviendo en la misma casa   
medianIncome: Media de ingresos por unidad familiar (medida en dólares americanos $)   
medianHouseValue: Valor medio de una vivienda (medida en dolares americanos $)   
oceanProximity: Ubicación de la casa con respecto al océano

## Análisis exploratorio de los datos (EDA)
Analicé la distribución de los datos, la correlación entre ellos y las estadísticas descriptivas de las variables numéricas. A continuación, se pueden ver algunos de los gráficos obtenidos. 

![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Histograma%20de%20las%20variables.png "Histograma de variables")
![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Heatmap%20de%20variables.png "Heatmap de las variables")
![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Ocupaci%C3%B3n%20promedio%20vs%20Antoguedad.png "Ocupación vs Antiguedad de la vivienda")
![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Poblaci%C3%B3n%20vs%20Antiguedad.png "Población vs Antigüedad de la vivienda")
![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Habitaciones%20promedio%20vs%20Antiguedad.png "Habitaciones promedio vs Antigüedad de la vivienda")

## Limpiando el Dataset
Después de importar el dataset fue necesario limpiarlo para que el modelo pueda entrenarse mejor y que no se encuentren valores desvirtuados. Hice los siguientes cambios en las variables y en los datos:

*	Uní las variables independientes y dependiente para poder tener un overview general de todo el dataset 
*	Eliminé los valores erróneos de la variable "Ocupación promedio"
*	Eliminé los valores incorrectos de la variable "Habitaciones promedio" y "Dormitorios promedio" ya que había viviendas con más de 20 habitaciones.
*	Eliminé las filas con valores exagerados de "Ocupación promedio" y de "Ingreso medio" 

![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Boxplot%20de%20Dormitorios%20promedios.png "Dormitorios promedios")
![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Boxplot%20de%20habitaciones%20promedio.png "Habitaciones promedio")
![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Boxplot%20de%20Ocupaci%C3%B3n%20promedio.png "Ocupación promedio")
![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Boxplot%20de%20Poblaci%C3%B3n.png "Población")
![alt text](https://github.com/estebanmgr/California_Housing_Price/blob/main/Im%C3%A1genes/Escalado%20de%20las%20variables.png "Escalado de variables")

## Creando el modelo 

Primero realicé un escalado de las variables con dos métodos, de este modo se puede evidenciar que tanto puede afectar el escalado al resultado de los modelos, también realicé una división del dataset en conjunto de entrenamiento y evaluación con un tamaño de muestra de evaluación de un 25%.   

Probé con varios modelos y evalué los resultados utilizando los valores de Score, Mean Absolute Error y R2 error.   

Probé los siguientes modelos:
*	**Regresión lineal múltiple** 
*	**Árbol de decisiones** 
*	**Support Vector Machine** – Dentro de este modelo probé con los kernels "rbf" y "poly de grado 2". 
*	**Random Forest** 
*	**Kneighbors** – Con este modelo hice la prueba con diferentes k vecinos obteniendo el mejor resultado entre los datos de entrenamiento y evaluación con k=5.
*	**Gradient Boosting**  

## Resultados de los modelos.
El modelo de Random Forest fue el que arrojó un mejor resultado en comparación con los otros modelos tanto en el conjunto de entrenamiento como en el conjunto de evaluación.
* **Regresión lineal múltiple** : MAE = 53.7%, R2 = 59,1%
*	**Arbol de decisiones** : MAE = 42.6%, R2 = 67.9%
*	**Support Vector Machine (Poly)** : MAE = 51.7%, R2 = 53.5% 
*	**Random Forest** : MAE = 33.8%, R2 = 79.5% (Después de depurar de los valores erróneos estos resultados cambiaron a MAE = 32.1%, R2 = 81.5%
*	**Kneighbors** : MAE = 164.1%, R2 = -149.3
*	**Gradient Boosting** : MAE = 37.3%, R2 = 77.8%

## Área de mejora a futuro
* Una manera de hacer accesible el model sería elaborar una API (se puede utilizar flask o cualquier otro similar) para poder utilizar dicho modelo con nuevos datos de una propiedad de la que se desee saber su valor medio y así poder ayudar a la compra/venta de dicha propiedad.
* Utilizar datos más actualizados de las viviendas ya que este es un dataset antiguo.
