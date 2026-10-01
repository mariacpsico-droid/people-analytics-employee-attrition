# People Analytics: Employee Attrition & Retention

## Análisis de factores asociados a la rotación de empleados

### Descripción del proyecto

Este proyecto analiza patrones asociados con la rotación de empleados utilizando técnicas de análisis exploratorio de datos y Machine Learning.

El objetivo es identificar qué características del entorno laboral, puesto, experiencia y perfil del empleado muestran asociaciones con la rotación, y explorar cómo esta información podría utilizarse en un contexto de People Analytics para apoyar estrategias de retención.

> **Nota:** El dataset utilizado es un conjunto de datos de práctica utilizado para análisis de HR Analytics. Los resultados de este proyecto no representan empleados reales ni deben interpretarse como evidencia causal.

---

## Pregunta de negocio

**¿Qué patrones están asociados con la rotación de empleados y qué información podría utilizar un equipo de People Analytics para diseñar acciones de retención?**

---

## Objetivos

* Explorar la distribución de la rotación de empleados.
* Identificar variables asociadas con `Attrition`.
* Comparar tasas de rotación entre diferentes grupos de empleados.
* Analizar relaciones entre variables numéricas y rotación.
* Construir un modelo de clasificación para identificar patrones asociados con posibles casos de rotación.
* Evaluar el desempeño del modelo.
* Traducir los resultados en posibles líneas de acción para People Analytics.

---

## Dataset

**IBM HR Analytics Employee Attrition & Performance**

El dataset contiene información relacionada con características demográficas, laborales y de satisfacción de empleados.

El conjunto de datos utilizado contiene:

* **1,470 registros**
* **35 variables originales**
* **32 variables utilizadas para el análisis**, después de eliminar variables constantes.

La variable objetivo es:

* `Attrition = Yes`: empleado con rotación.
* `Attrition = No`: empleado sin rotación.

La tasa de rotación observada en el dataset es de **16.12%**.

---

## Herramientas utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

---

## Análisis exploratorio

Durante el análisis se estudiaron variables categóricas y numéricas relacionadas con:

* Horas extra
* Frecuencia de viajes
* Departamento
* Rol del empleado
* Edad
* Ingreso mensual
* Antigüedad en la empresa
* Satisfacción laboral
* Satisfacción con el entorno
* Distancia desde el hogar
* Experiencia laboral
* Nivel del puesto
* Estado civil
* Otras características laborales

### Principales patrones observados

Los empleados que realizan horas extra presentan una tasa de rotación observada mayor que aquellos que no realizan horas extra.

También se observaron diferencias en la rotación según la frecuencia de viajes y el rol del empleado.

En las variables numéricas, los empleados que presentaron rotación mostraron, en promedio, menor edad, menor ingreso mensual y menor antigüedad en la empresa.

Las variables relacionadas con satisfacción laboral y experiencia dentro de la empresa también mostraron diferencias entre los grupos.

Estos resultados representan **asociaciones observadas** y no permiten establecer relaciones de causalidad.

---

## Machine Learning

Se construyó un modelo de **Regresión Logística** para analizar simultáneamente múltiples variables.

### Preparación de los datos

* Separación entre variables predictoras (`X`) y variable objetivo (`y`).
* División de los datos en entrenamiento y prueba.
* Uso de `OneHotEncoder` para variables categóricas.
* Eliminación de categorías de referencia mediante `drop="first"`.
* Estandarización de variables numéricas mediante `StandardScaler`.
* Eliminación de `EmployeeNumber` como identificador.

### Modelo

```python
LogisticRegression(
    max_iter=1000,
    random_state=42
)
```

---

## Resultados del modelo

El modelo obtuvo un **ROC-AUC de 0.81** en el conjunto de prueba.

Con el umbral predeterminado de 0.50:

| Métrica               | Resultado |
| --------------------- | --------: |
| ROC-AUC               |      0.81 |
| Accuracy              |      0.86 |
| Precision (Attrition) |      0.64 |
| Recall (Attrition)    |      0.34 |
| F1 (Attrition)        |      0.44 |

Debido al desequilibrio entre las clases, la accuracy no debe interpretarse como la única medida del desempeño. Para la clase `Attrition = Yes`, el recall resulta especialmente relevante para evaluar cuántos casos reales de rotación fueron identificados por el modelo.

---

## Análisis del umbral

También se evaluaron diferentes umbrales de clasificación.

Reducir el umbral incrementa el recall de la clase `Attrition = Yes`, pero también puede aumentar el número de falsos positivos.

Por ejemplo:

* Umbral **0.50** → Recall: **0.34**
* Umbral **0.30** → Recall: **0.51**
* Umbral **0.25** → Recall: **0.64**

La selección del umbral depende del objetivo del análisis y del costo relativo de los falsos positivos y falsos negativos.

---

## Principales variables identificadas por el modelo

Entre las variables con mayores asociaciones positivas con la probabilidad estimada de `Attrition = Yes` se encuentran:

* `OverTime = Yes`
* `BusinessTravel = Travel_Frequently`
* `JobRole = Laboratory Technician`
* `JobRole = Sales Representative`
* `MaritalStatus = Single`

Entre las variables numéricas, el modelo también identificó asociaciones relevantes con variables como:

* `YearsSinceLastPromotion`
* `NumCompaniesWorked`
* `DistanceFromHome`

Los coeficientes del modelo deben interpretarse teniendo en cuenta que las variables numéricas fueron estandarizadas y que las variables categóricas se comparan con sus respectivas categorías de referencia.

---

## Recomendaciones para People Analytics

A partir de los patrones observados, un equipo de People Analytics podría considerar:

1. **Monitorear las horas extra y la carga de trabajo**, especialmente en equipos donde exista una concentración elevada de horas extra.

2. **Analizar los roles con mayores tasas de rotación observada** para investigar posibles diferencias en carga de trabajo, satisfacción, desarrollo profesional y condiciones laborales.

3. **Prestar atención a empleados durante las primeras etapas de permanencia**, utilizando indicadores como satisfacción, antigüedad, desarrollo profesional y experiencia con el manager.

4. **Combinar información de satisfacción con otros indicadores laborales** para comprender mejor la experiencia del empleado.

5. **Utilizar modelos predictivos como herramientas de apoyo**, evitando utilizarlos de manera automática para tomar decisiones individuales sobre empleados.

---

## Limitaciones

Este proyecto presenta algunas limitaciones importantes:

* El dataset es un conjunto de datos de práctica y no representa una organización real.
* Los resultados muestran asociaciones y no causalidad.
* La variable objetivo presenta un desequilibrio entre las clases.
* El modelo tiene un recall limitado para la clase `Attrition = Y
# People Analytics: Employee Attrition & Retention

## Análisis de factores asociados a la rotación de empleados

### Descripción del proyecto

Este proyecto analiza patrones asociados con la rotación de empleados utilizando técnicas de análisis exploratorio de datos y Machine Learning.

El objetivo es identificar qué características del entorno laboral, puesto, experiencia y perfil del empleado muestran asociaciones con la rotación, y explorar cómo esta información podría utilizarse en un contexto de People Analytics para apoyar estrategias de retención.

> **Nota:** El dataset utilizado es un conjunto de datos de práctica utilizado para análisis de HR Analytics. Los resultados de este proyecto no representan empleados reales ni deben interpretarse como evidencia causal.

---

## Pregunta de negocio

**¿Qué patrones están asociados con la rotación de empleados y qué información podría utilizar un equipo de People Analytics para diseñar acciones de retención?**

---

## Objetivos

* Explorar la distribución de la rotación de empleados.
* Identificar variables asociadas con `Attrition`.
* Comparar tasas de rotación entre diferentes grupos de empleados.
* Analizar relaciones entre variables numéricas y rotación.
* Construir un modelo de clasificación para identificar patrones asociados con posibles casos de rotación.
* Evaluar el desempeño del modelo.
* Traducir los resultados en posibles líneas de acción para People Analytics.

---

## Dataset

**IBM HR Analytics Employee Attrition & Performance**

El dataset contiene información relacionada con características demográficas, laborales y de satisfacción de empleados.

El conjunto de datos utilizado contiene:

* **1,470 registros**
* **35 variables originales**
* **32 variables utilizadas para el análisis**, después de eliminar variables constantes.

La variable objetivo es:

* `Attrition = Yes`: empleado con rotación.
* `Attrition = No`: empleado sin rotación.

La tasa de rotación observada en el dataset es de **16.12%**.

---

## Herramientas utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

---

## Análisis exploratorio

Durante el análisis se estudiaron variables categóricas y numéricas relacionadas con:

* Horas extra
* Frecuencia de viajes
* Departamento
* Rol del empleado
* Edad
* Ingreso mensual
* Antigüedad en la empresa
* Satisfacción laboral
* Satisfacción con el entorno
* Distancia desde el hogar
* Experiencia laboral
* Nivel del puesto
* Estado civil
* Otras características laborales

### Principales patrones observados

Los empleados que realizan horas extra presentan una tasa de rotación observada mayor que aquellos que no realizan horas extra.

También se observaron diferencias en la rotación según la frecuencia de viajes y el rol del empleado.

En las variables numéricas, los empleados que presentaron rotación mostraron, en promedio, menor edad, menor ingreso mensual y menor antigüedad en la empresa.

Las variables relacionadas con satisfacción laboral y experiencia dentro de la empresa también mostraron diferencias entre los grupos.

Estos resultados representan **asociaciones observadas** y no permiten establecer relaciones de causalidad.

---

## Machine Learning

Se construyó un modelo de **Regresión Logística** para analizar simultáneamente múltiples variables.

### Preparación de los datos

* Separación entre variables predictoras (`X`) y variable objetivo (`y`).
* División de los datos en entrenamiento y prueba.
* Uso de `OneHotEncoder` para variables categóricas.
* Eliminación de categorías de referencia mediante `drop="first"`.
* Estandarización de variables numéricas mediante `StandardScaler`.
* Eliminación de `EmployeeNumber` como identificador.

### Modelo

```python
LogisticRegression(
    max_iter=1000,
    random_state=42
)
```

---

## Resultados del modelo

El modelo obtuvo un **ROC-AUC de 0.81** en el conjunto de prueba.

Con el umbral predeterminado de 0.50:

| Métrica               | Resultado |
| --------------------- | --------: |
| ROC-AUC               |      0.81 |
| Accuracy              |      0.86 |
| Precision (Attrition) |      0.64 |
| Recall (Attrition)    |      0.34 |
| F1 (Attrition)        |      0.44 |

Debido al desequilibrio entre las clases, la accuracy no debe interpretarse como la única medida del desempeño. Para la clase `Attrition = Yes`, el recall resulta especialmente relevante para evaluar cuántos casos reales de rotación fueron identificados por el modelo.

---

## Análisis del umbral

También se evaluaron diferentes umbrales de clasificación.

Reducir el umbral incrementa el recall de la clase `Attrition = Yes`, pero también puede aumentar el número de falsos positivos.

Por ejemplo:

* Umbral **0.50** → Recall: **0.34**
* Umbral **0.30** → Recall: **0.51**
* Umbral **0.25** → Recall: **0.64**

La selección del umbral depende del objetivo del análisis y del costo relativo de los falsos positivos y falsos negativos.

---

## Principales variables identificadas por el modelo

Entre las variables con mayores asociaciones positivas con la probabilidad estimada de `Attrition = Yes` se encuentran:

* `OverTime = Yes`
* `BusinessTravel = Travel_Frequently`
* `JobRole = Laboratory Technician`
* `JobRole = Sales Representative`
* `MaritalStatus = Single`

Entre las variables numéricas, el modelo también identificó asociaciones relevantes con variables como:

* `YearsSinceLastPromotion`
* `NumCompaniesWorked`
* `DistanceFromHome`

Los coeficientes del modelo deben interpretarse teniendo en cuenta que las variables numéricas fueron estandarizadas y que las variables categóricas se comparan con sus respectivas categorías de referencia.

---

## Recomendaciones para People Analytics

A partir de los patrones observados, un equipo de People Analytics podría considerar:

1. **Monitorear las horas extra y la carga de trabajo**, especialmente en equipos donde exista una concentración elevada de horas extra.

2. **Analizar los roles con mayores tasas de rotación observada** para investigar posibles diferencias en carga de trabajo, satisfacción, desarrollo profesional y condiciones laborales.

3. **Prestar atención a empleados durante las primeras etapas de permanencia**, utilizando indicadores como satisfacción, antigüedad, desarrollo profesional y experiencia con el manager.

4. **Combinar información de satisfacción con otros indicadores laborales** para comprender mejor la experiencia del empleado.

5. **Utilizar modelos predictivos como herramientas de apoyo**, evitando utilizarlos de manera automática para tomar decisiones individuales sobre empleados.

---

## Limitaciones

Este proyecto presenta algunas limitaciones importantes:

* El dataset es un conjunto de datos de práctica y no representa una organización real.
* Los resultados muestran asociaciones y no causalidad.
* La variable objetivo presenta un desequilibrio entre las clases.
* El modelo tiene un recall limitado para la clase `Attrition = Y
# People Analytics: Employee Attrition & Retention

## Análisis de factores asociados a la rotación de empleados

### Descripción del proyecto

Este proyecto analiza patrones asociados con la rotación de empleados utilizando técnicas de análisis exploratorio de datos y Machine Learning.

El objetivo es identificar qué características del entorno laboral, puesto, experiencia y perfil del empleado muestran asociaciones con la rotación, y explorar cómo esta información podría utilizarse en un contexto de People Analytics para apoyar estrategias de retención.

> **Nota:** El dataset utilizado es un conjunto de datos de práctica utilizado para análisis de HR Analytics. Los resultados de este proyecto no representan empleados reales ni deben interpretarse como evidencia causal.

---

## Pregunta de negocio

**¿Qué patrones están asociados con la rotación de empleados y qué información podría utilizar un equipo de People Analytics para diseñar acciones de retención?**

---

## Objetivos

* Explorar la distribución de la rotación de empleados.
* Identificar variables asociadas con `Attrition`.
* Comparar tasas de rotación entre diferentes grupos de empleados.
* Analizar relaciones entre variables numéricas y rotación.
* Construir un modelo de clasificación para identificar patrones asociados con posibles casos de rotación.
* Evaluar el desempeño del modelo.
* Traducir los resultados en posibles líneas de acción para People Analytics.

---

## Dataset

**IBM HR Analytics Employee Attrition & Performance**

El dataset contiene información relacionada con características demográficas, laborales y de satisfacción de empleados.

El conjunto de datos utilizado contiene:

* **1,470 registros**
* **35 variables originales**
* **32 variables utilizadas para el análisis**, después de eliminar variables constantes.

La variable objetivo es:

* `Attrition = Yes`: empleado con rotación.
* `Attrition = No`: empleado sin rotación.

La tasa de rotación observada en el dataset es de **16.12%**.

---

## Herramientas utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

---

## Análisis exploratorio

Durante el análisis se estudiaron variables categóricas y numéricas relacionadas con:

* Horas extra
* Frecuencia de viajes
* Departamento
* Rol del empleado
* Edad
* Ingreso mensual
* Antigüedad en la empresa
* Satisfacción laboral
* Satisfacción con el entorno
* Distancia desde el hogar
* Experiencia laboral
* Nivel del puesto
* Estado civil
* Otras características laborales

### Principales patrones observados

Los empleados que realizan horas extra presentan una tasa de rotación observada mayor que aquellos que no realizan horas extra.

También se observaron diferencias en la rotación según la frecuencia de viajes y el rol del empleado.

En las variables numéricas, los empleados que presentaron rotación mostraron, en promedio, menor edad, menor ingreso mensual y menor antigüedad en la empresa.

Las variables relacionadas con satisfacción laboral y experiencia dentro de la empresa también mostraron diferencias entre los grupos.

Estos resultados representan **asociaciones observadas** y no permiten establecer relaciones de causalidad.

---

## Machine Learning

Se construyó un modelo de **Regresión Logística** para analizar simultáneamente múltiples variables.

### Preparación de los datos

* Separación entre variables predictoras (`X`) y variable objetivo (`y`).
* División de los datos en entrenamiento y prueba.
* Uso de `OneHotEncoder` para variables categóricas.
* Eliminación de categorías de referencia mediante `drop="first"`.
* Estandarización de variables numéricas mediante `StandardScaler`.
* Eliminación de `EmployeeNumber` como identificador.

### Modelo

```python
LogisticRegression(
    max_iter=1000,
    random_state=42
)
```

---

## Resultados del modelo

El modelo obtuvo un **ROC-AUC de 0.81** en el conjunto de prueba.

Con el umbral predeterminado de 0.50:

| Métrica               | Resultado |
| --------------------- | --------: |
| ROC-AUC               |      0.81 |
| Accuracy              |      0.86 |
| Precision (Attrition) |      0.64 |
| Recall (Attrition)    |      0.34 |
| F1 (Attrition)        |      0.44 |

Debido al desequilibrio entre las clases, la accuracy no debe interpretarse como la única medida del desempeño. Para la clase `Attrition = Yes`, el recall resulta especialmente relevante para evaluar cuántos casos reales de rotación fueron identificados por el modelo.

---

## Análisis del umbral

También se evaluaron diferentes umbrales de clasificación.

Reducir el umbral incrementa el recall de la clase `Attrition = Yes`, pero también puede aumentar el número de falsos positivos.

Por ejemplo:

* Umbral **0.50** → Recall: **0.34**
* Umbral **0.30** → Recall: **0.51**
* Umbral **0.25** → Recall: **0.64**

La selección del umbral depende del objetivo del análisis y del costo relativo de los falsos positivos y falsos negativos.

---

## Principales variables identificadas por el modelo

Entre las variables con mayores asociaciones positivas con la probabilidad estimada de `Attrition = Yes` se encuentran:

* `OverTime = Yes`
* `BusinessTravel = Travel_Frequently`
* `JobRole = Laboratory Technician`
* `JobRole = Sales Representative`
* `MaritalStatus = Single`

Entre las variables numéricas, el modelo también identificó asociaciones relevantes con variables como:

* `YearsSinceLastPromotion`
* `NumCompaniesWorked`
* `DistanceFromHome`

Los coeficientes del modelo deben interpretarse teniendo en cuenta que las variables numéricas fueron estandarizadas y que las variables categóricas se comparan con sus respectivas categorías de referencia.

---

## Recomendaciones para People Analytics

A partir de los patrones observados, un equipo de People Analytics podría considerar:

1. **Monitorear las horas extra y la carga de trabajo**, especialmente en equipos donde exista una concentración elevada de horas extra.

2. **Analizar los roles con mayores tasas de rotación observada** para investigar posibles diferencias en carga de trabajo, satisfacción, desarrollo profesional y condiciones laborales.

3. **Prestar atención a empleados durante las primeras etapas de permanencia**, utilizando indicadores como satisfacción, antigüedad, desarrollo profesional y experiencia con el manager.

4. **Combinar información de satisfacción con otros indicadores laborales** para comprender mejor la experiencia del empleado.

5. **Utilizar modelos predictivos como herramientas de apoyo**, evitando utilizarlos de manera automática para tomar decisiones individuales sobre empleados.

---

## Limitaciones

Este proyecto presenta algunas limitaciones importantes:

* El dataset es un conjunto de datos de práctica y no representa una organización real.
* Los resultados muestran asociaciones y no causalidad.
* La variable objetivo presenta un desequilibrio entre las clases.
* El modelo tiene un recall limitado para la clase `Attrition = Y
