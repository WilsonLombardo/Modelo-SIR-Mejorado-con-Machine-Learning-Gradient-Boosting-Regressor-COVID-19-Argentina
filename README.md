Modelo SIR Mejorado con Machine Learning para COVID-19 en Argentina
Descripción
Este proyecto implementa un modelo epidemiológico basado en la clásica dinámica SIR (Susceptibles-Infectados-Recuperados) para analizar y simular la evolución del COVID-19 en Argentina.

La particularidad es que los parámetros clave del modelo, la tasa de transmisión 
𝛽
(
𝑡
)
β(t) y la tasa de recuperación/remoción 
𝛾
(
𝑡
)
γ(t), son estimados dinámicamente mediante modelos de Machine Learning usando datos reales disponibles a nivel nacional y provincial.

Estructura del Proyecto
Argentina-covid19.csv — Datos nacionales diarios de COVID-19.

Argentina-covid19-por-provincia.csv — Datos provinciales diarios.

Argentina-covid19-fallecidos.csv — Datos de fallecidos con detalles demográficos.

sir_ml_model.py — Script principal que carga datos, entrena los modelos y simula la evolución SIR.

README.md — Este archivo.

Descripción del Código
1. Carga y Preprocesamiento
Se leen y combinan tres fuentes de datos con información nacional, provincial y de fallecidos.

Se crean variables epidemiológicas clave:

Infectados activos 
𝐼
I, recuperados/removidos 
𝑅
R, susceptibles 
𝑆
S.

Variables auxiliares: positividad, gravedad (uso UTI), edad promedio de fallecidos, etc.

Se limpian y rellenan datos faltantes para garantizar consistencia.

Se establece un umbral mínimo de infectados para análisis (>100 activos).

2. Simulación SIR Mejorada
La evolución del sistema SIR se modela usando los parámetros dinámicos 
𝛽
(
𝑡
)
β(t) y 
𝛾
(
𝑡
)
γ(t) estimados.

Se calcula la variación diaria de susceptibles, infectados y recuperados.

3. Entrenamiento de Modelos de Machine Learning
Se calculan valores empíricos diarios para 
𝛽
β y 
𝛾
γ a partir de diferencias numéricas y poblaciones.

Se suavizan estos valores para evitar ruido.

Se seleccionan características explicativas relevantes:

Variables temporales: día de cuarentena, mes, semana.

Indicadores epidemiológicos: positividad, gravedad, casos nuevos provinciales.

Datos demográficos: edad promedio fallecidos, porcentaje de UTI ocupadas.

Tendencias de infectados.

Se entrenan dos modelos de regresión con Gradient Boosting Regressor para 
𝛽
(
𝑡
)
β(t) y 
𝛾
(
𝑡
)
γ(t).

Se obtienen predicciones para todos los días.

4. Evaluación y Visualización
Se simula la evolución SIR con los parámetros estimados.

Se calculan métricas de calidad:

Error cuadrático medio (MSE).

Coeficiente de determinación (R²).

Se grafican:

Infectados reales vs. simulados.

Evolución temporal de 
𝛽
(
𝑡
)
β(t) y 
𝛾
(
𝑡
)
γ(t).

Número reproductivo básico estimado 
𝑅
0
(
𝑡
)
=
𝛽
(
𝑡
)
𝛾
(
𝑡
)
R 
0
​
 (t)= 
γ(t)
β(t)
​
 .

Cómo Ejecutar
Asegúrate de tener los archivos CSV en la carpeta del proyecto.

Instala las dependencias necesarias:

bash
Copiar
Editar
pip install pandas numpy matplotlib scikit-learn scipy
Ejecuta el script:

bash
Copiar
Editar
python sir_ml_model.py
Observa las métricas impresas y las gráficas generadas que muestran el ajuste y dinámica de la epidemia.

Tecnologías Utilizadas
Python 3.x

Pandas para manipulación de datos.

NumPy para cálculos numéricos.

Matplotlib para visualizaciones.

Scikit-learn para modelos de Machine Learning (Gradient Boosting Regressor).

SciPy para filtrado y suavizado de señales.

Notas Importantes
El modelo asume una población fija (45 millones) y condiciones homogéneas a nivel nacional.

El entrenamiento depende de la calidad y consistencia de los datos originales.

La predicción de 
𝛽
(
𝑡
)
β(t) y 
𝛾
(
𝑡
)
γ(t) permite adaptar el modelo SIR a cambios en políticas, comportamiento social, y características epidemiológicas.

El enfoque puede extenderse para incorporar más covariables o modelos más complejos.

Posibles Mejoras
Integrar datos de movilidad o vacunación.

Evaluar otros modelos ML o deep learning para estimar parámetros.

Incorporar variabilidad regional mediante modelos espaciales.

Hacer validación cruzada y ajuste fino de hiperparámetros ML.

Autor
Wilson Lombardo

