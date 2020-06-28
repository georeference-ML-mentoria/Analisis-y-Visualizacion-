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

**Cuáles son las variables categóricas? Cuál es la cardinalidad de las mismas?**

* CONJ, que si bien es numérica es sólo un código; su orden numérico no nos es útil. Su cardinalidad es de 6.
* BRR, con cardinalidad 706.
* CLAS_SUB, con cardinalidad 28.
* CNAE, con cardinalidad 142.
* FAS_CON, con cardinalidad 9.
* GRU_TEN, con cardinalidad 1.
* TEN_FORN, con cardinalidad 1.
* GRU_TAR, con cardinalidad 6.
* ARE_LOC, con cardinalidad 3.
* SIT_ATIV, con cardinalidad 2.

Con respecto a PAC: su cardinalidad es 145433. Este es un número muy alto, cercano al cardinal del conjunto de datos. La razón es que suele haber sólo un punto de acoplamiento para cada unidad consumidora. Por esta razón, me parece que no debería considerarse variable categórica; si fuese así la gran mayoría de las categorías tendría un solo elemento.

A pesar de que DAT_CON no es numérica no puedo considerarla categórica ya que contiene pares fecha-hora, los cuales pueden resultarnos útiles si están ordenados.

**En base a la respuesta anterior, ¿vale la manera mantenerlas a todas?**

Creo que GRUN_TEN y TEN_FORN no valen la pena, ya que todas las unidades pertenecen al mismo grupo de tensión (BT, "Baja Tensión") y tienen el mismo código de tensión de suministro (22).

**Cuáles son los 3 valores más comunes de cada categoría?**

| Variable | Valor más común                          | Segundo valor más común                        | Tercer valor más común                       |
| -------- | ---------------------------------------- | ---------------------------------------------- | -------------------------------------------- |
| CONJ     | 15602 (42090 consumidores)               | 12737 (32909 consumidores)                     | 12743 (28465 consumidores)                   |
| MUN      | 2802106 ("Estância", 30785 consumidores) | 2807402 ("Tobias Barreto", 22570 consumidores) | 2803005 ("Itabaianinha", 16067 consumidores) |
| BRR      | CENTRO (20614 consumidores)              | TOBIAS BARRETO (10151 consumidores)            | RIO REAL (9913 consumidores)                 |
| CLAS_SUB | RE1 (99475 consumidores)                 | RE2 (31682 consumidores)                       | CO1 (6860 consumidores)                      |
| CNAE     | 0 (148046 consumidores)                  | 6190601 (101 consumidores)                     | 9491000 (57 consumidores)                    |
| FAS_CON  | AN (96082 consumidores)                  | BN (21575 consumidores)                        | CN (12284 consumidores)                      |
| GRU_TEN  | BT (148801 consumidores)                 |                                                |                                              |
| TEN_FORN | 22 (148801 consumidores)                 |                                                |                                              |
| GRU_TAR  | B1 (130596 consumidores)                 | B3 (12297 consumidores)                        | B2RU (5001 consumidores)                     |
| ARE_LOC  | UB (87973 consumidores)                  | NU (60790 consumidores)                        | 0 (38 consumidores)                          |
| SIT_ATIV | AT (145609 consumidores)                 | DS (3192 consumidores)                         |                                              |

**Escoja dos variables y grafique sus niveles contra la cantidad de apariciones.**

Variable FAS_CON (códigos de referencia de fases de conexión):

![Gráfico de barras de FAS_CON](images/fas_con_bar_plot.png)

Variable GRU_TAR (grupos tarifarios):

![Gráfico de barras de GRU_TAR](images/gru_tar_bar_plot.png)

**Cuando sea posible calcule la correlacion entre cada variable y la salida, y entre variables.** <br>

El primer paso en establicer un relacion predictivo es identificar correlacion entre variables, definiendo nuestros variables independientes (x) y dependientes (y). 
Buscamos un "correlation" test para cada variable con "DIC", una variable quantitativa. En el caso de tener dos variables quatitativas podemos calcular el coeficiente de correlacion; e.g. x= 'CAR_INST', y ENE_01, ENE_02... ENE_12. Para identificar una correlacion entre una variable quantitativa (DIC) y una variable categorica usamos la ANOVA test, que nos dio un frequencia o f-statistic y un p-valor del test de correlacion. Un p-valor de zero significa que no podemos rechazar el hipothesis de que los variables tiene correlacion.  

Usamos DIC porque en general nos dio resultados como con salida con correlation mas grande.

### Numeric con numeric: coeficiente de correlacion o "R"
| entrada | salida| R|
| -------- | -----|--------|
|x='CAR_INST'|y='DIC'|-0.00236|
|x='ENE_01'|y='DIC'|-0.00526|
|x='ENE_02'|y='DIC'|-0.00626|
|x='ENE_03'|y='DIC'|-0.00591|
|x='ENE_04'|y='DIC'|-0.00669|

### Categorical con numeric (DIC): ANOVA statistic
| entrada | salida| correlation ratio|
| -------- | -----|------------------|
|x='CONJ'|y='DIC'|0.212|
|x='ARE_LOC'|y="DIC"|0.427|
|x='GRU_TAR'|y="DIC"|0.101|
|x='CNAE'|y='DIC'|0.038|


**Cual es la variable de mayor correlacion con la salida.** <br>
Segun a este experimento, la área donde se ubica la unidad de consumo, ARE_LOC, tiene mayor correlacion con DIC. Tambien notable son las correlacciones de activadad economico, CNAE, y departemento donde esta ubicado el consumido, CONJ, con DIC. 

**Escoja una variable categorica y calcule las distribuciones condicionales para cada nivel de la misma.** <br>
Eligimos la variable GRU_TAR (grupo tarifario). Primero categorizamos la variable DIC en tres categorias low, medium y high, para generar la tabla abajoe que muestra la frequencia de  GRU_TAR para cada rango de variables DIC.  

| GRU_TAR |low|medium|high|
|----|------|----|----|
| B1 | 26499|33601|35930|
| B1BR| 146|205|246|
| B2RU| 510|994|1333|
| B2SP| 0|1|1|
| B3| 2561|3442|2953|

Vemos que la duracion de corte esta mas o menos distribuido igualment entre todos las grupos de tarifario.

## 3 - Preguntas <br>

**Como podemos saber si las distribuciones condicionales son diferentes entre ellas?** <br>
Con un simple "for loop" se puede calcular el consumo total anual de cada consumidor.<br>
```
annual_totals = []
for index, row in data.iterrows():
    annual_total = row.ENE_01+row.ENE_02+ \
     row.ENE_03+row.ENE_04+row.ENE_05+ \
    row.ENE_06+row.ENE_07+row.ENE_08+ \
    row.ENE_09+row.ENE_10+row.ENE_11+ \
    row.ENE_02
    annual_totals.append(annual_total)
print(annual_totals[:10])
```
Despues podes agregar la lista ```annual_totals``` a tu dataset como una nueva columna ```data['consumo_anual'] = annual_totals```.<br>
<br> Por ejemplo, el promedio de consumo por consumidor era ```data.consumo_anual.mean()= 1392.671```kWh, maximum ```data.consumo_anual.max()= 7825074.0```, y el desvio estandar ```data.consumo_anual.std()= 27441.344``` .<br>
Existe correlacion entre consumo y frecuencia de corte de servicio (FIC)? <br>
Segun a nuestros calculos, hay un valor R de -0.00696 entre el consumo anual y FIC.<br>
**Como varia el servicio entre zonas urbanas y rurales?** <br>
Segun a este heatmap, la duración del corte es mas larga en zonas rurales que zonas urbanos. 
![heatmap of duracion of corte](images/heatmap_are_loc_dic.png "heatmap of duracion of corte")


**Como varia el consumo entre zonas urbanas y rurales?** <br>
Segun a este heatmap, el consumo anual es mas larga en zonas rurales que zonas urbanos.
![heatmap of consumo anual](images/heatmap_are_loc_consumo.png "heatmap of consumo anual")

**Cuáles son las diez actividades económicas más comunes de la región?**

Para más del 99% de los consumidores de este conjunto de datos (unidades consumidoras de baja tensión) no se registra actividad económica. Entre el resto -- una proporción muy pequeña -- estas son las diez actividades más comunes:

* 101 consumidores son **proveedores de accesso a redes de comunicaciones** (código 6190-6/01).
* 57 consumidores en **actividades de organizaciones religiosas** (código 9491-0/00).
* 43 consumidores en el **área de construcción de edificios** (código 4120-4/00).
* 38 consumidores en el **área de servicios de comunicación multimedia** (código 6110-8/03).
* 37 consumidores en **actividades odontológicas** (código 8630-5/04).
* 30 consumidores en **asociaciones de defensa de los derechos sociales** (código 9430-8/00).
* 28 consumidores en **incorporación de emprendimientos inmobiliarios** (código 4110-7/00).
* 27 consumidores en **captación, tratamiento y distribución de agua** (código 3600-6/01).
* 23 consumidores en **administración pública en general** (código 8411-6/00).
* 19 consumidores con **criaderos de ganado para faena** (código 0151-2/01).

**Dentro de ellas:**

**Cuáles tienen mayor y menor frecuencia de corte?**

* La mayor frecuencia de corte la tiene, sin dudas, el **área de construcción de edificios** (código 4120-4/00) con el 86% de las unidades consumidoras reportando de 9 a 12 cortes (mensuales?).
* La menor frecuencia de corte la tiene el área de **incorporación de emprendimientos inmobiliarios** (código 4110-7/00) con el 86% de las unidades consumidoras reportando 4 cortes (mensuales?) o menos.

**Cuáles son las de mayor y menor consumo?**

* La actividad que más consume es el **área de construcción de edificios** (código 4120-4/00) con 251130 kWh anuales.
* La actividad que menos consume es el área de **incorporación de emprendimientos inmobiliarios** (código 4110-7/00) con 13866 kWh anuales.
