### **DESCRIPCION**
Analisis completo a travez del Ente Nacional de Comunicaciones (ENACOM) de Argentina (organismo regulador de las telecomunicaciones en Argentina). Con el fin de buscar oportunidades de mejora, KPI'S entre otros.

<div id="header" align="center">
  <img src="images/Logo_enacom.png" width="150"/>
</div>

### **TABLA DE CONTENIDO**
## Tabla de contenido
1. [Introducción](#introducción)
2. [Instalación y Requisitos](#instalación-y-requisitos)
3. [Estructura del Proyecto](#estructura-del-proyecto)
4. [Uso y Ejecución](#uso-y-ejecución)
5. [Datos y Fuentes](#datos-y-fuentes)
6. [Metodología](#metodología)
7. [Resultados y Conclusiones](#resultados-y-conclusiones)
8. [Contribución y Colaboración](#contribución-y-colaboración)
9. [Autores](#autores)

### **Introducción**


El internet ha venido revolucionado las telecomunicaciones, transformando la comunicación de limitada y lenta a instantánea y global. Ha permitido el intercambio de información en tiempo real, el acceso a recursos en línea y la creación de nuevas industrias. 

Ahora no es nada extraño encontrar cada año noticias con titulares como:

 "*El Gobierno argentino confirmó nuevos aumentos a partir de 2023 para los servicios de televisión paga, telefonía e internet. A través del Ente Nacional de Comunicaciones (Enacom), estableció...*

A partir de lo anterior puede surgir una pregunta bien interesante.
¿Que es el ENACOM y como influye en el aumento y disminucion de la tasa de cobro por servicios? 

En este proyecto vamos a resolver esta pregunta y llevarla mas allá, plantenado opciones de mejora a partir de dasboards interactivos, opotunidades de crecimiento y KPI's.

### **Instalación y requisitos**

- Python 3.7 o superior
- Todas las librerias usadas las encuentras en el archivo "requirements.txt"
- Power BI (ultimas versiones de preferencia)

### **Estructura del proyecto**
Una vez entendido las necesidades de nuestro cliente procedemos a diseñar la estructura del proyecto sobre la que se sontendrá todo el desarrollo y exito del mismo.

<div id="header" align="center">
  <img src="images/estructura_proyecto2.gif" width="750"/>
</div>

### **Uso y Ejecución**
- Abrir archivo de power bi ubicado en este repo.
- Selecciona con el boton izquierdo del raton el filtro que quieres aplicar para obtener los kpi o la información.
- Con `Ctrl + doble click` puedes usar la herramienta de navegacion del dashboard.

### **Datos y fuentes**
- [Diccionario de datos](https://docs.google.com/document/d/1BYW0vT_DNIjjKM9v4hNg5KmqjRNOc7OBB1jCXc80gnI/edit#heading=h.hjukififf3ol)
- [Atribucion uso de iconos Freepic](https://www.flaticon.es/iconos-gratis/pregunta)
  
### **Metodología**
Antes de comenzar con la primera etapa del proyecto y descargar todos los datos para el proyecto procederemos a realizar una pequeña pero importante etapa previa a la ingesta de datos.

**Consolidacion de Datos**
>En esta etapa filtraremos cual data será relevante para nuestro EDA y cual no, usaremos un cojunto de dataset para el conjunto de datos principales relacionados al internet y uno complementario que nos peuda servir de utilidad para brindarnos informacioón util. Para ello haremos uso del diccionario de datos.

- Solo 2 hojas de las 15 contienen datos NO relacionados al trimestre. Esta columna tiene incidencia directa en un 86% aproximadamente.
- La columna 'Link Indec' es un identificador relacionado con las localidades, se revisará la cantidad de duplicados.
- Un mapa de datos segun la provincia nos puede entregar valores utiles. Para ello tendremos en cuenta el mapa argentino.

<div id="header" align="center">
  <img src="images/argentina.png" width="450"/>
</div>

- Con la columna link indec relacionaremos el numero de velocidades mas bajas con la tecnologia, asi como la tecnologia que esta produciendo mejores resultados de velocidad.
- Asi mismo identificaremos la provincia con mayores usuarios de internet bajo.



 1. eliminada
 2. eliminada
 3. mapa Mbps x provincia x tiempo 
 4. eliminada
 5. eliminada
 6. eliminada 
 7. elimnada
 8. eliminada 
 9. eliminada
 10. mapa poblacion x provincia x tiempo (penetracion)
 11. mapa hogares x provincia x tiempo (penetracion)
 12. diagrama de barras doble (hogares-poblacion)
 13. eliminada
 14. Grafica interesante (hacer al final) totales y luego velocidades
 15. Grafica de barras ingresos 

- **Conjunto Principal: (CP)**
  1. Velocidad % por prov
  2. Penetración-poblacion
  3. Penetracion-hogares
  4. Penetracion totales
  5. Accesos por velocidad
  6. Ingresos

- **Conjunto Complementario: (CC)**
  - portabilidad
    1. Portin
  - servicios postales

    2. unidades_telegraficas
    3. unidades_monetarios
  - telefonia fija

    4. Fija_ingresos

1. **Ingesta de datos**

Tanto en el EDA como en ETL haremos una ingesta de todos las hojas de excel y las dividiremos por df correspondientes.

Primero guardamos todos los archivos de excel en variables para poderlas manipular.

```
internet = basepath + 'data/Internet.xlsx'
portabilidad = basepath + 'data/Portabilidad.xlsx'
servicios_postales = basepath + 'data/servicios_postales.xlsx'
telefonia_fija = basepath + 'data/Telefonia_fija.xlsx'
mapa_conectividad = basepath + 'data/mapa_conectividad.xlsx'
```

Nuestra variable 'basepath' está definida por la ruta de nuestro directorio que nos lleva hasta la carpeta que contiene los archivos. ejemplo:

```
C:/User/Personal/Desktop/
```

Creamos los dataframes. 
- 6 para el archivo Internet.
- 4 para archivos complementarios.

Total 12 dataframes.

```
df_CP2 = pd.read_excel(internet ,sheet_name= 'Velocidad % por prov')
df_CP4 = pd.read_excel(internet ,sheet_name= 'Penetración-poblacion')
df_CP5 = pd.read_excel(internet ,sheet_name= 'Penetracion-hogares')
df_CP6 = pd.read_excel(internet ,sheet_name= 'Penetracion-totales')
df_CP7 = pd.read_excel(internet ,sheet_name= 'Accesos por velocidad')
df_CP8 = pd.read_excel(internet ,sheet_name= 'Ingresos')

df_CC1 = pd.read_excel(mapa_conectividad ,sheet_name= 'Hoja3')
df_CC2 = pd.read_excel(portabilidad ,sheet_name= 'Portin')
df_CC3 = pd.read_excel(servicios_postales ,sheet_name= 'unidades_telegraficas')
df_CC4 = pd.read_excel(servicios_postales ,sheet_name= 'unidades_monetarios')
df_CC5 = pd.read_excel(telefonia_fija ,sheet_name= 'Fija_ingresos')

```

2. **ETL Database**

### Dataframe maps
Los primeros dataframes se concatenan para buscar una tabla que contenga los datos suficientes para realizar un mapa por provincia a travez del tiempo con:

- Mbps (Media de bajada)
- Accesos por cada 100 hab
- Accesos por cada 100  hogares

Pero aun nos falta asignar una latitud promedio de cada provincia. Por lo que vamos a generar un csv que contenga la Latitud y la Longitud de cada provincia promedio.

Para unir estos dataframes usaremos un leftjoin, donde la mayoria de los datos quedaran en el dataframe maps.
Sin embargo deberemos hacer un pequeño ETL en nuestro dataframe de mapas, pondremos todas las provincias en mayuscula y quitaremos las tildes, de esta manera solo nos quedaran algunas latitudes nulas cuyo valor limpiaremos en el EDA

3. **EDA Database + Analisis**
_Seguir la documentacion en el notebook EDA._
5. **Dasboard KPI + Analisis**
Para la realización del dashboard tuvimos que crear nuevas columnas planteando los 3 KPI de la siguiente manera:

```
# KPI solicitado
df_kpis['Accesos_siguiente_trimestre'] = df_kpis.groupby('Provincia')['Accesos por cada 100 hogares'].shift(-1)
df_kpis['KPI_propuesto'] = ((df_kpis['Accesos por cada 100 hogares'] - df_kpis['Accesos_siguiente_trimestre']) / df_kpis['Accesos por cada 100 hogares']) * 100

# KPI 1: Tasa de crecimiento anual en el acceso a Internet
df_kpis['Mbps_ano_anterior'] = df_kpis.groupby('Provincia')['Mbps (Media de bajada)'].shift(4)
df_kpis['KPI_crecimiento_anual'] = ((df_kpis['Mbps (Media de bajada)'] - df_kpis['Mbps_ano_anterior']) / df_kpis['Mbps_ano_anterior']) * 100

# KPI 2: Variación trimestral media en el acceso a Internet
df_kpis['Variacion_trimestral'] = df_kpis.groupby('Provincia')['Accesos por cada 100 hab'].diff()
df_kpis['KPI_variacion_trimestral_media'] = df_kpis.groupby(['Provincia', 'Año'])['Variacion_trimestral'].transform('mean')
```

Luego realizamos la preparación de los KPI's basandonos en el siguiente material de estudio:
[Como realizar un KPI en power bi](https://www.youtube.com/watch?v=xEjZDT0N1JQ&t=633s)

Para la realización deldashbard elejimos 3 aspectos a trabajar:
-  Mapa de burbujas que identificara las provincias destacadas en velocidades de internet segun el filtro.
-  Diagrama de barras cruzado que identificara la relación entre hogares y habitantes.
-  Tarjetas para una sencilla visualización del valor exacto de habitantes y hogares.
7. **Preparación DEMO**
Para la preparación de la demos tomamos un cuadernos, generamos una lluvia de ideas de la información relevante que debemos tocar y comenzamos a organizar un flujo de las mismas a modo de storytelling para poder conducir al usuario a una experiencia grata e ineteresante de manera que logre captar la mayoria de los datos importantes a transmitir.
### **Resultados y conclusiones**

### **Contribución y colaboración**
¡Gracias por considerar contribuir a este proyecto! Valoramos y damos la bienvenida a las contribuciones de la comunidad. Si tienes ideas para mejorar la estructura del proyecto o cualquier otra sugerencia, no dudes en proponer cambios.

<div id="header" align="center">
  <img src="https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExbDQ2NzViaGJldXl2YXdlMmxqMXh2cmdiYW00am9xa3ZpYTRpeTZsayZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/1CsHxj6Q2iEeH4HhT7/giphy.gif" width="150"/>
</div>

### **Autores**
Gustavo Pardo Bermudez / Data Analist


