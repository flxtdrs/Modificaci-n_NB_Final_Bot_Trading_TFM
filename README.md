# Modificaci-n_NB_Final_Bot_Trading_TFM
TFM Matestria IA aplicado a los mercados financieros (Notebook_Bot_trading)
Ajustes realizados al modelo: sin realizar grandes cambios al modelo inicial, esta modificación logra pasar la prueba sin romper  ninguna de las otras reglas. Les describo un poco sobre los cambios realizados:

MODIFICACIONES EN EL MODELO 

TODOS LOS PARAMETROS DE INDICADORES QUEDAN EXACTAMENTE IGUAL. SOLO SE AGREGA EL CALCULO DEL LOTAJE 

LOTAJE = 100

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
EL CÁLCULO DEL LOTAJE:
SE EVALUO EL MODELO CON 1 LOTE PARA TOMAR EL PROMEDIO DE OPERACIONES POR DIA Y LOS PUNTOS PROMEDIOS POR SL

Metrica                             IN-SAMPLE     BACKTEST      FORWARD        TOTAL
Operaciones por dia                      0.71         0.66         0.92         0.77
SL promedio (pts)                        3.79          4.9         4.77         4.07

EL SL PROMEDIO  MAS ALTO ES 4.9 PTS, SE RENDONDEA A 5.

Asumiendo que el peor de los días ocurren 3 señales:
(PTS PROMEDIOS POR SL) X (Nº SEÑALES EN EL DIA)

                                     5 x 3 = 15

POR LO TANTO:
             EL TAMAÑO DE LA POSICION SE OBTENDRIA AL DIVIDIR LOS 1500E ESTIPULADOS EN LA GESTION DE RIESGO ENTRE EL TOTAL DE PUNTOS QUE PODRIA PERDER EL MODELO EN CASO DE QUE SE DEN 3 SEÑALES EN UN DIA.

                                1500/ (15) = 100 LOTES

EN EL CASO DE LAS DEMAS EMPRESAS DE FONDEO, AL DARLE AL MODELO LA PERDIDA MAXIMA DIARIA, ESTE VALOR SE DIVIDE ENTRE 2 Y POSTERIORMETE ENTRE 15. EN NUESTRO CASO LA PERDIDA MAXIMA EN GEDLEVARAGE DIRIA ERA 3000 Y CON EL SISTEMA DE RIESGO SE ACORDO EN 1500.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

EN CUANTO A LO PARAMETROS ANTI-OVERFITING SE VARIA EN EL MODULO DE ML:

MAX_DEPTH = DE 4 A 3        ; Se baja a 3 para que el modelo aprenda de reglas generales, limitándolo a solo tres niveles de profundidad.

N_ESTIMATORS =150           ; Se aumenta el numero de arboles para darle más perspectivas al modelo para promediar, esto no provoca sobreajuste.


# Random Forest con parametros anti-overfitting
modelo = RandomForestClassifier(
    n_estimators=200,
    max_depth=3,

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

SE AGREGA UN ALGORITMO PARA QUE EL MODELO AL INICIAR PIDA SI TRABAJARA CON LOS PARAMETROS GEDLEVERAGED (ESTA POR DEFECTO) O CON REGLAS DE OTRA EMPRESA. EN ESTE ÚLTIMO CASO PEDIRA LAS REGLAS GENERALES DE LA OTRA EMPRESA.
