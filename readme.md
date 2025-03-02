# Procesando datos con sklearn

## Descripción del Proyecto
Este proyecto realiza la preparación y transformación de datos utilizando `pandas` y `sklearn`. Se trabaja con un dataset que contiene información sobre individuos, incluyendo su género y profesión, y se aplican técnicas de preprocesamiento como mapeo de valores categóricos y codificación one-hot.

## Pasos Realizados

### 1. Carga de Datos
El dataset es cargado en un DataFrame de `pandas` para su manipulación.

### 2. Transformación de Género
Se convierte la columna `gender` de valores categóricos ('M', 'F') a valores numéricos usando un diccionario:
```python
gender_dict = {"M": 0, "F": 1}
df["gender"] = [gender_dict[g] for g in df["gender"]]
```
Esto facilita el uso del dato en modelos de Machine Learning.

### 3. Codificación One-Hot para la Variable `job`
Se aplica `OneHotEncoder` de `sklearn` para transformar la columna `job`, generando variables dummy para cada categoría:
```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder()
matrix = encoder.fit_transform(df[["job"]]).toarray()

column_names = encoder.get_feature_names_out(["job"])
df_encoded = pd.DataFrame(matrix, columns=column_names)
df = pd.concat([df, df_encoded], axis=1)
df.drop(columns=["job"], inplace=True)
```
Este paso permite que la variable categórica sea utilizada en modelos estadísticos y de Machine Learning sin sesgos arbitrarios.

## Requisitos
- Python 3.x
- Pandas
- Scikit-learn

## Ejecución
1. Instala las dependencias con `pip install pandas scikit-learn`.
2. Ejecuta el script en Jupyter Notebook o un entorno de Python compatible.

