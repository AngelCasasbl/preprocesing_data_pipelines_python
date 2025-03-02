# Procesando datos con sklearn

Este repositorio contiene un pipeline de preprocesamiento de datos utilizando `pandas` y `scikit-learn`. El objetivo principal es limpiar y transformar un conjunto de datos con información sobre individuos, incluyendo su edad, género y ocupación.

## Instalación

Antes de ejecutar el código, asegúrate de tener instaladas las siguientes bibliotecas:

```bash
pip install pandas scikit-learn
```

## Descripción del Pipeline

El proceso de preprocesamiento incluye los siguientes pasos:

1. **Eliminación de la columna `name`**: Se elimina esta columna ya que no es relevante para el análisis.
2. **Imputación de valores faltantes en `age`**: Se reemplazan los valores faltantes con la media de la columna `age`.
3. **Codificación numérica de `gender`**: Se transforma la variable categórica en valores numéricos (`M` → 0, `F` → 1).
4. **Codificación one-hot de `job`**: Se convierten las categorías de ocupación en variables binarias.

## Implementación

El código se organiza en dos enfoques:

1. **Preprocesamiento manual**:
    - Se utilizan `pandas` y `scikit-learn` para transformar los datos paso a paso.

2. **Implementación con Clases Personalizadas**:
    - Se crean clases personalizadas (`BaseEstimator`, `TransformerMixin`) para modularizar cada paso del preprocesamiento:
      - `NameDropper`: Elimina la columna `name`.
      - `AgeImputer`: Imputa los valores faltantes en `age` con la media.
      - `FeatureEncoder`: Aplica one-hot encoding a la columna `job`.

## Uso

```python
import pandas as pd
from sklearn.pipeline import Pipeline

# Datos de ejemplo
data = {
    'name': ['John', 'Anna', 'Peter', 'Linda'],
    'age': [23, 36, None, 26],
    'gender': ['M', 'F', 'M', 'F'],
    'job': ['student', 'teacher', 'developer', 'nurse']
}

df = pd.DataFrame(data)

# Aplicar transformaciones
pipeline = Pipeline([
    ('dropper', NameDropper()),
    ('imputer', AgeImputer()),
    ('encoder', FeatureEncoder())
])

df_transformed = pipeline.fit_transform(df)
print(df_transformed)
```

## Contribución

Si deseas contribuir, abre un issue o envía un pull request con mejoras o nuevas funcionalidades.


