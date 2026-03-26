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
# DESARROLLO DE LA PRÁCTICA
## Circuito para capturar las variaciones del volumen sanguíneo periférico.

El desarrollo de la práctica inició con la implementación del circuito mostrado acontinuación, cuyo objetivo era la adquisición de la señal fotopletismográfica (PPG) a partir de un sensor óptico de reflectancia. Para ello, se utilizó el dispositivo TCST110, el cual fue adaptado para funcionar como sensor reflectivo, separando el emisor infrarrojo y el fototransistor receptor, de manera que ambos quedaran orientados hacia el dedo del voluntario. Esta configuración permitóia que la luz emitida incidiera sobre el tejido y la señal reflejada fuera capturada por el fotodetector, en función de las variaciones del volumen sanguíneo.

La primera etapa del circuito correspondió al sistema de excitación del emisor óptico, en donde se empleó un transistor 2N3904 junto con una red de polarización para suministrar la corriente necesaria al diodo emisor del TCST110. El ajuste de esta etapa resultaba fundamental, ya que la intensidad de la luz incidente actúa directamente en la calidad de la señal reflejada. Posteriormente, en la etapa de detección, el fototransistor del sensor convirtió la luz reflejada en una señal eléctrica, la cual contenía tanto una componente continua dominante como una componente alterna asociada al pulso sanguíneo.

A continuación, la señal fue sometida a un proceso de acondicionamiento. En primer lugar, se implementó un filtro pasaaltas pasivo con el fin de eliminar la componente DC y resaltar las variaciones pulsátiles. Luego, la señal ingresó a una etapa de filtrado activo pasa bajas con ganancia, basada en un amplificador operacional LM358, la cual permitió amplificar la señal y reducir el ruido de alta frecuencia. Posteriormente, mediante el uso de potenciómetros, se realizaron ajustes de amplitud y offset, con el objetivo de evitar la saturación de la señal y ubicarla dentro de un rango adecuado para su adquisición por parte del Arduino.

A pesar de haber realizado el montaje completo del circuito y los ajustes correspondientes, no fue posible obtener una señal fotopletismográfica estable y con una relación señal-ruido adecuada. 

Debido a estas limitaciones, se optó por emplear el módulo MAX30102, el cual integra el sistema de emisión, detección y acondicionamiento de la señal en un solo dispositivo. Este módulo permitió obtener una señal PPG mucho más estable y confiable, facilitando su adquisición y posterior procesamiento para el cálculo del índice SPI.
<img width="760" height="400" alt="image" src="https://github.com/user-attachments/assets/3c9ef379-91d1-47d9-b8fe-e22bb0431ee1" />
## Fase experimental
Para la fase experimental se empleó la técnica del Cold Pressor Test con el objetivo de inducir una respuesta fisiológica asociada a un estímulo nociceptivo controlado. Para ello, se llevó previamente al laboratorio una bolsa con hielo, asegurando que estuviera a una temperatura suficientemente baja para generar un estímulo efectivo. Durante la medición, el voluntario se mantuvo en reposo, con el sensor correctamente ubicado en el dedo y procurando minimizar el movimiento para evitar alteraciones en la señal adquirida.

El procedimiento se desarrolló siguiendo los tiempos establecidos en la guía, iniciando con una fase basal de 40 segundos en reposo, durante la cual se registró la señal PPG sin ningún tipo de estímulo externo. Esta etapa permitió obtener una referencia del comportamiento fisiológico del sujeto en condiciones estables y sirvió como punto de comparación para las siguientes fases.

Posteriormente, se dio inicio a la fase de estímulo, en la cual se colocó la bolsa con hielo sobre la mano del voluntario durante 40 segundos, manteniendo la adquisición continua de la señal. Este estímulo térmico induce la activación del sistema nervioso simpático, lo que se traduce en fenómenos como vasoconstricción periférica y cambios en la frecuencia cardíaca, afectando directamente la forma y amplitud de la señal fotopletismográfica.

Finalmente, se retiró la bolsa de hielo y se continuó con la adquisición durante los 40 segundos restantes, correspondientes a la fase de recuperación. En esta etapa se buscó observar el retorno progresivo de las variables fisiológicas hacia sus valores basales, evidenciando la disminución de los efectos provocados por el estímulo frío. Durante todo el experimento la señal fue registrada de manera continua, lo que permitió analizar su comportamiento en cada fase y utilizarla posteriormente para el cálculo del índice SPI.

# IMPLEMENTACIÓN DEL SISTEMA
## Programación del microcontrolador 

```bash
#include <Wire.h>
#include "MAX30105.h"

MAX30105 particleSensor;

float dc = 0.0;
const float alpha = 0.95;

void setup() {
  Serial.begin(115200);
  delay(1000);
  Wire.begin(21, 22);

  if (!particleSensor.begin(Wire, I2C_SPEED_STANDARD)) {
    Serial.println("MAX30105 no encontrado");
    while (1);
  }

  byte ledBrightness = 0x1F;
  byte sampleAverage = 4;
  byte ledMode = 2;
  int sampleRate = 100;
  int pulseWidth = 411;
  int adcRange = 4096;

  particleSensor.setup(ledBrightness, sampleAverage, ledMode, sampleRate, pulseWidth, adcRange);

  particleSensor.setPulseAmplitudeRed(0x00);
  particleSensor.setPulseAmplitudeIR(0x1F);
  particleSensor.setPulseAmplitudeGreen(0x00);
}

void loop() {
  long irValue = particleSensor.getIR();

  if (dc == 0) {
    dc = irValue;
  }

  dc = alpha * dc + (1.0 - alpha) * irValue;
  float ac = irValue - dc;
  float ppg = -ac;

  Serial.println(ppg);

  delay(10);
}
```
El código implementado tiene como objetivo la adquisición de la señal fotopletismográfica (PPG) utilizando el módulo MAX30102 conectado a una ESP32 mediante comunicación I2C, empleando los pines GPIO 21 (SDA) y GPIO 22 (SCL). Inicialmente, se establece la comunicación serial a 115200 baudios y se configura el sensor con una frecuencia de muestreo de 100 Hz, utilizando únicamente el canal infrarrojo para la captura de la señal.

La señal obtenida directamente del sensor contiene una componente continua elevada asociada a las condiciones de iluminación y al tejido, por lo que se aplica un filtrado sencillo basado en un promedio exponencial para estimar y eliminar dicha componente. De esta forma se obtiene una señal centrada en cero que resalta las variaciones pulsátiles del flujo sanguíneo. Posteriormente, la señal es invertida con el fin de facilitar la identificación de los picos correspondientes a cada latido durante el procesamiento posterior.

Finalmente, la señal procesada se envía por el puerto serial a una tasa aproximada de 100 muestras por segundo, permitiendo su visualización en tiempo real y su posterior análisis en MATLAB.

### Librerías utilizadas

Para la implementación del sistema fue necesario instalar la siguiente librería en el entorno de Arduino:

SparkFun MAX3010x Pulse and Proximity Sensor Library

Adicionalmente, se emplea la librería estándar:

Wire.h, utilizada para la comunicación I2C entre la ESP32 y el sensor

## Señal en el serial plotter

<img width="1182" height="736" alt="image" src="https://github.com/user-attachments/assets/d5be33b8-49cf-4b92-a408-f10bb26951bc" />

La gráfica obtenida en el Serial Plotter presenta una forma periódica compatible con la señal fotopletismográfica procesada. Se observan picos pronunciados hacia valores positivos y valles en la región negativa, lo cual indica que la componente continua fue removida y que la señal fue invertida correctamente para resaltar el pulso hacia arriba. Esta representación resulta adecuada para identificar máximos y mínimos de cada latido, que posteriormente serán utilizados para calcular la amplitud de pulso y el intervalo entre latidos.

La forma no sinusoidal de la señal es comprendible, ya que la PPG real depende de la dinámica del flujo sanguíneo, la presión del dedo sobre el sensor, el nivel de perfusión periférica y pequeñas variaciones por movimiento. Aun así, la presencia de pulsos repetitivos y distinguibles indica que la adquisición es funcional y que la señal es apta para el análisis posterior en MATLAB.
## Código en MATLAB}
``` bash
clc
clear
close all

puerto = "COM4";
baudrate = 115200;
fs = 100;
duracion = 120;
N = fs * duracion;

t_calibracion = 40;
t_cpt_inicio  = 40;
t_cpt_fin     = 80;
t_final       = 120;

ventana_visible = 12;

s = serialport(puerto, baudrate, 'Timeout', 2);
configureTerminator(s, "LF");
flush(s);

senal  = nan(N,1);
tiempo = nan(N,1);

PPGA = [];
HBI  = [];
t_spi = [];
SPI  = [];

locPicos   = [];
valPicos   = [];
locValles  = [];
valValles  = [];

calibrado = false;
PPGA_min = NaN;
PPGA_max = NaN;
HBI_min  = NaN;
HBI_max  = NaN;

ventana_suavizado = 5;
dist_min = round(0.40 * fs);
ultima_deteccion_pico  = -inf;
ultima_deteccion_valle = -inf;

amp_min = 5;
hbi_min = 0.30;
hbi_max = 2.00;

fig = figure('Name','MAX30102 - Senal y SPI en tiempo real','NumberTitle','off','Color','w');

subplot(3,1,1)
hSigRaw = plot(nan, nan); hold on
hSigFil = plot(nan, nan);
hPicos  = plot(nan, nan, 'rv');
hValles = plot(nan, nan, 'g^');

subplot(3,1,2)
hPPGA = plot(nan, nan);

subplot(3,1,3)
hSPI = plot(nan, nan);

tic

for i = 1:N

    if ~ishandle(fig)
        break
    end

    try
        dato = readline(s);
        valor = str2double(strtrim(dato));
    catch
        valor = NaN;
    end

    if isnan(valor)
        if i == 1
            valor = 0;
        else
            valor = senal(i-1);
        end
    end

    senal(i) = valor;
    tiempo(i) = toc;

    if tiempo(i) >= duracion
        if ishandle(fig)
            close(fig);
        end
        break
    end

    if tiempo(i) < t_cpt_inicio
        etapa = "Reposo";
    elseif tiempo(i) < t_cpt_fin
        etapa = "CPT";
    else
        etapa = "Recuperacion";
    end

    if i > ventana_suavizado
        senal_f = movmean(senal(1:i), ventana_suavizado);
    else
        senal_f = senal(1:i);
    end

    if i > 3
        x1 = senal_f(i-2);
        x2 = senal_f(i-1);
        x3 = senal_f(i);

        if (x2 > x1) && (x2 > x3)
            if (i-1 - ultima_deteccion_pico) >= dist_min
                locPicos(end+1,1) = i-1;
                valPicos(end+1,1) = x2;
                ultima_deteccion_pico = i-1;
            end
        end

        if (x2 < x1) && (x2 < x3)
            if (i-1 - ultima_deteccion_valle) >= dist_min
                locValles(end+1,1) = i-1;
                valValles(end+1,1) = x2;
                ultima_deteccion_valle = i-1;
            end
        end
    end

    if numel(locPicos) >= 2 && ~isempty(locValles)

        k = numel(locPicos);
        t_actual = tiempo(locPicos(k));

        if isempty(t_spi) || abs(t_actual - t_spi(end)) > 0.25

            idxValle = find(locValles > locPicos(k-1) & locValles < locPicos(k), 1, 'last');

            if ~isempty(idxValle)

                amp = valPicos(k) - valValles(idxValle);
                hbi = tiempo(locPicos(k)) - tiempo(locPicos(k-1));

                if amp > amp_min && hbi > hbi_min && hbi < hbi_max

                    PPGA(end+1,1)  = amp;
                    HBI(end+1,1)   = hbi;
                    t_spi(end+1,1) = t_actual;

                    idx_cal = t_spi < t_calibracion;

                    if ~calibrado && sum(idx_cal) >= 4 && tiempo(i) >= t_calibracion
                        PPGA_min = min(PPGA(idx_cal));
                        PPGA_max = max(PPGA(idx_cal));
                        HBI_min  = min(HBI(idx_cal));
                        HBI_max  = max(HBI(idx_cal));
                        calibrado = true;
                    end

                    if calibrado
                        PPGA_norm = (PPGA(end) - PPGA_min) / (PPGA_max - PPGA_min + eps);
                        HBI_norm  = (HBI(end)  - HBI_min)  / (HBI_max  - HBI_min  + eps);
                        spi_actual = 100 - 100*(0.33*PPGA_norm + 0.67*HBI_norm);
                        spi_actual = max(0, min(100, spi_actual));
                    else
                        spi_actual = NaN;
                    end

                    SPI(end+1,1) = spi_actual;
                end
            end
        end
    end

    drawnow limitrate
end

clear s
```
El código desarrollado en MATLAB permite la adquisición, procesamiento y análisis en tiempo real de la señal fotopletismográfica proveniente del sensor MAX30102 a través de comunicación serial. La señal es leída a una frecuencia aproximada de 100 Hz durante un intervalo de 2 minutos, dividido en tres etapas: reposo, aplicación del estímulo frío (CPT) y recuperación.

Una vez adquirida la señal, se aplica un suavizado mediante media móvil con el fin de reducir el ruido y facilitar la detección de eventos característicos. La identificación de máximos y mínimos se realiza mediante el método del alpinista, evaluando cambios de tendencia en tres muestras consecutivas de la señal. Adicionalmente, se impone una distancia mínima entre detecciones para evitar múltiples identificaciones dentro de un mismo latido.

A partir de los máximos y mínimos detectados se calcula la amplitud de pulso (PPGA) y el intervalo entre latidos (HBI), los cuales son utilizados para estimar el índice SPI. La normalización de estas variables se realiza con base en los primeros 40 segundos de señal, correspondientes a la fase de reposo, estableciendo así una referencia basal para el análisis del experimento.

El sistema genera visualizaciones en tiempo real de la señal, los puntos detectados y la evolución del SPI, además de un análisis final por etapas.
### Visualización de los resultados experimentales
<img width="1091" height="663" alt="image" src="https://github.com/user-attachments/assets/63ef710e-3321-417f-9801-a089e66fbcf7" />
<img width="1080" height="657" alt="image" src="https://github.com/user-attachments/assets/b9d671aa-32f8-4333-9b47-aca55655db4b" />

Las gráficas obtenidas permiten visualizar de manera clara el comportamiento de la señal fotopletismográfica y las variables derivadas a lo largo del experimento. En la primera gráfica se presenta la señal PPG en tiempo real, donde se observa tanto la señal original como su versión suavizada. Esta señal muestra un comportamiento periódico característico de los ciclos cardíacos, evidenciando la presencia de pulsos bien definidos. Sobre esta misma gráfica se indican los máximos mediante triángulos rojos y los mínimos mediante triángulos verdes, los cuales corresponden a los puntos utilizados para el cálculo de las variables fisiológicas.

En la segunda gráfica se muestra la amplitud del pulso (PPGA) en función del tiempo. Cada punto representa la diferencia entre un máximo y un mínimo asociados a un latido, lo que permite observar cómo varía la intensidad del pulso a lo largo de las diferentes etapas del experimento.

La tercera gráfica corresponde al SPI en tiempo real, donde se presenta la evolución del índice calculado a partir de la PPGA y el intervalo entre latidos. En esta gráfica se identifican claramente las tres fases del experimento: reposo, aplicación del Cold Pressor Test (CPT) y recuperación, las cuales están delimitadas por líneas verticales.

#  ANÁLISIS DE RESULTADOS
A partir de las gráficas obtenidas se evidencia que la señal fotopletismográfica fue adquirida de manera adecuada, presentando un comportamiento periódico característico de los ciclos cardíacos. No obstante, el principal inconveniente del sistema se encuentra en la etapa de procesamiento, específicamente en la detección de los mínimos (valles) de la señal.

En las gráficas se observa que la cantidad de máximos detectados es mayor que la de mínimos, lo cual indica un fallo en la identificación correcta de los valles. Este problema se debe a las limitaciones del método del alpinista, el cual es sensible a pequeñas variaciones de la señal y al ruido residual, provocando que algunos mínimos no sean detectados o sean ubicados incorrectamente. Como consecuencia, no existe una correspondencia adecuada entre cada pico y su valle asociado.

Debido a este error, el cálculo de la amplitud de pulso (PPGA), que depende directamente de la diferencia entre máximos y mínimos, se ve afectado, generando valores inconsistentes. A su vez, estos errores se propagan en el cálculo del SPI, produciendo un comportamiento irregular del índice a lo largo del tiempo, sin reflejar de manera clara las fases del experimento.

En condiciones ideales, la señal debería mostrar una relación consistente de un máximo y un mínimo por cada ciclo cardíaco, es decir, un patrón repetitivo donde cada pico esté precedido y seguido por un valle bien definido. Esto permitiría calcular una amplitud de pulso estable y coherente. Asimismo, el SPI debería presentar un comportamiento más organizado, manteniéndose relativamente bajo y estable en reposo, aumentando durante la aplicación del Cold Pressor Test debido a la activación del sistema simpático, y disminuyendo nuevamente durante la fase de recuperación.

Finalmente, en la gráfica de la señal completa se visualiza toda la señal adquirida durante el experimento junto con los máximos y mínimos detectados, permitiendo observar la distribución de estos puntos a lo largo del tiempo. Asimismo, la gráfica final del SPI en función del tiempo resume el comportamiento del índice durante todo el experimento, mostrando su variación en cada una de las etapas establecidas.

## Comparación con valores clínicos del SPI

En el contexto clínico, el SPI se utiliza durante procedimientos quirúrgicos para evaluar el balance entre nocicepción y analgesia, manteniéndose típicamente en un rango aproximado de 20 a 50 cuando existe un adecuado nivel de anestesia. Valores superiores indican una mayor activación del sistema simpático, asociada a estímulos dolorosos o insuficiente analgesia.

En la práctica desarrollada, los valores obtenidos de SPI presentan una dispersión considerable, alcanzando en algunos casos valores elevados cercanos a 100 y en otros valores bajos sin una relación clara con las fases del experimento. Esto difiere del comportamiento esperado en un entorno clínico, donde el índice suele ser más estable y responde de manera controlada a los estímulos. Esta diferencia se debe a que el sistema implementado es una aproximación simplificada que no incluye los modelos avanzados ni los algoritmos propietarios utilizados en equipos médicos reales.

## Evaluación del alcance y limitaciones del sistema

El sistema desarrollado permite evidenciar de manera cualitativa la relación entre la señal fotopletismográfica y la actividad cardiovascular, así como implementar un índice que intenta representar la respuesta fisiológica ante un estímulo nociceptivo. Esto demuestra que es posible utilizar sensores ópticos de bajo costo y técnicas básicas de procesamiento para aproximar el comportamiento del SPI.

No obstante, el sistema presenta varias limitaciones importantes. En primer lugar, la detección de máximos y mínimos mediante el método del alpinista no es completamente robusta frente al ruido y las variaciones de la señal, lo que genera errores en el cálculo de la amplitud de pulso. En segundo lugar, la normalización empleada depende fuertemente de la fase de calibración inicial, por lo que cualquier variación en esta etapa afecta el resultado global. Adicionalmente, factores como el movimiento del dedo, la presión sobre el sensor y la perfusión periférica influyen directamente en la calidad de la señal adquirida.

Por otra parte, el SPI implementado en este sistema no corresponde al índice clínico real, ya que este último se basa en modelos más complejos y en la integración de múltiples variables fisiológicas. Por esta razón, el sistema no debe considerarse como una herramienta precisa para cuantificar el dolor, sino como una aproximación experimental que permite observar tendencias generales.
