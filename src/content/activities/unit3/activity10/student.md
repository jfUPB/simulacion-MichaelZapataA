#### Actividad 10

##### Fricción

La fricción es una fuerza que se opone al movimiento de un objeto. En este código:

Se modela un objeto (mover) con velocidad y aceleración.

Se calcula la fricción como un vector opuesto a la dirección de la velocidad, con una magnitud constante (0.02).

Se aplica la fricción al objeto, reduciendo su velocidad gradualmente.

Si el objeto toca los bordes, su velocidad se reduce simulando pérdida de energía.

Visualmente, el objeto es un círculo que se mueve y frena poco a poco debido a la fricción.

[Link a p5 fricción](https://editor.p5js.org/MichaelZapataA/sketches/gecwTwPb1)

##### Resistencia aire

La resistencia del aire se modela como una fuerza proporcional al cuadrado de la velocidad del objeto. En este código:

Se usa la ecuación de resistencia aerodinámica: $F = -c * v²$, donde $c$ es un coeficiente de resistencia.

Se normaliza la dirección de la velocidad y se multiplica por la magnitud de la resistencia.

Se aplica esta fuerza al objeto, reduciendo su velocidad de manera más notoria en velocidades altas.

Se verifica si el objeto está en los límites de la pantalla para evitar que se salga.

Visualmente, el objeto pierde velocidad de manera más brusca en función de su rapidez, simulando resistencia del aire.

[Link a p5 Resistencia Aire](https://editor.p5js.org/MichaelZapataA/sketches/jdRVTNVm_)


##### Gravedad

Se modela la atracción gravitacional entre dos objetos: un atractor (como un planeta) y un mover (como un satélite). En este código:

Se usa la Ley de la Gravitación Universal: F = G * (m1 * m2) / d², donde G es la constante gravitacional.

Se calcula la distancia entre el atractor y el objeto en movimiento.

La fuerza resultante se aplica al objeto, que es atraído hacia el centro del atractor.

Se limita la distancia para evitar efectos extremos en el cálculo.

Visualmente, el objeto es atraído hacia el centro del atractor y orbita alrededor de él, creando un efecto dinámico realista.

[Link a p5 gravedad](https://editor.p5js.org/MichaelZapataA/sketches/PEnm3ht8A)