#### Actividad 4

1. ¿Cómo se gestiona la creación y la desaparición de las partículas y cómo se gestiona la memoria?

    > La creación y destrucción de las partículas se maneja con un tiempo de vida asignado a cada partícula al momento de crearse y que se reduce en cada frame, revisando la validez de ese dato o por decirlo "su vida" se revisa cuando su valor de tiempo se agota y se elimina la partícula, así gastando siempre un valor fijo de elementos y no saturando la memoria del programa, ya que no se dejan las particulas existiendo ni se genera un array de un tamaño infinito que aumenta con cada frame.

2. ¿Cómo se aplica el marco de movimiento motion 101 en los sistemas de partículas que analizaste en la actividad anterior?

    > En el metodo update() de la clase particle, se añade la aceleración a la velocidad y luego la velocidad a la posición, luego se reduce el tiempo de vida y se reinicia la aceleración, a lo largo del código no vemos a función update de particle porque se llama desde el la función run, esto hace el código más  limpio. Además, las fuerzas adicionales se le van agregando a la aceleración con la función applyForce().

3. ¿Cómo se aplican fuerzas externas a los sistemas de partículas que trabajaste en la unidad? ¿Qué fuerzas se aplicaron y cómo están modeladas?

    > Como dije antes, las fuerzas externas se lee suman a la aceleración en su debido momento con applyForce, depende de los ejemplos se aplican diferentes fuerzas, gravedad, fricción, viento, repulsión, etc.

4. ¿Cómo se aplicaste los conceptos de herencia y polimorfismo en los sistemas de partículas que trabajaste en la unidad?

    > Creé una clase partícula general y de ahí extendí los diferentes tipos de partículas, editando en cada caso la función display(), haciendo que cada tipo de partícula aunque en raiz funcionan igual, se ven de forma diferente.

