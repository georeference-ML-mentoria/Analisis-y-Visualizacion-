# Analisis-y-Visualizacion-
Analisis de calidad de suministro electrico

1 - Analisis General¶
Cuantas entradas posee el dataset y que representa cada una? <br>
40 (original), 28 (eligidos),  <br>
Glossary: (Guillermo) TABLA <br>

nombre | traduccion | descripcion | numerica/categorica

Si queremos analizar calidad de servicio cual seria a su parece la variable de salida?
FIC o DIC?<br>

2 - Analisis Estadistico <br>
Cuales son las variables numericas? TABLA<br>

Guillermo<br>
Cuanto valen los principales estadisticos?<br>
Existen valores que no sean validos? Cuales? Que se puede hacer en esos casos? <br>
Poseen outliers? Que tecnicas se pueden utilizar para mitigar su impacto. <br>
Como es la distribucion de los valores? Son normales? <br>
Calcule los principales estadisticos despues del preprocesamiento. <br>
Adicione los graficos o tablas que considere oportuno para graficar los puntos anteriores. <br>

Javier <br>
Cuales son las variables categoricas? Cual es la cardinalidad de las mismas? <br>
En base a la respuesta anterior vale la manera mantenerlas a todas? <br>
Cuales son los 3 valores mas comunes de cada categoria? <br>
Escoja 2 variables y grafique sus niveles contra la cantidad de apariciones. <br>

Brandon <br>
**Cuando sea posible calcule la correlacion entre cada variable y la salida, y entre variables.** <br>
The first step in establishing a predictive relationship is identifying correlation between variables and next defining the independent variable, and dependent variables in those correlations. 
x= 'CONJ', y='FIC' or "DIC" 
x= 'ARE_LOC', y='FIC' or "DIC"
x= 'GRU_TAR', y='FIC' or "DIC"
x= 'DIC', y='FIC' or "DIC"
x= 'ENE_01', y='FIC' or "DIC"
x= 'CAR_INST', y='FIC' or "DIC"

We identified 18 variables that could be considered independent ("entrada" o "X") en nuestro correlacion, pero solamente que mostraron correlacion notable. 
There exists a positive correlation between DIC and FIC, but that doesn't help us much since those are both our supposed salidas. 

**Cual es la variable de mayor correlacion con la salida.** <br>


**Escoja una variable categorica y calcule las distribuciones condicionales para cada nivel de la misma.** <br>

**Como podemos saber si las distribuciones condicionales son diferentes entre ellas?** <br>

3 - Preguntas <br>

Brandon <br>
Calcule el consumo total anual de cada consumidor. <br>
Existe correlacion entre consumo y frecuencia de corte de servicio (FIC)? <br>
Como varia el servicio entre zonas urbanas y rurales? <br>
Como varia el consumo entre zonas urbanas y rurales? <br>

Javier <br>
Cuales son 10 actividades economicas mas comunes de la region? <br>
Dentro de ellas: <br>
Cuales tienen mayor y menor frecuencia de corte <br>
Cuales son las de mayor y menor consumo? <br>