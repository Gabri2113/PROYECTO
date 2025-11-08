# Descripción general

Bienvenido a mi análisis del mercado laboral de datos, centrado en los roles de analista de datos. Este proyecto fue creado con el objetivo de comprender y navegar el mercado laboral de manera más efectiva. Profundiza en las habilidades mejor pagadas y más demandadas para ayudar a encontrar oportunidades laborales óptimas para los analistas de datos.

Los datos provienen del curso de Python de Luke Barousse, que proporciona la base para mi análisis e incluye información detallada sobre títulos de trabajo, salarios, ubicaciones y habilidades esenciales. A través de una serie de scripts en Python, exploro preguntas clave como las habilidades más demandadas, las tendencias salariales y la intersección entre la demanda y el salario en el análisis de datos.


# Las preguntas

A continuación se presentan las preguntas que quiero responder en mi proyecto:

    1.¿Cuáles son las habilidades más demandadas en los 3 roles de datos más populares?
    2.¿Cómo están evolucionando las habilidades más demandadas para los analistas de datos?
    3.¿Qué tan bien pagan los trabajos y las habilidades en análisis de datos?
    4.¿Cuáles son las habilidades óptimas para que los analistas de datos aprendan? (Alta demanda y alta remuneración)


Para profundizar en el mercado laboral de analistas de datos, aproveché el poder de varias herramientas clave:

    Python: La columna vertebral de mi análisis, que me permitió analizar los datos y encontrar información crítica.

        Librería Pandas: La librería de Python que utilicé para analizar los datos.

        Librería Matplotlib: La librería que utilicé para visualizar mis datos.

        Librería Seaborn: La librería que utilicé para crear visualizaciones más avanzadas.

    Jupyter Notebooks: La herramienta que usé para ejecutar mis scripts de Python, lo que me permitió incluir fácilmente mis notas y análisis.

    Visual Studio Code: Mi herramienta principal para ejecutar mis scripts de Python.

    Git y GitHub: Esenciales para el control de versiones y para compartir mi código y análisis en Python, asegurando la colaboración y la organización del proyecto.



# Preparación y limpieza de datos

Esta sección describe los pasos realizados para preparar los datos para el análisis, garantizando su precisión y usabilidad.

Importar y limpiar los datos

Comienzo importando las librerías necesarias y cargando el conjunto de datos, seguido de tareas iniciales de limpieza de datos para asegurar la calidad de la información.

```python

import pandas as pd
import matplotlib.pyplot as plt
import copy
import tabulate
import openpyxl
import ast
import seaborn as sns

df = pd.read_csv(r"C:\Users\gabri\Documents\PYTHON\Archivos youtube\data_jobs.csv")
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x : ast.literal_eval(x) if pd.notna(x) else x)

```


# Filtrar trabajos en EE.UU.

Para enfocar mi análisis en el mercado laboral estadounidense, aplico filtros al conjunto de datos, reduciendo a los roles ubicados en Estados Unidos.

```python

df_USA = df.query('job_country == "United States"')

```


# Analisis 

Cada cuaderno de Jupyter en este proyecto está orientado a investigar aspectos específicos del mercado laboral de datos. Así es como abordé cada pregunta:

## 1.¿Cuáles son las habilidades más demandadas para los 3 roles de datos más populares?

Para encontrar las habilidades más demandadas en los 3 roles de datos más populares, filtré las posiciones según cuáles eran las más comunes y obtuve las 5 habilidades principales para esos 3 roles.
Esta consulta resalta los títulos de trabajo más populares y sus principales habilidades, mostrando en cuáles debería enfocarme según el rol al que estoy apuntando.

Puedes ver mi cuaderno con los pasos detallados aquí:
[Proyecto.ipynb](Proyecto.ipynb)


## Visualizar los datos


```python
fig , ax = plt.subplots(len(job_titles), 1)
plt.figure(figsize=(10,10))
sns.set_theme(style='ticks')

for i, job in enumerate(job_titles):
    df_plot1 = job_perc[job_perc['job_title_short'] == job].head(5).round(2)
    # df_plot.plot(kind='barh',x='job_skills', y='job_skill_oerce', ax=ax[i], title=job)
    sns.barplot(df_plot1,x='job_skill_perce', y='job_skills', hue='skill_count', ax=ax[i], palette='dark:b_r')
    fig.tight_layout()
    ax[i].set_title(job)
    # ax[i].tick_params(axis='y',rotation=5)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    # ax[i].xt
    ax[i].legend().set_visible(False)
    ax[i].set_xlim(0,80)

    for n, v in enumerate(df_plot1['job_skill_perce']):
        ax[i].text(v+1,n,f'{v:.0f}%', va='center')
    if i != len(job_titles) - 1 :
        ax[i].set_xticks([])
fig.suptitle('Porcentaje de solicitud de lenguajes y herramientas clave según el rol de datos.',fontsize=15)  
fig.tight_layout(h_pad=0.5)
plt.show()  
```


## Resultado
 
![Visual de herramientas](Imagen\output.png)



## Hallazgos Clave

- Python es una habilidad versátil, muy demandada en los tres roles, pero más prominentemente para Científicos de Datos (72%) e Ingenieros de Datos (65%).
- SQL es la habilidad más solicitada para Analistas de Datos y Científicos de Datos, apareciendo en más de la mitad de las publicaciones de trabajo para ambos roles. Para Ingenieros de Datos, Python es la habilidad más buscada, apareciendo en el 68% de las publicaciones de trabajo.
- Los Ingenieros de Datos requieren habilidades técnicas más especializadas (AWS, Azure, Spark) en comparación con Analistas de Datos y Científicos de Datos, de quienes se espera dominio en herramientas más generales de gestión y análisis de datos (Excel, Tableau).

