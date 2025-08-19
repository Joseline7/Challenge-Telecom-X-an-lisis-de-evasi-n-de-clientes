## 📉 Diagnóstico de Cancelación de Clientes – Telecom X

### 🧩 Contexto del problema  
Telecom X, empresa del rubro de telecomunicaciones, atraviesa una situación crítica: una alta tasa de cancelación de clientes. Hasta el momento, no se han identificado las causas principales de esta pérdida. En este proyecto, asumes el rol de analista de datos para investigar el fenómeno y aportar soluciones basadas en evidencia.

---

### 📦 Obtención de datos  
Los datos fueron extraídos desde el archivo `TelecomX_Data.json`. Este conjunto incluye información detallada de cada cliente:  
👤 Datos demográficos  
📞 Servicios contratados  
💼 Información de cuenta  
🚪 Estado de cancelación (churn)

---

### 🧪 Preparación del entorno  
Se importaron las librerías necesarias para el análisis y visualización:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Estilo visual para los gráficos
sns.set_style("whitegrid")
```

---

### 📥 Carga de datos  
El archivo JSON se carga en un DataFrame de pandas. Se incluye manejo de errores para asegurar que el archivo esté disponible en el entorno de trabajo:

```python
try:
    df = pd.read_json("/content/drive/MyDrive/Data_Science/Pandas/TelecomX_Data.json")
    print("✅ Datos cargados correctamente.")
    print("📐 Dimensiones del DataFrame:", df.shape)

    print("\n🔍 Primeras 5 filas:")
    display(df.head())

    print("\n📋 Información general del DataFrame:")
    df.info()

except FileNotFoundError:
    print("⚠️ Error: No se encontró el archivo 'TelecomX_Data.json'.")
    print("📎 Por favor, súbelo al entorno de Colab.")
except Exception as e:
    print(f"❌ Se produjo un error: {e}")
```

---

### 📊 Resultado inicial  
Los datos se cargaron con éxito.  
**Tamaño del DataFrame:** 7267 filas × 6 columnas


Primeras 5 filas del DataFrame:

<img width="1145" height="326" alt="image" src="https://github.com/user-attachments/assets/c36d8071-5b01-4de1-b9f4-197ed382b316" />

Información del DataFrame:
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 7267 entries, 0 to 7266
Data columns (total 6 columns):

<img width="374" height="161" alt="image" src="https://github.com/user-attachments/assets/4600afe7-0a78-4f72-82d3-8d5191b190d3" />


## 🔧 Transformación de Datos  
### 3. Limpieza y Preprocesamiento 🧼

---

### 🧱 1. Desanidar la estructura JSON  
Los datos originales contienen columnas con información anidada (diccionarios) que dificultan el análisis directo. Para facilitar el acceso y manipulación, se descompusieron en DataFrames separados:

📊 `customer` → Datos demográficos  
📑 `account` → Información contractual  
📞 `phone` → Servicios telefónicos  
🌐 `internet` → Servicios de internet

```python
df_customer = pd.json_normalize(df['customer'])
df_account = pd.json_normalize(df['account'])
df_phone_services = pd.json_normalize(df['phone'])
df_internet_services = pd.json_normalize(df['internet'])

df_clean = pd.concat([df[['customerID', 'Churn']], df_customer, df_account, df_phone_services, df_internet_services], axis=1)
```

🔗 *Resultado:* Un DataFrame consolidado y plano, listo para análisis exploratorio.

---

### 🚫 2. Limpieza de valores faltantes en `Churn`  

### 💸 3. Conversión de `Charges.Total` a formato numérico  

### 👵 4. Recodificación de `SeniorCitizen`  

✅ **Estado final:**  

## 🧼 Resultados de la Limpieza y Transformación


