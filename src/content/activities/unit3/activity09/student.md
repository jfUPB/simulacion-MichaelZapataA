#### Actividad 9

Para modelar una fuerza en una simulación hay que seguir lo siguientes pasos:

1. Entender el concepto detrás de la fuerza
2. Deconstruir la fuerza en 2 partes:
   1. Como puedo calcular la dirección de la fuerza?
   2. Como puedo calcular la magnitud de la fuerza?
3. Adaptar esas formulas a código de p5.js para calcular cual es el vector que se le va a pasar al objeto

Por ejemplo, una fuerza facil de calcular es la fuerza de gravedad:

1. Es una fuerza que atrae los objetos cercanos al centro de el objeto que ejerce la fuerza, en el planeta por ejemplo, nos atrae hacia abajo
2. Deconstruir en dirección y magnitud:
   1. La dirección es hacia abajo constantemente ya que no es una fuerza que esté cambiando
   2. La magnitud de la gravedad en la tierra es de aproximadamente $9.8 m/s^2$
3. Para adaptar la gravedad a p5.js, hay que calcular el vector que sería [0, 9.8], ya que es una fuerza que descompuesta no ejerce movimiento horizontal y el valor en $y$ debe ser positivo ya que en p5.js, el origen [0,0] está en la esquina superior izquierda, por lo que hacia abajo, es mayor el valor de $y.$