# Laboratorio 2 de señales (problema de la fiesta de cóctel)

El efecto cóctel consiste en enfocar la audición en una sola voz dentro de una habitación llena de personas. La solución de este problema a nivel computacional requiere diferentes mecanismos, como la transformada rápida de Fourier para el análisis en frecuencia de las señales y métodos de separación de fuentes.

Para este propósito, se grabaron dos audios en una sala insonorizada (ruido ambiental y voces), teniendo en cuenta que se utilizaron tres fuentes diferentes, así como tres micrófonos con un sistema de adquisición de señales.

La configuración de la captación de audio se muestra en la siguiente imagen. En este ejercicio, cada fuente dijo una frase diferente al mismo tiempo de grabación.

[imagen]

Los micrófonos se ubicaron a una distancia de 0.5 metros frente a cada fuente y a 1 metro de distancia entre las fuentes, como se muestra en la imagen anterior.

Para la adquisición de la señal, se utilizó el sistema de adquisición de datos llamado Recforge, que es una aplicación móvil para celulares. Esta aplicación permite garantizar la frecuencia de muestreo, el nivel de cuantización y el tiempo de grabación. Para este ejercicio, se utilizó una frecuencia de muestreo de 44 kHz, un nivel de cuantificación de 160 Kbps (kilobits por segundo) y un tiempo de grabación de 5.1 segundos. Estos valores aseguran una buena precisión de la señal digitalizada con respecto a la análoga, lo que permite un análisis más completo y preciso de las señales tanto en el dominio del tiempo como en el de frecuencia.

Continuando de esta manera, con la ayuda de la librería librosa, se subieron los audios a Colab, y con la librería matplotlib, se graficaron cada señal. Estas se pueden observar a continuación.

[imagen]

Como se visualiza, estas primeras tres señales corresponden al ruido ambiental captado por cada micrófono, teniendo en el eje vertical la amplitud de la señal y en el eje horizontal el tiempo en segundos.

[imagen]

Continuando, estas tres últimas imágenes hacen referencia a la señal cuando las tres fuentes están hablando. De la misma manera que anteriormente, en el eje vertical tenemos la amplitud de la señal y en el eje horizontal el tiempo de la grabación. Es relevante mencionar que la amplitud máxima de estas señales es de 0.075 y la duración es de 5.1 segundos, al igual que el ruido ambiental.

Seguidamente, se realizó un análisis de esta señal respecto al ruido. Este estudio se llama SNR (relación señal-ruido), que, como su nombre lo indica, nos permite determinar la relación de la señal con respecto al ruido. Este análisis se generó para cada micrófono, obteniendo los siguientes resultados:

SNR micrófono 1: 14.80
SNR micrófono 2: 12.31
SNR micrófono 3: 12.51
Para esta práctica de laboratorio, era importante tener un SNR mayor a 10, ya que esto garantiza que el ruido ambiental no interfiera con la caracterización y separación de la señal a estudiar, brindando, además, una amplia confiabilidad en el ejercicio.

Así, el objetivo es descomponer la grabación, en la que hay tres fuentes, dejando una sola para que se escuche con claridad la frase utilizada. Para ello, necesitamos implementar una herramienta matemática como la transformada rápida de Fourier, la cual nos permite pasar del dominio del tiempo al dominio de la frecuencia para determinar las frecuencias dominantes y el ancho de banda. Este análisis permite entender qué componentes frecuenciales están presentes en la señal y cómo se distribuyen, lo cual es útil en diversas aplicaciones, como el procesamiento de voz.

Teniendo esto en cuenta, se muestran las gráficas respectivas donde se evidencia el comportamiento de la señal en el dominio de la frecuencia. Estas se obtuvieron con la ayuda de las librerías scipy y matplotlib para graficar cada una de las transformadas.

[imagen]

Para el análisis espectral de esta señal en el dominio de la frecuencia, es importante entender que solo se evalúa la mitad de la longitud de la señal original, ya que la respuesta en frecuencia es simétrica al tratarse de una señal natural, como la voz humana. Además, cada pico en esta gráfica muestra las frecuencias presentes en la señal original, junto con su respectiva magnitud. En este caso, la frecuencia dominante del sistema es de aproximadamente 2 kHz, con una magnitud de 80.

Finalmente, se utilizaron diversas librerías para la separación de fuentes en las diferentes señales mencionadas. Esto se logró gracias al Análisis de Componentes Independientes (ICA), que busca descomponer una mezcla de señales en sus componentes originales, asumiendo que estas señales son estadísticamente independientes entre sí. Este método se utiliza cuando hay múltiples señales mezcladas (como varias voces en una grabación) y se desea recuperar las fuentes originales.

Adicionalmente, se graficaron las fuentes independientes en el dominio del tiempo para luego descargar los archivos MP3, donde predomina una sola fuente. Esto significa que una fuente sobresale respecto a las demás, aunque aún se puedan escuchar las otras. Sin embargo, se observó una modificación en el audio, es decir, el tiempo cambia y se distorsiona, lo que hace que la fuente predominante se escuche de manera incorrecta. Este fenómeno podría deberse a cortes y una falta de precisión en la alineación de los audios, ya que el análisis de componentes independientes se realiza con matrices que deben tener la misma cantidad de columnas. Al igualar dichas columnas, se genera una adaptación errónea de los datos, y cuanto mayor sea la diferencia de estos, mayor será la distorsión.

Siguiendo esta idea, en relación con los posibles errores, es importante mencionar que si la fuente sonora está más cerca del micrófono, tendrá una mayor resolución respecto a los decibeles captados, ya que la onda sonora estará más cerca. Por lo tanto, la pérdida de información será menor, dado que el sonido se disipa en el aire, lo que significa que cuanto más lejos esté el dispositivo de adquisición de audio, menos información de la onda sonora captará. De igual manera, las distancias entre las fuentes también influyen: cuanto más cerca estén las fuentes, mayor será la distorsión o el ruido, ya que habrá una mayor interferencia constructiva. En otras palabras, las ondas de cada fuente tienden a sumarse, lo que complica la percepción de las señales originales. Por otro lado, si las fuentes están más alejadas, será más fácil comprender las señales originales de cada foco.



