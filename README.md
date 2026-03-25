# LABORATORIO 3: Cálculo ambulatorio del índice pletismográfico quirúrgico
# INTRODUCCIÓN
El manejo adecuado del dolor es un aspecto fundamental en procedimientos médicos, especialmente en entornos quirúrgicos donde el paciente no puede expresar de forma directa su percepción nociceptiva. Por tal motivo, se han desarrollado métodos que permiten estimar el nivel de dolor de manera objetiva a partir de señales fisiológicas, como lo es el índice pletismográfico quirúrgico (SPI), el cual se obtiene a partir de la señal fotopletismográfica (PPG), asociada a las variaciones del volumen sanguíneo periférico.

El SPI toma valores entre 0 y 100, donde rangos elevados indican una mayor respuesta del organismo ante estímulos nociceptivos. Este índice se basa en el análisis de características de la onda de pulso, permitiendo evaluar el equilibrio entre nocicepción y analgesia. Su importancia radica en que ofrece una herramienta cuantitativa para el monitoreo del dolor, complementando la valoración clínica tradicional.

En esta práctica de laboratorio se propone el desarrollo de un sistema capaz de adquirir la señal PPG, procesarla y calcular el SPI de forma continua. Además, se analiza la respuesta fisiológica del organismo ante estímulos controlados como el Cold Pressor Test, lo que permite evidenciar cambios en la señal y en el índice calculado.
# FUNDAMENTOS TEÓRICOS
## Cold pressor test
El Cold Pressor Test (CPT) es un procedimiento experimental muy utilizado en estudios fisiológicos y clínicos para inducir una respuesta nociceptiva de manera controlada. La técnica consiste en la inmersión de una extremidad, comúnmente la mano, en agua a bajas temperaturas, típicamente entre 0 °C y 4 °C, durante un intervalo de tiempo definido, generando así un estímulo térmico que activa los nociceptores periféricos, desencadenando una respuesta del sistema nervioso autónomo, particularmente del sistema simpático.

Diversos estudios han demostrado que el CPT produce efectos fisiológicos consistentes, como el incremento de la frecuencia cardíaca, el aumento de la presión arterial y la vasoconstricción periférica. Esta última genera modificaciones en la señal fotopletismográfica (PPG), especialmente en la amplitud de la onda de pulso, debido a la reducción del flujo sanguíneo en los tejidos periféricos. En este sentido, el CPT se considera una herramienta válida y reproducible para simular condiciones de dolor agudo en entornos experimentales, permitiendo analizar la respuesta cardiovascular y autonómica del organismo.
## Fundamento matemático del SPI
El índice pletismográfico quirúrgico (SPI) es un parámetro diseñado para cuantificar el balance entre nocicepción y analgesia a partir de variables fisiológicas obtenidas de la señal fotopletismográfica. Este índice combina información relacionada con la actividad cardiovascular y la dinámica vascular periférica, reflejando la influencia del sistema nervioso autónomo sobre estas variables.

Desde el punto de vista matemático, el SPI se calcula a partir de dos componentes  principales: la amplitud de la señal fotopletismográfica (PPGA) y el intervalo entre latidos cardíacos (HBI). Ambos parámetros son previamente normalizados con el fin de estandarizar su contribución al índice. La expresión general del SPI se define como:

$$
SPI = 100 - (0.33 \cdot PPGA_{norm} + 0.67 \cdot HBI_{norm})
$$

Esta formulación asigna un mayor peso al intervalo entre latidos cardíacos, lo cual se justifica por la fuerte relación entre la variabilidad cardíaca y la activación del sistema nervioso simpático. Por otro lado, la amplitud de la señal PPG refleja cambios en el tono vascular periférico, particularmente aquellos asociados a procesos de vasoconstricción inducidos por el estrés o el dolor.

El SPI se expresa en una escala de 0 a 100, donde valores bajos indican un estado de menor activación nociceptiva, mientras que valores elevados sugieren una mayor respuesta al dolor o al estrés fisiológico. En entornos clínicos, este índice ha sido utilizado como una herramienta para optimizar la administración de analgésicos durante procedimientos quirúrgicos, proporcionando una medida objetiva complementaria a la evaluación clínica tradicional.
