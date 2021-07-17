### Control de ventilación automática

Debido á situación excepcional vivida nos centros por causa da COVID-19 e ante a ausencia inicial dun protocolo de ventilación das aulas, xurdíu a necesidade de medir parámetros de calidade do aire no interior das aulas e talleres. Como non é posible ter unha medida instantánea da carga vírica nun entorno pechado, en todas as guías e manuais técnicos consultados óptase por correlacionar a calidade do aire en relación coa COVID-19, coa concentración de dióxido de carbono (CO2). Desta maneira, podemos aplicar a [normativa do RITE](https://www.idae.es/uploads/documentos/documentos_17_Guia_tecnica_instalaciones_de_climatizacion_con_equipos_autonomos_5bd3407b.pdf) para cualificar o aire interior como óptimo, aceptable ou tolerable.

A concentración de CO2 mídese en partes por millón (ppm) e os valores establecidos como válidos son:
* Óptimo: concentracións de CO2 equivalentes ao exterior (entre 350 e 450 ppm)
* Aceptable para IAQ (indoor air quality): de 600 a 800 ppm
* Tolerable para IAQ, até un máximo de 1000 ppm.

Decidíuse realizar un medidor portátil que:
1. monitorice permanentemente a concentración de CO2 dunha estancia, e
2. (opcionalmente) encenda un ventilador para a renovación de aire ao superarse un umbral prefixado ou superarse un tempo máximo no umbral anterior.

Para montar o medidor portátil, decidíuse empregar un Arduino UNO no canto dun ESP8266 por non seren necesarias as posibilidades de comunicación WiFi do ESP e adicionalmente por o Arduino UNO ser máis versátil á hora de empregar diferentes fontes de alimentación. Como sensor para a medida da concentración de CO2 empregouse un [MQ-135](https://components101.com/sensors/mq135-gas-sensor-for-air-quality).

![sensor MQ](https://user-images.githubusercontent.com/26594148/126041057-f07063b8-04b9-4581-bdbe-f8fc7d0271ab.jpg)

Os sensores de gases MQ son unha familia de dispositivos deseñados para detectar a presenza de diferentes compoñentes químicos no aire. Existe unha grande variedade de sensores MQ. Cada modelo está deseñado para detectar unha ou máis sustancias gasosas (p.ex. gases inflamábeis, calidade de aire ou detección de álcol en aire respirado). Os sensores MQ comercialízanse normalmente cunha placa de medición estándar que incorpora o comparador LMC662 ou algún similar. Isto permite obter un valor analóxico e taméun un valor dixital. Este último corresponde con un '1' lóxico ao superarse un determinado umbral regulado mediante un potenciómetro ubicado na propia placa. Nós faremos uso da lectura analóxica e empregaremos máis de un umbral, como se indicou nos parágrafos anteriores. Estes sensores de gases deben ser calibrados mediante as súas curvas características antes de obtermos unha medida precisa. Aínda así calibrados, estes sensores non se deben empregar para sistemas industriais con alta demanda de precisión, tempo de operación, seguridade, etc. Aínda así, estes sensores son moi apropipados para o seu uso didáctico na formación de futuros técnicos de instalacións térmicas, refrixeración e climatización.

![mq-series-sensor-mq2-2c-mq3-2c-mq6-2c-mq7-2c-mq135-500x500](https://user-images.githubusercontent.com/26594148/126041147-df1d7258-f0b2-4592-9299-2c260ceaaf33.jpg)


![arduino-sensor-gas-mq-esquema](https://user-images.githubusercontent.com/26594148/126040998-e4de4dc1-acae-4d07-a084-e5f488e654d4.png)

Os sensores da familia MQ están formados por un sensor electro-químico que varía a súa resistencia ao estar en contacto con diversas sustancias gasosas. Son dispoisitivos de alta inercia. É dicir, precisas tempos relativamente largos para estabilizárense tras un cambio na concentración dos gases medidos. Isto é porque se necesita un certo tempo para que o gas abandone o recinto no que se encontra o material sensible e en ocasións leva un certo tempo. Para facilitar o reemplazo do gas, todos os modelos MQ dispoñen dun aquecedor que eleva a temperatura do sensor. Cando o aquecedor acada a temperatura de operación é cando o dispositivo terá a maior fiabilidade. Normalmente esta temperatura acádase aos poucos minutos, sen embargo algúns modelos poden precisar até 12 ou 48 h. Non é o noso caso. Estes sensores precisan dunha tensión duns 5 V para alimentar o aquecedor e algúns modelos poden chegar a consumos de até 800 mV, polo que pode ser recomendable que leven alimentación independente da placa controladora (no noso caso o Arduinon UNO). No noso caso, o MQ-135 precisa dunha alimentación de 5 V e o consumo non nos obriga a alimentalo cunha fonte externa, o que facilita o deseño do medidor portátil.
