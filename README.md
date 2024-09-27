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

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Reporte: Modelo KNN para Clasificación de Pokémon
1. Preparación de Datos
1.1 Carga de Datos

Se cargó un dataset de Pokémon desde un archivo CSV.
El dataset incluye varias características, incluyendo 'base_attack', 'base_defense', 'base_stamina', 'rarity', entre otras.

1.2 Manejo de Valores Faltantes

Se implementó una función missing() para rellenar valores faltantes utilizando forward fill y backward fill.

1.3 Análisis Exploratorio de Datos

Se identificaron las categorías únicas en la columna 'rarity': 'Standard', 'Legendary', 'Mythic', 'Ultra beast'.
Se generó una matriz de correlación y un mapa de calor para variables numéricas.
Se creó un gráfico de pares (pairplot) para visualizar relaciones entre variables.

1.4 Reducción de Dimensionalidad

Se aplicó PCA (Análisis de Componentes Principales) para reducir las dimensiones de 'base_attack', 'base_defense', y 'base_stamina' a dos componentes principales.
Se visualizó la distribución de los Pokémon en estas dos dimensiones, coloreados por 'rarity'.

2. Preparación del Modelo
2.1 Selección de Características y Objetivo

Características (X): 'base_attack', 'base_defense', 'base_stamina'
Objetivo (y): 'rarity'

2.2 División del Dataset

Se utilizó train_test_split para dividir el dataset:

80% para entrenamiento
20% para pruebas


Se utilizó random_state=123 para reproducibilidad

3. Entrenamiento y Evaluación del Modelo
3.1 Modelo Inicial

Se utilizó KNeighborsClassifier con los siguientes parámetros:

n_neighbors=5
metric='manhattan'



3.2 Evaluación Inicial

Se realizó una predicción en el conjunto de prueba.
Se calculó la matriz de confusión y la precisión (accuracy).
Precisión inicial: 0.905940594059406 (aproximadamente 90.59%)

3.3 Optimización del Hiperparámetro K

Se realizó una búsqueda de K óptimo probando valores impares de 1 a 49.
Resultados para algunos valores de K:

K=1: Accuracy=0.9108910891089109
K=5: Accuracy=0.905940594059406
K=9: Accuracy=0.900990099009901
K=15-33: Accuracy=0.9108910891089109



3.4 Modelo Final

Basado en los resultados de la búsqueda de hiperparámetros, se seleccionó K=9.
Se entrenó el modelo final con KNeighborsClassifier(n_neighbors=9, metric='manhattan')

4. Conclusiones

Rendimiento del Modelo: El modelo KNN alcanzó una precisión máxima de aproximadamente 91.09% con varios valores de K (15-33), lo cual es un buen rendimiento para un problema de clasificación multiclase.
Estabilidad del Modelo: El rendimiento del modelo se mantuvo relativamente estable para un amplio rango de valores de K (15-33), lo que sugiere que el modelo es robusto.
Elección de K: Aunque K=9 no dio el rendimiento más alto, se eligió como un equilibrio entre rendimiento y complejidad del modelo. Valores más altos de K podrían llevar a un sobreajuste.
Características Utilizadas: Las características 'base_attack', 'base_defense', y 'base_stamina' parecen ser buenos predictores de la rareza de un Pokémon.
Distribución de Clases: La matriz de confusión sugiere que puede haber un desequilibrio en las clases, con la mayoría de los Pokémon siendo 'Standard'. Esto podría afectar el rendimiento del modelo en clases minoritarias.
Mejoras Potenciales:

Considerar técnicas de balanceo de clases para mejorar la predicción en clases minoritarias.
Explorar otras métricas de distancia además de Manhattan.
Investigar la inclusión de otras características o la creación de nuevas características.
Probar otros algoritmos de clasificación y comparar rendimientos.



En general, el modelo KNN muestra un buen rendimiento en la clasificación de la rareza de los Pokémon basándose en sus estadísticas base. Sin embargo, hay espacio para mejoras, especialmente en el manejo de clases minoritarias y la exploración de características adicionales.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Reporte: Modelo de Árbol de Decisión para Pokémon
1. Proceso de Selección del Dataset de Entrenamiento
1.1 Carga de Datos

Se cargó un dataset de Pokémon desde un archivo CSV.
Se utilizaron las columnas 'base_attack', 'base_defense', y 'base_stamina'.

1.2 Preprocesamiento

Se implementó una función fill_nan_pokemon_data() para manejar valores faltantes:

Valores numéricos faltantes se rellenaron con la media de la columna.
Valores de texto faltantes se rellenaron con "Unknown".
Valores booleanos faltantes se rellenaron con False.



1.3 Selección de Características

Se seleccionaron 'base_defense' y 'base_stamina' como características (X).
Se seleccionó 'base_attack' como variable objetivo (y).

1.4 División del Dataset

Se utilizó train_test_split para dividir el dataset:

70% para entrenamiento.
30% para pruebas.


Se eliminó la primera fila de ambos conjuntos (X e y).

1.5 Codificación de Variables

Se aplicó LabelEncoder a las columnas categóricas.
Se convirtieron strings booleanos a valores booleanos reales.

2. Resultados del Entrenamiento del Modelo
2.1 Modelo Utilizado

Se utilizó un Árbol de Decisión (DecisionTreeClassifier) de scikit-learn.

2.2 Entrenamiento

Se entrenó el modelo con los datos de entrenamiento (X_train, y_train).

2.3 Predicción

Se realizaron predicciones sobre el conjunto de prueba (X_test).

2.4 Evaluación

Se calculó la precisión del modelo utilizando metrics.accuracy_score.
Resultado: Accuracy: 1.0 (100% de precisión)

3. Conclusión
El modelo de Árbol de Decisión entrenado con datos de Pokémon ha logrado una precisión perfecta (100%) en el conjunto de prueba. Sin embargo, este resultado tan perfecto plantea algunas consideraciones importantes:

Overfitting: Una precisión del 100% en el conjunto de prueba puede indicar un sobreajuste del modelo a los datos de entrenamiento. Esto podría limitar su capacidad para generalizar a nuevos datos.
Complejidad del modelo: Es posible que el árbol de decisión sea demasiado profundo, memorizando efectivamente el conjunto de entrenamiento en lugar de aprender patrones generalizables.
Tamaño y representatividad del conjunto de datos: Debemos considerar si el conjunto de datos es lo suficientemente grande y diverso como para ser representativo de todos los posibles Pokémon.
Características seleccionadas: Las características 'base_defense' y 'base_stamina' parecen ser altamente predictivas del 'base_attack'. Esto sugiere una fuerte correlación entre estos atributos en el diseño de Pokémon.
Validación adicional: Sería recomendable realizar una validación cruzada y probar el modelo con un conjunto de datos completamente nuevo para confirmar su rendimiento.
Ajuste del modelo: Considerar la aplicación de técnicas de regularización o la limitación de la profundidad del árbol para mejorar la generalización del modelo.

En resumen, aunque los resultados parecen excelentes a primera vista, es crucial realizar una evaluación más profunda y considerar posibles ajustes para asegurar que el modelo sea robusto y generalizable en la predicción de atributos de Pokémon.
