# Informe Final: Análisis de Evasión de Clientes en TelecomX LATAM

## 🔹 Introducción

El presente informe detalla el análisis exploratorio y de limpieza de datos realizado sobre el dataset de clientes de TelecomX LATAM. El objetivo principal de este proyecto es comprender los factores que influyen en la **evasión de clientes (Churn)**, identificando patrones y características comunes entre los clientes que deciden cancelar su servicio. La evasión de clientes representa un desafío significativo para las empresas de telecomunicaciones, ya que retener a los clientes existentes suele ser más rentable que adquirir nuevos. Un análisis profundo de los datos puede proporcionar insights valiosos para desarrollar estrategias de retención efectivas.

## 🔹 Limpieza y Tratamiento de Datos

El proceso de limpieza y tratamiento de datos fue una etapa fundamental para preparar el dataset para el análisis. Los pasos realizados incluyeron:

1.  **Importación de Datos**: Se importó el dataset `TelecomX_Data.json` utilizando la librería pandas.
2.  **Normalización de Columnas Anidadas**: Se identificaron columnas con estructuras anidadas (`customer`, `phone`, `internet`, `account`). Estas columnas fueron normalizadas utilizando `pd.json_normalize` para expandir sus contenidos en nuevas columnas dentro del DataFrame principal.
3.  **Eliminación de Columnas Originales Anidadas**: Una vez normalizadas, las columnas anidadas originales fueron eliminadas del DataFrame para evitar redundancia y simplificar la estructura.
4.  **Renombrado de Columnas**: Se renombraron las columnas a nombres más descriptivos y en español para facilitar la comprensión y el análisis.
5.  **Verificación de Tipos de Datos y Valores Nulos/Duplicados**: Se realizó una inspección inicial con `.info()`, `.duplicated().sum()`, y `.isnull().sum()` para entender la estructura, identificar duplicados y valores nulos. No se encontraron filas duplicadas, pero sí valores nulos en la columna `Cargos_totales`.
6.  **Limpieza y Conversión de 'Cargos_totales'**: La columna `Cargos_totales` contenía caracteres no numéricos ('$', ',' y espacios) y estaba como tipo 'object'. Se limpiaron estos caracteres y se convirtió la columna a tipo numérico (`float`). Se identificaron 11 filas con valores nulos en esta columna, las cuales fueron eliminadas del dataset ya que representaban un porcentaje muy pequeño del total y no era posible imputar un valor confiable.
7.  **Limpieza de Columnas Categóricas**: Se estandarizó el formato de texto en columnas categóricas como `Tipo_contrato` y `Metodo_pago`, convirtiéndolos a minúsculas y eliminando caracteres especiales o espacios innecesarios.
8.  **Conversión de 'Cancelacion' a Numérico**: La columna objetivo `Cancelacion` (Churn) fue convertida a un formato numérico (1 para 'Yes', 0 para 'No') para facilitar futuros análisis cuantitativos y modelado.
9.  **Creación de Nueva Característica**: Se creó una nueva columna, `Cuentas_diarias`, calculando el cargo diario promedio a partir de `Cargos_mensuales`.

## 🔹 Análisis Exploratorio de Datos

Se llevaron a cabo diversos análisis exploratorios para visualizar la distribución de la evasión y su relación con otras variables:

*   **Distribución de Evasión**: Un gráfico de pastel mostró la proporción general de clientes que cancelaron (aproximadamente 25.5%) frente a los que no (aproximadamente 74.5%). Esto indica un desbalance en la clase objetivo, algo a considerar en futuras etapas de modelado.
   