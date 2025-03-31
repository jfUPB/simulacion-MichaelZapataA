#### Actividad 2

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
    this.position = createVector(width/2, height/2);
    this.velocity = createVector(0, 0);
  }

  show() {
    stroke(0);
    this.position.add(this.velocity)
    point(this.position);
    this.velocity.x = 0;
    this.velocity.y = 0;
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.velocity.x = 1;
    } else if (choice == 1) {
      this.velocity.x = -1;
    } else if (choice == 2) {
      this.velocity.y = 1;
    } else {
      this.velocity.y = -1;
    }
  }
}

```


Realicé el cambio de las variables de posición por un vector con las coordenadas del punto y un vector de velocidad que es el que afecta el movimiento respecto a la función ```step();```.
