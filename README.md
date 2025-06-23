# Clasificación de la Capacidad Financiera con Datos de la ENIF 2024

Este proyecto implementa una metodología para clasificar la **capacidad financiera** de las personas utilizando datos de la Encuesta Nacional de Inclusión Financiera (ENIF) 2024 del INEGI. Dado que no existe una variable directa que mida esta capacidad, se propone una estrategia basada en técnicas de reducción de dimensión y codificación de variables categóricas para construir un índice sintético.

## Objetivo

Construir un índice multidimensional que permita clasificar a los individuos según su **capacidad financiera**, entendida como:

> La habilidad de una persona u organización para administrar eficientemente sus ingresos y gastos, cumplir con sus obligaciones económicas, tomar decisiones informadas de inversión y prepararse ante eventualidades financieras.

---

## Metodología

1. **Exploración y unión de datos**: Se combinan los datos de personas y viviendas mediante un `LEFT JOIN`.
2. **Filtrado de variables**:
   - Filtro por palabras clave relacionadas con la definición de capacidad financiera.
   - Eliminación de variables con más de 20% de datos faltantes.
   - Eliminación manual de variables conceptualmente irrelevantes.
3. **Limpieza de datos**:
   - Se elimina una sola fila con demasiados faltantes.
   - El conjunto final no requiere imputación.
4. **Preparación para modelado**:
   - Se codifican las 85 variables nominales usando One-Hot Encoding.
   - Se escalan todas las variables con `StandardScaler`.
5. **Reducción de dimensionalidad**:
   - Se aplica Análisis de Componentes Principales (PCA).
   - Se retienen 40 componentes que explican el 68% de la varianza.
6. **Construcción del índice**:
   - Se genera un **índice financiero continuo**.
   - Se discretiza en **tres niveles de capacidad financiera**.
7. **Exportación**:
   - Se guarda un archivo con `llavemod`, `índice financiero` y `grado financiero` (1, 2 o 3).

---

## Estructura del Proyecto

```
├── capacidad_financiera_ENIF_2024.ipynb   # Notebook principal con el análisis completo
├── presentación.pdf                       # Presentación del proyecto (resumen metodológico)
├── README.md                              # Este archivo
```

---

## Resultados

Se construyó un índice continuo que permite ordenar a las personas según su capacidad financiera. Este índice se discretizó en tres categorías para su uso práctico:

| Llavemod | Índice Financiero | Grado Financiero |
|----------|-------------------|------------------|
| 101101   | -0.662753         | 1                |
| 503101   | 0.246904          | 3                |
| 803102   | -0.151144         | 2                |
| ...      | ...               | ...              |

> El índice no implica directamente "mejor comportamiento financiero" con valores altos, ya que se construyó a partir de variables dummy. Se recomienda interpretar sus componentes con cautela.

---

## Recomendaciones y futuras mejoras

- Analizar los **componentes principales** para una mejor interpretación del índice.
- Explorar modelos de **Análisis Factorial** como alternativa.
- Aplicar técnicas de **clustering** y comparar resultados.
- Refinar la **selección semántica de variables**.
- Experimentar con enfoques **supervisados y no supervisados** adicionales.

---

## Requisitos Técnicos

- Python 3.9+
- Pandas, NumPy
- Scikit-learn
- Matplotlib / Seaborn



