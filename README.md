# Laboratorio 2 de señales (problema de la fiesta de cóctel)

El efecto cóctel consiste en enfocar la audición en una sola voz dentro de una habitación llena de personas. La solución de este problema a nivel computacional requiere diferentes mecanismos, como la transformada rápida de Fourier para el análisis en frecuencia de las señales y métodos de separación de fuentes.

Para este propósito, se grabaron dos audios en una sala insonorizada (ruido ambiental y voces), teniendo en cuenta que se utilizaron tres fuentes diferentes, así como tres micrófonos con un sistema de adquisición de señales.

La configuración de la captación de audio se muestra en la siguiente imagen. En este ejercicio, cada fuente dijo una frase diferente al mismo tiempo de grabación.

![image](https://github.com/user-attachments/assets/0214f9f0-8200-4abe-9d2a-77c12ba35f5c)

Los micrófonos se ubicaron a una distancia de 0.5 metros frente a cada fuente y a 1 metro de distancia entre las fuentes, como se muestra en la imagen anterior.

Para la adquisición de la señal, se utilizó el sistema de adquisición de datos llamado Recforge, que es una aplicación móvil para celulares. Esta aplicación permite garantizar la frecuencia de muestreo, el nivel de cuantización y el tiempo de grabación. Para este ejercicio, se utilizó una frecuencia de muestreo de 44 kHz, un nivel de cuantificación de 160 Kbps (kilobits por segundo) y un tiempo de grabación de 5.1 segundos. Estos valores aseguran una buena precisión de la señal digitalizada con respecto a la análoga, lo que permite un análisis más completo y preciso de las señales tanto en el dominio del tiempo como en el de frecuencia.

Continuando de esta manera, con la ayuda de la librería librosa, se subieron los audios a Colab, y con la librería matplotlib, se graficaron cada señal. Estas se pueden observar a continuación.

![image](https://github.com/user-attachments/assets/e210245e-12a6-41bd-8124-1b307d7b3286)

![image](https://github.com/user-attachments/assets/bc67ca0e-c452-4500-ab5d-253e1974b1dc)

![image](https://github.com/user-attachments/assets/d6a36e97-23be-4d52-a832-103a8cf2af69)

Como se visualiza, estas primeras tres señales corresponden al ruido ambiental captado por cada micrófono, teniendo en el eje vertical la amplitud de la señal y en el eje horizontal el tiempo en segundos.

![image](https://github.com/user-attachments/assets/367ed5e3-4b74-4d74-99a1-4801cb3950b2)

![image](https://github.com/user-attachments/assets/7a68e28b-d68f-4ebd-b528-34a085e5e416)

![image](https://github.com/user-attachments/assets/89b60ecf-6fae-4eef-b7b3-2f9d098572f0)

Continuando, estas tres últimas imágenes hacen referencia a la señal cuando las tres fuentes están hablando. De la misma manera que anteriormente, en el eje vertical tenemos la amplitud de la señal y en el eje horizontal el tiempo de la grabación. Es relevante mencionar que la amplitud máxima de estas señales es de 0.075 y la duración es de 5.1 segundos, al igual que el ruido ambiental.

Seguidamente, se realizó un análisis de esta señal respecto al ruido. Este estudio se llama SNR (relación señal-ruido), que, como su nombre lo indica, nos permite determinar la relación de la señal con respecto al ruido. Este análisis se generó para cada micrófono, obteniendo los siguientes resultados:

SNR micrófono 1: 14.80
SNR micrófono 2: 12.31
SNR micrófono 3: 12.51
Para esta práctica de laboratorio, era importante tener un SNR mayor a 10, ya que esto garantiza que el ruido ambiental no interfiera con la caracterización y separación de la señal a estudiar, brindando, además, una amplia confiabilidad en el ejercicio.

Así, el objetivo es descomponer la grabación, en la que hay tres fuentes, dejando una sola para que se escuche con claridad la frase utilizada. Para ello, necesitamos implementar una herramienta matemática como la transformada rápida de Fourier, la cual nos permite pasar del dominio del tiempo al dominio de la frecuencia para determinar las frecuencias dominantes y el ancho de banda. Este análisis permite entender qué componentes frecuenciales están presentes en la señal y cómo se distribuyen, lo cual es útil en diversas aplicaciones, como el procesamiento de voz.

Teniendo esto en cuenta, se muestran las gráficas respectivas donde se evidencia el comportamiento de la señal en el dominio de la frecuencia. Estas se obtuvieron con la ayuda de las librerías scipy y matplotlib para graficar cada una de las transformadas.

![image](https://github.com/user-attachments/assets/6065b022-92ed-47ba-8fbc-f75812de797a)

![image](https://github.com/user-attachments/assets/0af1ad59-bd3f-4781-9b41-380ae988e8c4)

![image](https://github.com/user-attachments/assets/e4bfcb47-e792-4dd9-a05e-742a0c6b7bfe)


Para el análisis espectral de esta señal en el dominio de la frecuencia, es importante entender que solo se evalúa la mitad de la longitud de la señal original, ya que la respuesta en frecuencia es simétrica al tratarse de una señal natural, como la voz humana. Además, cada pico en esta gráfica muestra las frecuencias presentes en la señal original, junto con su respectiva magnitud. En este caso, la frecuencia dominante del sistema es de aproximadamente 2 kHz, con una magnitud de 80.

Finalmente, se utilizaron diversas librerías para la separación de fuentes en las diferentes señales mencionadas. Esto se logró gracias al Análisis de Componentes Independientes (ICA), que busca descomponer una mezcla de señales en sus componentes originales, asumiendo que estas señales son estadísticamente independientes entre sí. Este método se utiliza cuando hay múltiples señales mezcladas (como varias voces en una grabación) y se desea recuperar las fuentes originales.

Adicionalmente, se graficaron las fuentes independientes en el dominio del tiempo para luego descargar los archivos MP3.

[image](https://github.com/user-attachments/assets/fd5edfcd-3d58-4071-b81c-f68b9ba7729c)

En la imagen anterior se visualiza la fuente independiente. En el eje x está representado el dominio del tiempo en milisegundos (ms), y en el eje y se encuentra la amplitud. Esta señal es muy similar a la original captada por los micrófonos. Sin embargo, en esta señal predomina una sola fuente, lo que significa que esta fuente resalta sobre las demás. Aunque se logran escuchar las otras, la relación señal-ruido (SNR) de esta señal fue de 0.20 debido al ruido presente. El programa describe las demás fuentes como ruido ambiental. A pesar de un SNR tan bajo, se logra diferenciar una sola fuente de las demás.

El resultado de la fuente independiente no es de alta resolución, ya que el método utilizado puede verse afectado por la cantidad de muestras de cada señal. Este método requiere un amplio número de muestras, y en este ejercicio fue necesario recortar las señales para que tuvieran la misma longitud. Esto pudo haber favorecido la pérdida de información. Con esto en mente, se pueden implementar algunas mejoras en la metodología del Análisis de Componentes Independientes (ICA) para obtener mejores resultados, tales como:

Configuración del Arreglo de Micrófonos: Un arreglo lineal de tres micrófonos espaciados uniformemente puede mejorar la calidad del resultado. Asegúrate de que los micrófonos estén calibrados y tengan una respuesta de frecuencia similar para evitar sesgos. Además, coloca el arreglo en una posición óptima respecto a las fuentes de sonido para maximizar la separación de señales.

Resolución de Captura: Si la fuente sonora está más cerca del micrófono, se tendrá una mayor resolución frente a los decibeles captados, ya que la onda sonora estará más cercana. Esto reduce la pérdida de información, ya que el sonido se disipa en el aire y, mientras más lejos esté el dispositivo de adquisición de audio, menor será la información captada de la onda sonora.

Distancias entre Fuentes: Si las fuentes están más cerca unas de otras, se presentará mayor distorsión o ruido debido a la interferencia constructiva. En otras palabras, las ondas de cada fuente tienden a sumarse, lo que complica la percepción de las señales originales. Por el contrario, si las fuentes están más alejadas, será más fácil comprender las señales originales de cada foco.
