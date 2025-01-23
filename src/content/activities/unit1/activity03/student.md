#### Actividad 3

Es un código simple, donde se le da una dirección al movimiento de un punto que inicia en el medio del canvas y se desplaza en alguna dirección generando una línea de forma aleatoria.

Quiero probar aumentando las probabilidades de la línea, haciendo más probable su movimiento hacia abajo y la derecha, también quiero probar hacer la más gruesa o delgada.

Espero que la línea crezca su tamaño, pero también espero que en algunas ocasiones incluso desaparezca la línea y que a pesar de sus probabilidades de ir hacia abajo y derecha, no sea una línea diagonal y algunas veces incluso se regrese.

---
##### Código

```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    this.size = 1;
  }

  show() {
    stroke(0);
    strokeWeight(this.size);
    point(this.x, this.y);
  }

  step() {
    const choice = floor(random(12));
    if (choice < 4) {
      this.x++;
    } else if (choice < 5) {
      this.x--;
    } else if (choice < 9) {
      this.y++;
    } else if (choice < 10){
      this.y--;
    } else if (choice < 11){
      this.size++;
    } else {
      this.size--;
    }
    
  }
}

```
---
##### Resultados
![resultado1](/src/assets/unit1/act3_1.png)
> En este resultado podemos ver que la línea desapareció en algunos momentos, sin embargo, era relativamente continua con algunos picos hacia la izquierda.

![resultado2](/src/assets/unit1/act3_2.png)
> Aquí podemos ver que la línea casi desapareció en todo el camino.

![resultado3](/src/assets/unit1/act3_3.png)
> En cambio, con esta se observa como la línea desapareció en la mitad del trayecto y luego empezó a engrosar.

![resultado4](/src/assets/unit1/act3_4.png)
> Para terminar con este resultado donde la línea tuvo un crecimiento más o menos constante, con solo algunas perdidas de tamaño y desapariciones en su trayecto

> [!NOTE]
> Es interesante como a pesar de ser el mismo código ejecutado diferentes veces, la aleatoriedad ocasiona que sean resultados en esencia diferentes, algunos otorgando mucha información del movimiento de la línea y otros simplemente mostrando pequeños fragmentos de su viaje.

---

