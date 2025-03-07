#### Actividad 5

En el planteamiento hay un problema muy simple, cuando aplicamos la fuerza en la función ```applyForce()```, en realidad se está dando el valor del argumento a la variable fuerza, en vez de sumarse, solo habría que modificarla para que sume en vez de reasignar.

##### Aplicación p5js

[link](https://editor.p5js.org/MichaelZapataA/sketches/lI1DE_w8m)

```js

class Mover {
  constructor() {
    this.position = createVector();
    this.velocity = createVector();
    this.acceleration = createVector();
    this.radius = 10; // Radio del círculo
  }
  applyForce(force) {
  this.acceleration.add(force);
}
  
  motion101() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.set(0, 0); // Resetea la aceleración después de aplicar fuerzas
    
    // **Chequeo de colisión con las paredes**
    if (this.position.x - this.radius < 0 || this.position.x + this.radius > width) {
      this.velocity.x *= -1; // Invertir dirección en X
      this.position.x = constrain(this.position.x, this.radius, width - this.radius); // Evitar que se salga
    }

    if (this.position.y - this.radius < 0 || this.position.y + this.radius > height) {
      this.velocity.y *= -1; // Invertir dirección en Y
      this.position.y = constrain(this.position.y, this.radius, height - this.radius); // Evitar que se salga
    }
  }
}

function setup() {
  createCanvas(400, 400);
  prueba = new Mover();
  prueba.position.set(random(100, width), random(100, height));
  prueba.velocity.set(0,0);
  prueba.acceleration.set(0,0);
  
  //Vectores wind y gravity
  
  centro = createVector(width / 2, height / 2); // Posición inicial para el viento
  
  fuerzaViento = 0.0;
  
  wind = createVector();
  gravity = createVector(0,0.01);
}

function draw() {
  background(220);
  
  wind.set(mouseX - centro.x, mouseY - centro.y); // setear dirección hacia el mouse
  wind.normalize(); // Normaliza el vector para que solo tenga dirección
  wind.mult(fuerzaViento); // Cambiar velocidad 
  
  prueba.applyForce(wind);
  prueba.applyForce(gravity);
  
  // Motion 101
  
  prueba.motion101();
  
  
  circle(prueba.position.x,prueba.position.y,prueba.radius);
  
  
  stroke(255, 0, 0);
  line(centro.x, centro.y, centro.x + wind.x * 1000, centro.y + wind.y * 1000);
}

function mouseClicked() {
  centro.set(mouseX, mouseY);
}

function doubleClicked() {
  fuerzaViento += 0.01;
  fuerzaViento %= 0.02;
}

```


Aqui se aplican ambas fuerzas con la función ```motion101()``` , cambiando el centro del origen del viento con el click y apagando y encendiendo el viento doble click.