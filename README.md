# Analisys Data Project - Forum Repraesentativas Exchange Rate Praedictio

==============================================================================

## Este proyecto busca poder abordar una problemática de análisis de datos con condiciones reales, tal como ocurriría en cualquier empresa o entidad.

Elija alguno de los datasets que se encuentran en las páginas de datos abiertos de USA (https://data.gov/) o Colombia (https://www.datos.gov.co/). Asuma que usted fue contratado por dicha empresa o entidad para realizar un proyecto de analítica que resuelva alguna problemática que pueda ser abordada con el dataset elegido. La problemática debe ser relacionada con la temática de modelamiento de series de tiempo.
Tenga en cuenta que el dataset elegido debe tener una volumetría no muy pequeña (no puede ser un conjunto de datos muy pequeño).
De esta forma, siga todas las etapas y subetapas de la metodología CRISP-DM de principio a fin para dar solución a esta problemática. Se pueden guiar de este link: https://pdf4pro.com/amp/cdn/crisp-dm-1-the-modeling-agency-com-73581e.pdf 
El proyecto puede ser realizado en equipos de máximo 3 personas.

Los entregables del proyecto serían los siguientes:

1.	Informe en Word que explique cómo se ejecutaron y cuáles fueron los resultados de cada una de las etapas y subetapas de este proyecto, siguiendo la estructura propuesta por CRISP-DM en https://pdf4pro.com/amp/cdn/crisp-dm-1-the-modeling-agency-com-73581e.pdf. Se deben guiar del documento para las secciones y subsecciones que debe contener este informe (además de la portada y la introducción al documento, en total serían 6 secciones según lo dispuesto en CRISP-DM, cada una con múltiples subsecciones).

2.	Se deben entregar también los notebooks utilizados para todo el desarrollo del proyecto, incluyendo los códigos ejecutados y las salidas de cada uno. Se recomienda entregar al menos 4 notebooks: uno para todo el análisis exploratorio y la preparación de datos, otro para el modelamiento, otro para la evaluación de resultados del modelo escogido y un último para el uso del modelo en producción (este último debe permitir generar nuevas predicciones a futuro bajo demanda del usuario, teniendo en cuenta que es posible que este usuario le suministre una versión actualizada a la fecha de los datos).

==============================================================================

## Introducción

La Tasa de Cambio Representativa del Mercado (TCRM), corresponde al promedio ponderado de las operaciones de compra y venta de contado de dólares de los Estados Unidos de América a cambio de moneda legal colombiana.
Este documento modela los tipos de cambio anuales entre USD/CO, y compara los datos reales con pronósticos desarrollados utilizando análisis de series de tiempo durante el período de 1992 a 2022. Los datos semanales oficiales del Banco Nacional de la República de Colombia se utilizan para el presente estudio. El objetivo principal de este documento es aplicar el modelo ARIMA para la previsión de tipos de cambio semanales de USD/CO. La precisión del pronóstico se compara con el error absoluto medio (MAE) y el error cuadrático medio (MSE).

------------------------------------------------------------------------------------------------
1.	Entendimiento de negocio

Esta etapa se refiere a la predicción del precio de dólar. En esta etapa se necesita una comprensión de los antecedentes y objetivos de los procesos relacionados con la bolsa de valores, incluyendo:

a)	Establecer objetivos comerciales
•	El objetivo comercial de hacer investigación es reconocer el precio del dólar de meses anteriores para determinar la predicción de la moneda en la posteridad para que se puedan tomar políticas y acciones si las predicciones no son apropiadas y conocer la relación de otros factores que afectan su valor.


b)	Evaluar la situación
•	El precio del dólar con respecto a la moneda colombiana está influenciado por factores internos y externos. Factores internos, exportaciones, el precio del petróleo y factores externos, inversionistas extranjeros y los capitales golondrina.


c)	Determinar el propósito de la minería de datos
•	El propósito de la minería de datos o el propósito de este estudio es explorar el conocimiento sobre los patrones de influencia de los factores externos en el precio del dólar con respecto a al peso colombiano para la predicción del valor futuro.


d)	Preguntas que el modelo responderá
•	¿Puedo predecir el precio del dólar con respecto al peso colombiano con los datos de hace una semana? 
•	¿Cuántos datos debería entrenar para poder obtener el precio del dólar del día siguiente?
•	¿Es buen momento para hacer negocios en esta divisa?

e)	Riesgos
•	Los datos no presentan riesgos, pues son extraídos de una fuente confiable, este sistema lo establece el mercado de divisas sobre la oferta y la demanda del peso colombiano en particular en relación con el dólar estadounidense. Además, el tipo de cambio se guía por el impacto significativo de las actividades de los bancos centrales y otras instituciones financieras. 


2.	Entendimiento de datos

•	En los datos obtenidos existen pocas variables, pues solo se requiere la fecha y el valor del dólar actual para poder predecir el valor futuro, es difícil que tengamos datos faltantes, ya que los datos se actualizan constantemente (lunes - viernes) y es imposible que haya algún error en la toma de datos.

•	Los datos de series temporales que estamos utilizando se pueden encontrar en https://www.datos.gov.co/Econom-a-y-Finanzas/Tasa-de-Cambio-Representativa-del-Mercado-TRM/32sa-8pi3. Los datos históricos se pueden recuperar utilizando la hoja de Excel ingresando la abreviatura de moneda estándar, fecha de inicio y fecha de finalización. Usando la API anterior, hemos recopilado datos de los últimos 30 años a partir de 1992 para el dólar con respecto al peso colombiano.

•	La fecha se entregó en un formato distinto al "datetime", por lo tanto, debemos realizar las conversiones necesarias para poder poner este formato estándar en todas las fechas, luego, esta fecha será el índice de nuestra tabla para poder graficar bien nuestros datos.

•	Para poder modelar se necesita también ajustar el periodo de las fechas, ya que como los datos son entregados de lunes a viernes, y el modelo no responde a este orden, porque se necesita una secuencia uniforme. Por lo tanto, se reorganiza de manera semanal para que puedan ser modelados.


3.	Preparación de datos

•   La etapa de preparación de datos es la preparación del conjunto de datos, los datos utilizados para el modelado. En esta etapa se selección y construyen los datos, se elige la tabla relacionada para simplificar el proceso de selección de datos. Esta tabla contiene el valor del peso colombiano frente al dólar estadounidense con su respectiva fecha de registro. Contiene 7431 datos con variaciones, se re-muestrean para que queden con una frecuencia semanal.

•   El uso de datos diarios para su serie temporal contiene demasiada variación (lunes a viernes), por lo que primero debe volver a muestrear los datos de la serie temporal por semana. Luego use esta serie de tiempo remuestreada para predecir los tipos de cambio del peso colombiano frente al dólar estadounidense:

4.	Modelado de datos

•  Para este proyecto, el primer modelo que construimos fue el modelo ARIMA (Promedio móvil integrado autorregresivo). La técnica ARIMA es un modelo estadístico que se utiliza para pronosticar el conjunto de datos que tiene una naturaleza de serie temporal. El modelo ARIMA no es más que una composición de tres modelos, a saber, autorregresión (AR), integración (I) y media móvil (MA).

•  Recordemos que los hiperparámetros de un modelo ARIMA son (p,d,q), donde p es para la parte "AR" (cuántos rezagos incluir), d es para la parte "I" (cuántas veces integrar o diferenciar la serie) y la q es para la parte "MA" (cuántos medias móviles del error se incluirán).

•  Observando detenidamente la gráfica, vemos que los datos de tipos de cambio de divisas entre USA y colombia no son estacionarios y esto es cierto para cualquier tipo de cambio de moneda. Para hacerlo estacionario se tuvo que diferenciar la serie, en el modelo ARIMA para apli•  car este cambio la "d" será igual a 1. Nos falta determinar entonces valores para la p y la q.

<p align="center">
  <img src="resources\ARIMA.png" width="600" title="hover text">
</p>

•  Podemos observar que el modelo que más exacto dio, fue el ARIMA, por lo tanto seguiremos con este, sin embargo, sus resultados fueron muy parecidos, procedemos a realizar la predicción de los datos futuros.

----------------------------------------------------------------------------------------------------------------------

<p align="center">
  <img src="resources\ARIMA_PRAEDICTIO.png" width="600" title="hover text">
</p>

Conclusión
•   En este proyecto la técnica ARIMA fue la que se usó para la modelación, fue mejor esta que la técnica SARIMA, en todos los casos no será así, por eso se deben probar diferentes técnicas para el modelado de los datos.

•   La técnica ARIMA para pronosticar los tipos de cambio de divisas del peso colombiano frente al dólar estadounidense (USD), se aplicó durante el período de 1992 a 2022. Se utilizó el software Python para la predicción. de los tipos de cambio. Se presentó la técnica ARIMA y se identificaron tres pasos principales para construir el modelo, a saber, Identificación, Estimación y Verificación del modelo. Además, se estimó el modelo de pronóstico y se comparó con los datos reales de la moneda. La eficacia de los resultados del modelo de pronóstico se comparó con el error absoluto medio (MAE) y el error cuadrático medio (MSE).