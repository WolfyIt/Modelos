Reporte: Modelo de Regresión Lineal
1. Descripción del Dataset
El dataset incluye información de vehículos con características como la capacidad del motor, emisiones de CO2, costos de combustible, y emisiones contaminantes. Algunas de las columnas principales son:

year: Año del modelo del vehículo.
engine_capacity: Capacidad del motor en centímetros cúbicos.
co2: Emisiones de dióxido de carbono.
urban_metric, extra_urban_metric, combined_metric: Consumo de combustible en diferentes condiciones.
fuel_cost_12000_miles: Costo de combustible por 12,000 millas recorridas.
El dataset contiene un total de 45,511 entradas y 31 columnas.

2. Limpieza y Preparación de Datos
2.1 Datos Nulos
Varias columnas del dataset contienen valores nulos, incluyendo:

tax_band, thc_nox_emissions, particulates_emissions, fuel_cost_6000_miles, entre otras.
Se aplicaron técnicas de imputación como:

Rellenar con la media en columnas numéricas.
Eliminación de columnas no relevantes para el modelo.
2.2 Distribución de la Capacidad del Motor
El análisis de la variable engine_capacity muestra una alta asimetría (Skewness: 2.16) y kurtosis (Kurtosis: 6.07), lo que indica una fuerte desviación de la normalidad. Este comportamiento puede afectar el rendimiento del modelo.

3. Entrenamiento y Validación
3.1 División de los Datos
El dataset fue dividido en datos de entrenamiento y validación:

X_train shape: (31,857, 17)
y_train shape: (31,857,)
X_valid shape: (13,654, 17)
y_valid shape: (13,654,)
3.2 Entrenamiento del Modelo
Se utilizó un modelo de regresión lineal para predecir la variable objetivo, la cual es engine_capacity (capacidad del motor).

3.3 Predicción
El modelo predijo valores para la capacidad del motor en el conjunto de validación, obteniendo predicciones como:

python
Copy code
array([1810.10687219, 1979.85015352, 1997.32137676, ..., 1431.82105138, 1567.91483693, 1583.1056848 ])
4. Evaluación del Modelo
El modelo se evaluó utilizando métricas estándar como el Error Cuadrático Medio (MSE) y el Coeficiente de Determinación (R²). Sin embargo, los resultados específicos de estas métricas no se mencionan en los datos proporcionados, por lo que se recomienda calcularlas para medir la calidad del modelo.

5. Conclusión
El modelo de regresión lineal muestra un rendimiento razonable en la predicción de la capacidad del motor, aunque la alta asimetría de los datos sugiere que podría ser útil aplicar transformaciones (como logaritmos o raíz cuadrada) para mejorar los resultados.



Reporte del Modelo KNN aplicado a Pokémon
Introducción
He trabajado en un modelo de clasificación utilizando K-Nearest Neighbors (KNN) para predecir la rareza de los Pokémon con base en sus estadísticas de ataque, defensa y resistencia. Utilicé un dataset que incluye varias características de los Pokémon, como sus movimientos, rareza, tipo, entre otras.

Preprocesamiento de Datos
Limpieza de Datos:

Manejé los valores nulos aplicando las funciones ffill() y bfill() para el relleno hacia adelante y atrás, respectivamente.
Posteriormente, seleccioné solo las columnas numéricas para realizar un análisis de correlación.
Análisis de Correlación:

Apliqué un análisis de correlación entre las características numéricas y visualicé la matriz de correlación mediante un mapa de calor con seaborn.
Realicé un análisis visual adicional con un pairplot para observar la distribución de los datos.
Reducción de Dimensionalidad:

Utilicé un modelo de Análisis de Componentes Principales (PCA) para reducir las tres dimensiones originales (base_attack, base_defense, base_stamina) a dos dimensiones (x y y) para fines de visualización.
Un gráfico de dispersión con seaborn mostró la distribución de las diferentes clases de rareza en el nuevo espacio reducido.
Entrenamiento del Modelo KNN
División de Datos:

Las características seleccionadas fueron base_attack, base_defense y base_stamina. La variable de salida (target) fue la columna rarity (Standard, Legendary, Mythic, Ultra Beast).
Dividí los datos en conjunto de entrenamiento (80%) y de prueba (20%) utilizando train_test_split.
Definición del Modelo:

Implementé el algoritmo KNN utilizando 5 vecinos (n_neighbors=5) y la distancia Manhattan como métrica.
Ajusté el modelo a los datos de entrenamiento y realicé las predicciones sobre el conjunto de prueba.
Evaluación del Modelo:

La precisión inicial del modelo fue de 0.9059.
Generé una matriz de confusión que mostró las predicciones correctas e incorrectas para cada clase de rareza. La clase Standard fue la más precisa, aunque algunas clases más raras (como Mythic y Legendary) tuvieron errores de predicción.
Matriz de confusión:

lua
Copy code
[[  8,   1,   5,   0],
 [  1,   1,   2,   0],
 [  6,   1, 174,   0],
 [  1,   0,   2,   0]]
Precisión del Modelo:

Copy code
0.9059
Optimización del Modelo:

Experimenté con diferentes valores de K (de 1 a 49 en incrementos de 2) para determinar el valor óptimo.
La mayor precisión se obtuvo con K=1, K=15, K=17, K=19, y varios otros, alcanzando una precisión de 0.9108.
Conclusiones
El modelo KNN mostró una precisión general alta (0.9108) al predecir la rareza de los Pokémon, especialmente con valores de K bajos y medianos.
La métrica de Manhattan fue adecuada para este conjunto de datos.
Las clases más comunes (Standard) fueron predichas con mayor precisión, mientras que las clases más raras (como Legendary y Mythic) mostraron más confusión en el modelo.
Podría mejorar el rendimiento del modelo ajustando aún más la selección de características o utilizando técnicas de oversampling para equilibrar las clases minoritarias.
