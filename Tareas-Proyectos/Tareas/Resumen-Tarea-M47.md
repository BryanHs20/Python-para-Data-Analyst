# Resumen y Explicación - Tarea M47: Análisis de Series Temporales

**Autor:** Bryan Hernández Solís  
**Fecha:** 19 de enero de 2026  
**Dataset:** Datos históricos de acciones de Google (GOOG.csv)

---

## 📋 Objetivo del Proyecto

Este proyecto tiene como objetivo aplicar diferentes modelos de series de tiempo a datos reales de acciones de Google, incluyendo:
- Modelo de Reversión a la Media (Vasicek)
- Movimiento Browniano
- Modelos Autorregresivos (AR)
- Modelos de Media Móvil (MA)
- Predicciones con ARIMA
- Visualización de series temporales

---

## 🔍 1. Exploración y Preparación de Datos

### Importación de Librerías
Se importaron las siguientes librerías para el análisis:
- **Pandas** y **NumPy**: Manipulación de datos
- **Matplotlib** y **Seaborn**: Visualización
- **Statsmodels**: Modelos estadísticos y series temporales
- **Scikit-learn**: Métricas de evaluación
- **Plotly**: Visualizaciones interactivas

### Análisis Exploratorio de Datos (EDA)
- **Dataset**: GOOG.csv con datos históricos de acciones de Google
- **Dimensiones**: Se verificó la estructura del dataset
- **Valores nulos**: Se identificaron valores faltantes
- **Limpieza**: Se eliminaron las columnas `Dividends` y `Stock Splits` por tener pocos datos relevantes

**Columnas principales:**
- Date, Open, High, Low, Close, Volume

---

## 📊 2. Modelo de Reversión a la Media (Vasicek)

### ¿Qué es el Modelo de Vasicek?
Es un modelo matemático usado para simular la evolución de tasas de interés que tienden a revertir hacia una media a largo plazo.

### Implementación
Se creó la función `mod_vasicek()` con los siguientes parámetros:
- **r0**: Tasa inicial (0.1875)
- **k**: Velocidad de reversión (0.2)
- **theta**: Tasa media a largo plazo (0.04)
- **sigma**: Volatilidad (0.012)
- **T**: Horizonte temporal (10 años)
- **N**: Número de pasos (1000)

### Resultado
Se generó un gráfico mostrando cómo la serie temporal tiende a revertir hacia la media (línea roja) a lo largo del tiempo.

---

## 🎲 3. Movimiento Browniano

### ¿Qué es el Movimiento Browniano?
Es un proceso estocástico continuo que describe el movimiento aleatorio de partículas. En finanzas, se usa para modelar el comportamiento impredecible de los precios.

### Implementación
- **Parámetros**: Delta = 0.25, dt = 0.1
- **Trayectorias**: Se generaron 10 trayectorias diferentes
- **Iteraciones**: 20 pasos por trayectoria

### Proceso
1. Se generaron múltiples trayectorias aleatorias
2. Se almacenaron en un DataFrame con columnas: traj, nsample, sample
3. Se visualizaron todas las trayectorias en un gráfico
4. Se calcularon estadísticas (medias) de las trayectorias

### Resultado
Se observó cómo diferentes caminos aleatorios evolucionan desde un punto inicial común.

---

## 📈 4. Modelo Autorregresivo (AR)

### ¿Qué es un Modelo AR?
Un modelo AR predice valores futuros basándose en una combinación lineal de valores pasados.

### Modelos Implementados

#### AR(1) - Una dependencia
- **AR = +0.9**: Fuerte correlación positiva con el valor anterior
- **AR = -0.9**: Fuerte correlación negativa con el valor anterior

#### AR(2) - Dos dependencias
- Se expandió el modelo para incluir los dos valores anteriores

### Predicción con AR
Se utilizó el modelo ARIMA(1,0,0) para realizar forecasting sobre la primera serie simulada, obteniendo:
- Parámetros estimados del modelo
- Resumen estadístico completo

---

## 📉 5. Modelo de Media Móvil (MA)

### ¿Qué es un Modelo MA?
Un modelo MA predice valores futuros basándose en errores de predicción pasados.

### Implementación
- Se generó una serie MA(1) con parámetro -0.5
- Se aplicó ARIMA(0,0,1) para forecasting
- Se obtuvieron parámetros estimados y métricas

### Aplicación a Datos Reales de Google
1. Se calcularon las diferencias del precio de cierre (variaciones absolutas)
2. Se aplicó un modelo ARIMA(0,0,3) (MA de orden 3)
3. Se generaron predicciones para 100 períodos futuros (días 1000-1100)
4. Se evaluó el modelo con RMSE (Root Mean Square Error)

---

## 🔮 6. Predicción con Media Móvil Simple

### Metodología
1. **Cálculo de Media Móvil**: Ventana de 30 días
2. **División de datos**: 70% entrenamiento (3,770 días) - 30% prueba
3. **Predicción**: Se usó la media móvil como forecast

### Visualización
Se generó un gráfico comparando:
- Datos de entrenamiento (azul)
- Datos de prueba (naranja)
- Predicción con media móvil (verde)

### Evaluación del Modelo
Se calcularon dos métricas principales:
- **RMSE** (Root Mean Squared Error): Error promedio en unidades originales
- **MAPE** (Mean Absolute Percentage Error): Error porcentual promedio

### Comparación
Se creó una tabla comparativa mostrando los valores predichos vs. observados reales.

---

## 📊 7. Visualización de Series Temporales

### Análisis Visual del Período 2010-2020
Se generaron subgráficos para cada variable:
- Open (Precio de apertura)
- High (Precio máximo)
- Low (Precio mínimo)
- Close (Precio de cierre)
- Volume (Volumen de transacciones)

Este análisis permitió observar:
- Tendencias a largo plazo
- Patrones de volatilidad
- Comportamiento del volumen de transacciones

---

## 🎯 Conclusiones

### Modelos Teóricos
1. **Reversión a la Media**: Útil para modelar tasas de interés que tienden a estabilizarse
2. **Movimiento Browniano**: Captura la naturaleza aleatoria de los precios
3. **Modelos AR**: Capturan la autocorrelación en series temporales
4. **Modelos MA**: Modelan efectos de shocks temporales

### Predicción Práctica
- La media móvil simple proporciona predicciones razonables para datos con tendencia
- ARIMA permite modelar estructuras más complejas en series temporales
- Es fundamental evaluar los modelos con métricas como RMSE y MAPE

### Aprendizajes Clave
- Las series financieras exhiben alta volatilidad y patrones complejos
- Diferentes modelos capturan diferentes aspectos de los datos
- La visualización es crucial para entender el comportamiento temporal
- La validación con datos de prueba es esencial para evaluar el desempeño real

---

## 🛠️ Herramientas y Técnicas Utilizadas

| Categoría | Técnicas/Herramientas |
|-----------|----------------------|
| **Modelado** | Vasicek, Browniano, ARIMA, AR, MA |
| **Evaluación** | RMSE, MAPE |
| **Visualización** | Matplotlib, Seaborn, Plotly |
| **Análisis** | Statsmodels, Pandas |
| **Predicción** | Media móvil, ARIMA forecasting |

---

## 📚 Referencias

- Modelo de Vasicek para tasas de interés
- Movimiento Browniano en finanzas cuantitativas
- Modelos ARIMA (AutoRegressive Integrated Moving Average)
- Statsmodels: Statistical modeling library for Python
- Análisis de series temporales financieras

---

**Nota:** Este proyecto demuestra la aplicación práctica de modelos estocásticos y de series temporales a datos financieros reales, proporcionando una base sólida para análisis cuantitativo y predicción.
