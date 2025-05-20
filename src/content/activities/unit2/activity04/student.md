#### Actividad 4

- ¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?

<sl>

El metodo ```mag()``` funciona para calcular la magnitud de un vector, es decir, la raiz cuadrada de la suma del cuadrado de sus componetes. El ```magSq()``` calcula el cuadrado de la magnitud, es decir, la suma de los cuadrados de sus componentes, sin sacar la raiz externa.

```magSq()``` es mas eficiente que ```mag()``` ya que evita calcular la raiz cuadrada que siempre es una tarea exigente para la máquina, lo que hace que muchas veces sea mejor comparar asi, por ejemplo

```js
// Eficiente ya que no se calcula la raiz cuadrada,
// sino que se compara ccon el cuadrado del valor,
// siendo este más fácil de calcular

if (v.magSq() < distanciaMaxima * distanciaMaxima) {
}

// Menos eficiente ya que calcula la raiz de mag()

if (v.mag() < distanciaMaxima) {
}
```

<sl>

- ¿Para qué sirve el método normalize()?
<sl>
Normaliza el vector, es decir, genera un nuevo vector donde sus componentes dan una magnitud sea igual a 1, con la misma dirección que el original, sin modificar este. Muy util para usar vectores de dirección.

<sl>

- Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?
<sl>
El método dot() calcula el producto punto entre 2 vectores, es decir, la suma del producto entre cada uno de sus componentes.

<sl>

- El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?
<sl>
La versión de instancia, calcula el producto punto entre la instancia y, bien sea, el vector pasado como argumento o los 3 valores de componentes del vector. Mientras que la versión estática recibe 2 vectores y calcula el producto punto entre ellos, haciendo equivalentes a ```v1.dot(v2);``` y ```p5.Vector.dot(v1, v2);```

<sl>

- Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.
  <sl>
  Si tienes 2 vectores en un espacio 3d, el producto cruz genera un vector nuevo que es perpendicular al plano generado por los dos vectores originales siguiendo la regla de la mano derecha, con su magnitud siendo igual al producto de sus magnitudes multiplicado por el valor absoluto del seno del ángulo generado entre ellos.

<sl>


- ¿Para que te puede servir el método dist()?
  <sl>
  sirve para calcular la distancia entre 2 puntos representados por vectores.

<sl>

- ¿Para qué sirven los métodos normalize() y limit()?
  <sl>
  El metodo normalize() ya lo expliqué antes y el método limit() asegura que un vector no supere una magnitud máxima, generando un nuevo vector con la misma dirección que el original pero con la magnitud del tamaño maximo pasado como argumento en csao de que lo supere, si no lo supera, returna el mismo vector original. Sin embargo, estos métodos no modifican el vector original sino que generan nuevos vectores.