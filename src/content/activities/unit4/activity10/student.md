#### Actividad 10

[Link a p5](https://editor.p5js.org/MichaelZapataA/sketches/vrPZ7SJ7d)

```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

// Pendulum

// A simple pendulum simulation
// Given a pendulum with an angle theta (0 being the pendulum at rest) and a radius r
// we can use sine to calculate the angular component of the gravitational force.

// Gravity Force = Mass * Gravitational Constant;
// Pendulum Force = Gravity Force * sine(theta)
// Angular Acceleration = Pendulum Force / Mass = gravitational acceleration * sine(theta);

// Note this is an ideal world scenario with no tension in the
// pendulum arm, a more realistic formula might be:
// Angular Acceleration = (g / R) * sine(theta)

// For a more substantial explanation, visit:
// http://www.myphysicslab.com/pendulum1.html
let pendulum;
let pendulum2;

function setup() {
  createCanvas(640, 240);
  // Make a new Pendulum with an origin position and armlength
  pendulum = new Pendulum(width / 2, 0, 100);
  pendulum2 = new Pendulum(pendulum.bob.x, pendulum.bob.y, 100);
}

function draw() {
  background(255);
  pendulum.update();
  pendulum2.pivot.set(pendulum.bob);
  pendulum2.update();
  
  
  pendulum.show();
  pendulum2.show();
  
  
  pendulum.drag(); // for user interaction
  pendulum2.drag();
}

function mousePressed() {
  pendulum.clicked(mouseX, mouseY);
  pendulum2.clicked(mouseX, mouseY);

}

function mouseReleased() {
  pendulum.stopDragging();  
  pendulum2.stopDragging();

}

```

![img](../../../../assets/unit4/act10.png)
