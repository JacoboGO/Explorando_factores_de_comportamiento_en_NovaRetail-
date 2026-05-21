# 🛒 NovaRetail+ · Análisis de Comportamiento de Clientes 2024

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?style=for-the-badge&logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-Stats-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0?style=for-the-badge)

**Análisis correlacional exploratorio · 15,000 registros · 12 variables · 4 métodos estadísticos**

</div>

---

## 📌 Contexto del negocio

**NovaRetail+** es una plataforma de comercio electrónico en Latinoamérica con millones de usuarios activos. Para el cierre de 2024, el equipo de **Crecimiento y Retención** planteó la siguiente pregunta estratégica:

> _¿Qué factores del comportamiento del cliente están más fuertemente asociados con el **ingreso anual** generado para la empresa?_

Este proyecto responde esa pregunta a través de un análisis **correlacional exploratorio** estructurado en 6 secciones, aplicando el método estadístico correcto según el tipo de cada variable.

> ⚠️ **Nota metodológica:** Correlación ≠ causalidad. Los hallazgos son asociativos, no causales.

---

## 📂 Estructura del repositorio

```
📦 Project-NovaRetail/
 ┣ 📓 Project-NovaRetail.ipynb          ← Notebook principal con análisis completo
 ┣ 📊 novaretail_comportamiento_clientes_2024.csv   ← Dataset fuente
 ┗ 📄 README.md
```

---

## 📊 Dataset

| Atributo | Detalle |
|---|---|
| Registros | 15,000 clientes |
| Variables | 12 columnas |
| Valores nulos | 0 |
| Período | 2024 |
| Fuente | Plataforma NovaRetail+ (simulado) |

### Variables del dataset

| Variable | Tipo | Descripción |
|---|---|---|
| `id_cliente` | Categórica | Identificador único del cliente |
| `edad` | Numérica | Edad del cliente (18–75 años) |
| `nivel_ingreso` | Numérica | Ingreso anual estimado del cliente |
| `visitas_mes` | Numérica | Visitas al sitio/app en el mes |
| `compras_mes` | Numérica | Compras realizadas en el mes |
| `gasto_publicidad_dirigida` | Numérica | Inversión en anuncios asignada al usuario |
| `satisfaccion` | Numérica | Calificación del cliente (escala 1–5) |
| `miembro_premium` | Binaria | Suscripción premium (1 = sí, 0 = no) |
| `abandono` | Binaria | Churn del cliente (1 = abandonó) |
| `tipo_dispositivo` | Categórica | Móvil / Escritorio / Tablet |
| `region` | Categórica | Norte / Sur / Este / Oeste |
| `ingreso_anual` ⭐ | Numérica | **Variable objetivo** — ingreso anual generado |

---

## 🔬 Metodología

El análisis se estructuró en **6 secciones** con una lógica progresiva:

```
Sección 1 → Carga y exploración inicial del dataset
Sección 2 → Limpieza, tipificación y documentación de supuestos
Sección 3 → Visualización de relaciones (Heatmap + Scatterplots)
Sección 4 → Coeficientes de correlación y evidencia numérica
Sección 5 → Interpretación de hallazgos para el negocio
Sección 6 → Limitaciones y próximos pasos
```

### Métodos estadísticos aplicados

| Método | Variables | Razón de uso |
|---|---|---|
| **Pearson** | Numérica ↔ Numérica | Evalúa relaciones lineales entre variables continuas |
| **Spearman** | Numérica ↔ Numérica | Evalúa relaciones monótonas; no asume normalidad |
| **Punto-biserial** | Numérica ↔ Binaria | Correlación entre variable continua y dicotómica |
| **V de Cramér** | Categórica ↔ Categórica | Asociación entre variables nominales vía χ² |

---

## 📈 Hallazgos principales

### Tabla 1 · Correlaciones numéricas (Pearson / Spearman)

| Variable 1 | Variable 2 | Pearson | Spearman | Colinealidad |
|---|---|---|---|---|
| `ingreso_anual` | `compras_mes` | **0.967** | **0.967** | 🔴 Fuerte |
| `gasto_publicidad_dirigida` | `visitas_mes` | 0.579 | 0.559 | 🟠 Moderada |
| `compras_mes` | `visitas_mes` | 0.354 | 0.333 | 🟠 Moderada |
| `ingreso_anual` | `visitas_mes` | 0.337 | 0.321 | 🟠 Moderada |
| `gasto_publicidad_dirigida` | `compras_mes` | 0.208 | 0.193 | 🟡 Ligera |
| `ingreso_anual` | `gasto_publicidad_dirigida` | 0.197 | 0.185 | 🟡 Ligera |

### Tabla 2 · Correlaciones biseriales (p-value ≤ 0.05)

| Binaria | Numérica | Coef. | p-valor |
|---|---|---|---|
| `miembro_premium` | `ingreso_anual` | +0.093 | 0.000 ✅ |
| `miembro_premium` | `satisfaccion` | +0.026 | 0.002 ✅ |
| `abandono` | `satisfaccion` | −0.024 | 0.004 ✅ |

### Tabla 3 · Satisfacción de usuarios activos

| Rango satisfacción | Premium (%) | Normal (%) |
|---|---|---|
| 0–1 | 0.00 | 0.01 |
| 1–2 | 0.13 | 1.12 |
| 2–3 | 2.50 | 16.52 |
| 3–4 | 7.51 | 44.51 |
| **4–5** | **3.79** | **22.76** |

> El **79% de los usuarios activos** tienen una satisfacción ≥ 3. Tasa de abandono: **1.15%** de la población total.

### Tabla 4 · Asociación categórica (V de Cramér)

| Variable 1 | Variable 2 | V de Cramér | Interpretación |
|---|---|---|---|
| `tipo_dispositivo` | `region` | 0.012 | 🟢 Asociación casi nula |

> El **55% de los usuarios** utiliza móvil en todas las regiones, sin dependencia geográfica significativa.

---

## 💡 Implicaciones de negocio

| # | Hallazgo | Implicación |
|---|---|---|
| 1 | `compras_mes` → `ingreso_anual` (r=0.967) | Incentivar la conversión de visitas a compras es la palanca más directa de ingresos |
| 2 | `gasto_publicidad_dirigida` → `visitas_mes` (r=0.579) | La inversión en publicidad dirigida sí atrae usuarios; optimizar el targeting amplifica el retorno |
| 3 | `compras_mes` → `visitas_mes` (r=0.354) | Aumentar la frecuencia de visitas eleva la probabilidad de compra |
| 4 | `miembro_premium` → `ingreso_anual` (p<0.001) | El segmento premium aporta ingresos superiores; programas de fidelización tienen potencial de escala |
| 5 | Móvil = 55% en todas las regiones | Priorizar la experiencia mobile-first en todas las regiones |

---

## 🛠️ Stack tecnológico

```python
# Core
pandas       # Manipulación y análisis de datos
numpy        # Operaciones numéricas

# Visualización
matplotlib   # Gráficos base
seaborn      # Heatmaps y scatterplots estadísticos

# Estadística
scipy.stats  # pointbiserialr, chi2_contingency
```

---

## ▶️ Cómo ejecutar el proyecto

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/project-novaretail.git
cd project-novaretail

# 2. Instalar dependencias
pip install pandas numpy matplotlib seaborn scipy jupyter

# 3. Abrir el notebook
jupyter notebook Project-NovaRetail.ipynb
```

> Asegúrate de que el archivo CSV esté en la misma carpeta que el notebook, o actualiza la ruta de `pd.read_csv()` en la Sección 1.

---

## 🗺️ Próximos pasos

- [ ] Segmentar análisis por `miembro_premium` vs usuario normal para evaluar la paradoja de Simpson
- [ ] Análisis de cohortes por región y dispositivo
- [ ] Modelo predictivo de churn con regresión logística o árbol de decisión
- [ ] Dashboard interactivo con Plotly o Power BI

---

## 👤 Autor

**[Jacobo Galindo Ortiz]**
Analista de Datos

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Conectar-0A66C2?style=flat&logo=linkedin)](https://linkedin.com/in/jacobo-galindo-ortiz)
[![GitHub](https://img.shields.io/badge/GitHub-Perfil-181717?style=flat&logo=github)](https://github.com/JacoboGO)
[![Email](https://img.shields.io/badge/Email-Contacto-EA4335?style=flat&logo=gmail)](mailto:jacobo.galindo.ortiz@hotmail.com)

---

"El lenguaje es una ventana al pensamiento"
Noam Chomsky

<div align="center">

⭐ Si este proyecto te resultó útil, considera dejar una estrella en el repositorio.

</div>
