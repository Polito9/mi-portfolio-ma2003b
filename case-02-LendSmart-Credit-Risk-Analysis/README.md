# Análisis de Riesgo Crediticio - LendSmart

**Autores:**  
- Diego Colin Reyes  
- Daniel Alejandro López Martínez  
- Eduardo Ramírez Almanza  

---

## 1. Contexto del Negocio

**Descripción del Cliente y Problema:**  
**LendSmart** es una empresa FinTech especializada en préstamos personales y para pequeñas empresas. Actualmente, su cartera de préstamos presenta una **tasa de morosidad del 28%**, nivel que la dirección considera demasiado alto. La empresa necesita un modelo predictivo que identifique de manera precisa a los solicitantes de alto riesgo antes de aprobar los préstamos.

**Importancia Estratégica:**  
Este análisis convierte datos crediticios en un **modelo de clasificación predictivo** que permite a LendSmart:  
- **Reducir pérdidas financieras** al minimizar la aprobación de préstamos que eventualmente entrarán en mora.  
- **Optimizar la rentabilidad** al mantener un nivel aceptable de préstamos "buenos" rechazados (falsos positivos).  
- **Mejorar la toma de decisiones** mediante la identificación de los factores clave que impulsan el riesgo de incumplimiento.  
- **Incrementar la confianza de los inversionistas** mediante una gestión de riesgo más científica y basada en datos.  

---

## 2. Metodología

**Métodos de Clasificación Aplicados:**  
Se compararon dos técnicas de análisis discriminante:  
1. **Análisis Discriminante Lineal (LDA)**: Asume que las clases comparten la misma matriz de covarianza.  
2. **Análisis Discriminante Cuadrático (QDA)**: Permite que cada clase tenga su propia matriz de covarianza.  

**Justificación:**  
- **Preparación de Datos**: Se aplicó **codificación one-hot** a variables categóricas (`education_level`, `marital_status`) y **estandarización** de características numéricas usando `StandardScaler`.  
- **División de Datos**: Se utilizó una división 80-20 (entrenamiento-prueba) con `stratify=y` para mantener la proporción de clases.  
- **Supuestos Estadísticos**: Se discutieron los supuestos de normalidad multivariada y homogeneidad de matrices de covarianza, hipotetizando que QDA superaría a LDA debido a las diferencias observadas en las distribuciones.  

**Herramientas y Librerías:**  
- **Python**: Lenguaje de programación principal.  
- **Pandas & NumPy**: Manipulación y análisis de datos.  
- **Scikit-learn**: Implementación de LDA, QDA, StandardScaler, train_test_split y métricas de evaluación.  
- **Plotly**: Visualizaciones interactivas de resultados y análisis exploratorio.  

---

## 3. Datos

**Descripción del Conjunto de Datos:**  
El análisis se basó en el archivo `credit_risk_data.csv`, que contiene **2,500 solicitudes de préstamo** con **18 variables** cada una.

**Variables Clave:**  
El conjunto de variables incluye:  

- **Variables Predictoras (17 características)**:  
  - **Financieras**: `annual_income`, `loan_amount`, `debt_to_income_ratio`, `savings_ratio`, `asset_value`.  
  - **Crediticias**: `credit_score`, `credit_utilization`, `payment_history_score`, `open_credit_lines`.  
  - **Laborales y Demográficas**: `employment_years`, `job_stability_score`, `age`, `education_level`, `marital_status`, `residential_stability`.  

- **Variable Objetivo (1 variable)**:  
  - `loan_status`: Indicador binario (0 = No moroso, 1 = Moroso).  

**Calidad de Datos:**  
- No se encontraron valores nulos en el conjunto de datos.  
- Las distribuciones mostraron separabilidad clara entre morosos y no morosos.  

---

## 4. Hallazgos Clave

El análisis concluyó que ambos modelos (LDA y QDA) logran un **desempeño perfecto** en el conjunto de prueba, con **100% de precisión y AUC de 1.0000**.

**Factores Críticos (Identificados mediante Coeficientes LDA):**  
Los principales impulsores del riesgo de incumplimiento, en orden de importancia, son:  
1. **`payment_history_score`** (Coef: -15.47): Historial de pagos sólido reduce drásticamente el riesgo.  
2. **`job_stability_score`** (Coef: -13.05): Estabilidad laboral como factor clave de confiabilidad.  
3. **`credit_utilization`** (Coef: +11.77): Alto uso de crédito disponible aumenta significativamente el riesgo.  
4. **`debt_to_income_ratio`** (Coef: +4.47): Mayor endeudamiento relativo a ingresos incrementa la probabilidad de mora.  
5. **`credit_score`** (Coef: -3.98): Puntaje crediticio alto reduce el riesgo, como es esperado.  

**Perfil de Alto Riesgo:**  
- Historial de pagos bajo.  
- Baja estabilidad laboral.  
- Alta utilización de crédito disponible.  
- Elevada relación deuda-ingresos.  

**Selección del Modelo:**  
Aunque ambos modelos son perfectos, se recomienda **LDA** por su **interpretabilidad**, ya que proporciona coeficientes lineales que explican claramente el impacto de cada variable en la decisión crediticia.  

---

## 5. Recomendaciones de Negocio

**Recomendación Principal:**  
Implementar el **modelo LDA** en el proceso de evaluación de solicitudes de préstamo de LendSmart.

**Impacto Esperado:**  
- **Identificación del 100% de los morosos** en los datos de prueba.  
- **Reducción drástica de pérdidas** por préstamos incobrables.  
- **Mayor eficiencia en la asignación de capital** al aprobar solo préstamos de bajo riesgo.  
- **Transparencia en las decisiones** gracias a la interpretabilidad del modelo.  

**Compensación Empresarial (Trade-Off):**  
El modelo perfecto implica que no se rechazarán buenos clientes ni se aprobarán malos préstamos en los datos de prueba, lo que representa un escenario ideal sin compensaciones en este conjunto de datos.

**Próximos Pasos:**  
- **Validación en datos en tiempo real** para confirmar el desempeño del modelo fuera del conjunto de prueba.  
- **Desarrollo de un sistema de scoring** basado en los coeficientes de LDA para uso operativo.  
- **Monitoreo continuo** del modelo para detectar cambios en los patrones de riesgo crediticio.