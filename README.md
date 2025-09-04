# Tarea 3 — Winequality (Red)

Este repositorio contiene el análisis del dataset **winequality-red.csv** para cumplir los puntos del enunciado:

- Importar y cargar el CSV  
- Limpieza / preparación básica  
- Resumen estadístico  
- Matriz de correlación  
- ≥ 3 gráficas  
- ≥ 3 conclusiones

---

## 1) Requisitos

- **Python** 3.10+ (probado en 3.12)
- Paquetes: `pandas`, `numpy`, `matplotlib`, `notebook` (para Jupyter)

Instalación rápida (Windows, en la carpeta del proyecto):

```powershell
py -m venv .venv
.\.venv\Scriptsctivate
pip install pandas numpy matplotlib notebook
jupyter notebook
```

> Si usas `pipenv`, ajusta tu `Pipfile` a `python_version = "3.12"` y crea el entorno con  
> `pipenv --python <ruta-a-python>` y `pipenv install`.

---

## 2) Estructura

```
Tarea3/
├─ analyze.ipynb          # Notebook con el paso a paso
├─ winequality-red.csv    # Dataset (separador ';')
└─ output/                # Se crea al correr; guarda PNG y conclusiones.txt
```

---

## 3) Cómo ejecutar

1. Abre Jupyter en la carpeta del proyecto:
   ```powershell
   jupyter notebook
   ```
2. Abre **`analyze.ipynb`** y ejecuta las celdas en orden (o `Kernel → Restart & Run All`).

El notebook:
- Lee el CSV con `sep=';'` (si hiciera falta, prueba `,` automáticamente).
- Normaliza nombres de columnas, elimina duplicados y tipifica `quality` a entero.
- Calcula `describe()`, la **matriz de correlación (Pearson)** y genera ≥3 **gráficas**.
- Guarda **todas** las figuras en `output/` y redacta `output/conclusiones.txt`.

---

## 4) Proceso

### 4.1 Importación y vista rápida
- `pd.read_csv('winequality-red.csv', sep=';')`
- `df.head()` y `df.info()` para confirmar estructura (**1599 filas × 12 columnas**).

### 4.2 Limpieza / preparación
- Nombres a *snake_case*.
- **Duplicados removidos:** **240**  
- **NA totales (previos a limpiar):** **0**  
- **Filas finales:** **1359**  
- `quality` a `int`.

### 4.3 Resumen estadístico
- `df.describe().T` → `count, mean, std, min, 25%, 50%, 75%, max`.

### 4.4 Matriz de correlación
- `df.select_dtypes(...).corr()` (Pearson).
- Visualización tipo **heatmap** con valores anotados.
- **Salida:** `output/paso04_matriz_correlacion.png`.

**Cómo leerla:**  
Rojo (positivo) ↗, Azul (negativo) ↘, 0 ≈ sin relación lineal. Diagonal = 1.

### 4.5 Gráficas (≥3) generadas
1. **Histograma de `quality`** → `output/paso05_1_hist_quality.png`  
2. **Dispersión `alcohol` vs `quality`** → `output/paso05_2_scatter_alcohol_quality.png`  
3. **Boxplot `volatile_acidity` por `quality`** → `output/paso05_3_box_volatile_acidity.png`  
4. *(Extra)* **Boxplot `sulphates` por `quality`** → `output/paso05_4_box_sulphates.png`

> Nota (Matplotlib ≥ 3.9): en `boxplot`, usa `tick_labels=` en lugar de `labels=`.

---

## 5) Conclusiones principales

- **Alcohol calidad (positiva moderada):** la relación es clara (**r ≈ 0.48**).
- **Acidez volátil calidad (negativa):** valores altos penalizan la calidad (**r ≈ −0.39**).
- **Distribución de `quality`:** centrada en valores medios; mediana **≈ 6** (rango **3–8**).
- **Sulphates calidad (positiva leve–moderada):** asociación positiva discreta (**r ≈ 0.25**).

> Recordatorio: **correlación ≠ causalidad**. Estas cifras pueden variar si se aplican filtros diferentes.

---

## 6) Cómo armar el PDF único (entrega)

Orden sugerido:

1. **Portada** (curso, “Tarea 3”, nombre/carné, fecha).  
2. **Metodología**: “Se usó Python (pandas, numpy, matplotlib) en Jupyter; se realizó limpieza, resumen estadístico, matriz de correlación y ≥3 gráficas.”  
3. **Limpieza** (resumen de cifras).  
4. **Resumen estadístico** (tabla/captura de `describe`).  
5. **Matriz de correlación** + breve interpretación.  
6. **Gráficas**: histograma, scatter `alcohol vs quality`, boxplot `volatile_acidity` (y *extra* `sulphates`).  
7. **Conclusiones** (copiar desde `conclusiones.txt`).

**Cómo producirlo:**
- Inserta los PNG en Word/Google Docs → **Exportar a PDF**, **o**
- En Jupyter, `File → Download as HTML`, abrir el `.html` y **Imprimir → Guardar como PDF**.

---

## 7) Solución de problemas

- **Solo 1 columna al leer el CSV:** usa `sep=';'` (dataset UCI); si sigue, intenta `sep=','`.  
- **`NameError: df no definido`:** vuelve a ejecutar la celda que crea `df`.  
- **Warning en `boxplot`:** reemplaza `labels=` por `tick_labels=`.  
- **“Not Trusted” en Jupyter:** `File → Trust Notebook`.

---

## 8) Créditos

- Dataset: *Wine Quality – Red*, UCI Machine Learning Repository.  
- Librerías: **pandas**, **numpy**, **matplotlib**, **Jupyter**.
