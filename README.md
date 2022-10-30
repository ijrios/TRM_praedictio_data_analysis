# Analisys Data Project - Forum Repraesentativas Exchange Rate Praedictio

## Este proyecto busca poder abordar una problemática de análisis de datos con condiciones reales, tal como ocurriría en cualquier empresa o entidad.

Elija alguno de los datasets que se encuentran en las páginas de datos abiertos de USA (https://data.gov/) o Colombia (https://www.datos.gov.co/). Asuma que usted fue contratado por dicha empresa o entidad para realizar un proyecto de analítica que resuelva alguna problemática que pueda ser abordada con el dataset elegido. La problemática debe ser relacionada con la temática de modelamiento de series de tiempo.
Tenga en cuenta que el dataset elegido debe tener una volumetría no muy pequeña (no puede ser un conjunto de datos muy pequeño).
De esta forma, siga todas las etapas y subetapas de la metodología CRISP-DM de principio a fin para dar solución a esta problemática. Se pueden guiar de este link: https://pdf4pro.com/amp/cdn/crisp-dm-1-the-modeling-agency-com-73581e.pdf 
El proyecto puede ser realizado en equipos de máximo 3 personas.

Los entregables del proyecto serían los siguientes:

1.	Informe en Word que explique cómo se ejecutaron y cuáles fueron los resultados de cada una de las etapas y subetapas de este proyecto, siguiendo la estructura propuesta por CRISP-DM en https://pdf4pro.com/amp/cdn/crisp-dm-1-the-modeling-agency-com-73581e.pdf. Se deben guiar del documento para las secciones y subsecciones que debe contener este informe (además de la portada y la introducción al documento, en total serían 6 secciones según lo dispuesto en CRISP-DM, cada una con múltiples subsecciones).

2.	Se deben entregar también los notebooks utilizados para todo el desarrollo del proyecto, incluyendo los códigos ejecutados y las salidas de cada uno. Se recomienda entregar al menos 4 notebooks: uno para todo el análisis exploratorio y la preparación de datos, otro para el modelamiento, otro para la evaluación de resultados del modelo escogido y un último para el uso del modelo en producción (este último debe permitir generar nuevas predicciones a futuro bajo demanda del usuario, teniendo en cuenta que es posible que este usuario le suministre una versión actualizada a la fecha de los datos).

## Introducción

La Tasa de Cambio Representativa del Mercado (TCRM), corresponde al promedio ponderado de las operaciones de compra y venta de contado de dólares de los Estados Unidos de América a cambio de moneda legal colombiana.
Este documento modela los tipos de cambio anuales entre USD/CO, y compara los datos reales con pronósticos desarrollados utilizando análisis de series de tiempo durante el período de 1992 a 2022. Los datos semanales oficiales del Banco Nacional de la República de Colombia se utilizan para el presente estudio. El objetivo principal de este documento es aplicar el modelo ARIMA para la previsión de tipos de cambio semanales de USD/CO. La precisión del pronóstico se compara con el error absoluto medio (MAE) y el error cuadrático medio (MSE).

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

Conclusión
•	La técnica ARIMA para pronosticar los tipos de cambio de divisas del peso colombiano frente al dólar estadounidense (USD), se aplicó durante el período de 1992 a 2022. Se utilizó el software Python para la predicción. de los tipos de cambio. Se presentó la técnica ARIMA y se identificaron tres pasos principales para construir el modelo, a saber, Identificación, Estimación y Verificación del modelo. Además, se estimó el modelo de pronóstico y se comparó con los datos reales de la moneda. La eficacia de los resultados del modelo de pronóstico se comparó con el error absoluto medio (MAE) y el error cuadrático medio (MSE).
