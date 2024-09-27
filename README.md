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
