# Modelo SIR Mejorado con Machine Learning (Gradient Boosting Regressor)para COVID-19 en Argentina

## Descripción

Este proyecto implementa un modelo epidemiológico basado en la clásica dinámica SIR (Susceptibles-Infectados-Recuperados) para analizar y simular la evolución del COVID-19 en Argentina. 

La particularidad es que los parámetros clave del modelo, la tasa de transmisión **β(t)** y la tasa de recuperación **γ(t)**, son estimados dinámicamente mediante modelos de Machine Learning utilizando datos reales disponibles a nivel nacional y provincial.

---

## Estructura del Proyecto

- `Argentina-covid19.csv` — Datos nacionales diarios de COVID-19.
- `Argentina-covid19-por-provincia.csv` — Datos provinciales diarios.
- `Argentina-covid19-fallecidos.csv` — Datos de fallecidos con detalles demográficos.
- `sir_ml_model.py` — Script principal que carga datos, entrena los modelos y simula la evolución SIR.
- `README.md` — Este archivo.

---

## Descripción del Código

### 1. Carga y Preprocesamiento

- Se combinan fuentes de datos nacionales, provinciales y de fallecidos.
- Se construyen variables clave:
  - Infectados activos (`I`)
  - Recuperados (`R`)
  - Susceptibles (`S`)
  - Positividad (tests positivos / tests realizados)
  - Gravedad (UTI ocupadas / casos activos)
  - Edad promedio de fallecidos, etc.
- Se filtran días con baja cantidad de casos activos y se completan datos faltantes.

### 2. Simulador SIR

- Se implementa el modelo clásico de ecuaciones diferenciales discretizadas.
- Se usa una población total de 45 millones.
- Se simula la evolución de S, I y R en función de los parámetros estimados.

### 3. Entrenamiento con Machine Learning

- Se calculan las tasas empíricas diarias de β y γ.
- Se suavizan los valores con filtros gaussianos.
- Se entrena un modelo de regresión por Gradient Boosting para predecir:
  - **β(t)**: tasa de contagio
  - **γ(t)**: tasa de recuperación
- Variables utilizadas (features):
  - `dia_cuarentena`, `positividad`, `gravedad`, `edad_mean`, 
    `casos_nuevos_prov`, `UTI_%Nacion`, `mes`, `semana`, `tendencia_I`

### 4. Evaluación y Visualización

- Se simula el modelo SIR usando los parámetros estimados.
- Se calculan métricas:
  - MSE (Error Cuadrático Medio)
  - R² (Coeficiente de Determinación)
- Se grafican:
  - Infectados reales vs simulados
  - Evolución de β(t) y γ(t)
  - Número de reproducción R₀(t) = β(t) / γ(t)

---

## Cómo Ejecutar

1. Asegurate de tener los tres archivos `.csv` en la misma carpeta.
2. Instalá las dependencias necesarias:
   ```bash
   pip install pandas numpy matplotlib scikit-learn scipy
   ```
3. Ejecutá el script:
   ```bash
   python sir_ml_model.py
   ```

---

## Tecnologías Utilizadas

- **Python 3.x**
- **Pandas** — manipulación de datos
- **NumPy** — cálculos numéricos
- **Matplotlib** — visualización
- **Scikit-learn** — modelos de Machine Learning (Gradient Boosting)
- **SciPy** — filtros y suavizado de datos

---

## Posibles Mejoras

- Agregar variables de movilidad o vacunación
- Validación cruzada y tuning de hiperparámetros
- Modelos regionales (por provincia)
- Uso de modelos no paramétricos o redes neuronales

---

## Autor

**Wilson Lombardo**

---

