# PRUEBA-DE-HIPOTESIS-FUTBOL-FEMENINO-VS-FUTBOL-MASCULINO
Análisis estadístico y prueba de hipótesis no paramétrica (Mann-Whitney U) en Python para comparar la media de goles en mundiales de fútbol femenino y masculino. Proyecto capstone de certificación Data Analyst in Python (DataCamp).
# ⚽ FIFA World Cup: ¿Se marcan más goles en el fútbol femenino? 📊

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![DataCamp](https://img.shields.io/badge/DataCamp_Certified-05192D?style=for-the-badge&logo=datacamp&logoColor=05D6A0)

Este proyecto corresponde al caso práctico final (*capstone project*) para la obtención de la certificación oficial **Data Analyst in Python** de DataCamp.

---

## 📌 Contexto del Problema

Como periodista analista deportivo, surge la hipótesis intuitiva de que los partidos internacionales de fútbol femenino registran una mayor dinámica de goles que los masculinos. El objetivo es validar estadísticamente esta afirmación utilizando registros históricos de partidos oficiales de la **Copa Mundial de la FIFA** desde **2002-01-01**.

---

## 📐 Definición del Experimento Estadístico

Se establece un **nivel de significancia ($\alpha$) del 10% (0.10)** para evaluar las siguientes hipótesis:

* **$H_0$ (Hipótesis Nula):** El número medio de goles en partidos mundiales femeninos es igual al de masculinos.
* **$H_A$ (Hipótesis Alternativa):** El número medio de goles en partidos mundiales femeninos es estrictamente **mayor** que en los masculinos.

---

## 🛠️ Metodología y Pipeline en Python

1. **Infiltración y Filtrado de Datos (`pandas`):**
   * Lectura de conjuntos de datos históricos (`women_results.csv` y `men_results.csv`).
   * Filtrado exclusivo por torneo (`'FIFA World Cup'`) y fecha ($\ge$ `2002-01-01`).
   * *Feature Engineering:* Creación de la métrica `total_goals = home_score + away_score`.

2. **Evaluación de Normalidad (`seaborn` / `matplotlib`):**
   * Visualización de histogramas de distribución de frecuencia de goles por grupo.
   * **Hallazgo:** La distribución de goles presenta un claro sesgo a la derecha y no sigue una distribución normal.
   * **Decisión metodológica:** Se descarta la prueba paramétrica ($t$-test) en favor de una prueba **no paramétrica**: **Wilcoxon-Mann-Whitney** (Mann-Whitney U Test).

3. **Ejecución del Test Estadístico (`pingouin`):**
   * Transformación de datos mediante pivotaje.
   * Aplicación de `pg.mwu()` evaluando la cola derecha (`alternative='greater'`).

---

## 🎯 Resultados y Veredicto

| Métrica Estadística | Valor Obtenido | Umbral de Decisión |
| :--- | :--- | :--- |
| **$p$-value** | **`0.0051`** | $\alpha = 0.10$ |
| **Decisión** | **Rechazar $H_0$** | $p\text{-value} < \alpha$ |

**Conclusión:**
Dado que el $p$-value ($0.0051$) es sustancialmente menor que el nivel de significancia del $10\%$, existe **evidencia estadística suficiente** para afirmar que se marcan significativamente más goles por partido en la Copa Mundial Femenina que en la Masculina desde 2002.

---

## 📁 Estructura del Repositorio

```text
├── data/
│   ├── men_results.csv
│   └── women_results.csv
├── notebook.ipynb          # Jupyter Notebook con el análisis completo
├── requirements.txt        # Librerías necesarias para replicar
└── README.md               # Documentación del proyecto
