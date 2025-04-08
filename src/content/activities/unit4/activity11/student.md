#### Actividad 11

Después de ver y pensar que podría hacer con lo que vimos en la unidad, y luego de hacer 1000 walk cycles y ver algunos ejemplos como [este en youtube](https://www.youtube.com/watch?v=XXx0vYGDKiw).

Quiero intentar hacer algo similar a ese y hacer un walk cycle procedural con movimientos sinusoidales.

Vamos a ver que sale, en principio debo plantear 2 particulas que se muevan en horizontal para simular ambos pies y una particula con un movimiento rectilineo o quizá una onda un poco menos marcada para generar la cadera.

Luego debo aprender como simular un brazo (o pierna en este caso) en IK, para poder generar la rodilla y conectar las particulas de los pies con la de la cadera.

---

##### Actualización

Estudié [este código](https://editor.p5js.org/rjgilmour/sketches/2xTLrNAlp) para aprender como funciona el IK.

---

##### Actualización 2

Recibí mucha información y estoy un poco saturado pero vi muchos videos que explicaban

https://www.youtube.com/watch?v=SJyo4z53iUc

https://www.youtube.com/watch?v=V-Lre03F1Ls

https://www.youtube.com/watch?v=IKOGwoJ2HLk&t=309s

Este no tenía mucho que ver pero estaba muy interesante entonces lo vi

https://www.youtube.com/watch?v=GXh0Vxg7AnQ

---

##### Actualización 3

Me rendí con la animación procedural pero logré algo similar, logré generar una particula que gira gracias a curvas sinusoidales, generando un movimiento similar al que hacen los pies al moverse, y con ayuda del sistema IK que mencioné antes, generé piernas para la animación.

Llegué a [este código](https://editor.p5js.org/MichaelZapataA/sketches/4c19GGP_U) de forma arcaica con un código mal planteado buscando un resultado pero luego le pedí a chatGPT que me refactorizara y modulara el código

```js
let armature = {
  x: 200, 
  y: 180,
  l: 80
}

let target = {
  x: 250,
  y: 200
}


let d = 150;


let x = 0;
let y2 = 0;
let x3 = 100;
let y4 = 100;
let waveAmplitude = 40;
let waveFrequency = -0.05;

function setup() {
  createCanvas(600, 400);
  
  rectMode(CENTER)
  imageMode(CENTER)
}

function draw() {
  armature.x = 150;
  background(220);

  // Calcular la posición vertical con la función seno
  let y = armature.y + 115 + sin(x * waveFrequency) * waveAmplitude;
  let x2 = armature.x + 20 + cos(y2 * waveFrequency) * waveAmplitude;
  
    // Calcular la posición vertical con la función seno
  let y3 = armature.y + 110 + sin(x3 * waveFrequency) * waveAmplitude;
  let x4 = armature.x + 20 + cos(y4 * waveFrequency) * waveAmplitude;
  
  // Avanzar horizontalmente
  x += 2;
  y2 += 2;
  
  x3 += 2;
  y4 += 2;
  
  
  
  target.x = x2;
  target.y = y;
  
  d = min(armature.l*2, dist(armature.x, armature.y, target.x, target.y) )
  
  translate(armature.x, armature.y)
  let dy = target.y - armature.y;
  let dx = target.x - armature.x;
  let th = atan2(dy, dx)
  rotate(th)
  
  let h = sqrt(armature.l**2 - (d/2)**2)
  
   // Draw arm with rectangles
  push()
    translate(d/2/2, h/2)
    rotate(atan2(h, d/2))
    rect(0, 0, armature.l, 15)
  pop()
  push()
    translate(d, 0)
    translate(-d/2/2, h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, armature.l, 15)
    rotate(atan2(h, d/2))
    translate(d/2/2, -h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, 25, 25)
  pop()
 
  push()
    translate(d/2/2, h/2)
    rotate(atan2(h, d/2))
    rect(0, 0, armature.l, 15)
  pop()
  push()
    translate(d, 0)
    translate(-d/2/2, h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, armature.l, 15)
    rotate(atan2(h, d/2))
    translate(d/2/2, -h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, 25, 25)
  pop()
  
  resetMatrix()
  
  target.x = x4;
  target.y = y3;
  
  d = min(armature.l*2, dist(armature.x, armature.y, target.x, target.y) )
  
  translate(armature.x, armature.y)
  dy = target.y - armature.y;
  dx = target.x - armature.x;
  th = atan2(dy, dx)
  rotate(th)
  
  h = sqrt(armature.l**2 - (d/2)**2)
  
   // Draw arm with rectangles
  push()
    translate(d/2/2, h/2)
    rotate(atan2(h, d/2))
    rect(0, 0, armature.l, 15)
  pop()
  push()
    translate(d, 0)
    translate(-d/2/2, h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, armature.l, 15)
    rotate(atan2(h, d/2))
    translate(d/2/2, -h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, 25, 25)
  pop()
  
  push()
    translate(d/2/2, h/2)
    rotate(atan2(h, d/2))
    rect(0, 0, armature.l, 15)
  pop()
  push()
    translate(d, 0)
    translate(-d/2/2, h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, armature.l, 15)
    rotate(atan2(h, d/2))
    translate(d/2/2, -h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, 25, 25)
  pop()
  
  
  armature.x = 350;
  
  // Calcular la posición vertical con la función seno
  y = armature.y + 115 + sin(x * waveFrequency) * waveAmplitude;
  x2 = armature.x + 20 + cos(y2 * waveFrequency) * waveAmplitude;
  
    // Calcular la posición vertical con la función seno
  y3 = armature.y + 110 + sin(x3 * waveFrequency) * waveAmplitude;
  x4 = armature.x + 20 + cos(y4 * waveFrequency) * waveAmplitude;

  // Dibujar la partícula
  fill(150, 100, 255);
  noStroke();
  ellipse(x2, y, 20, 20);
  ellipse(x4, y3, 20, 20);
  
  // Avanzar horizontalmente
  x += 2;
  y2 += 2;
  
  x3 += 2;
  y4 += 2;
  
  
  
  target.x = x2;
  target.y = y;
  
  d = min(armature.l*2, dist(armature.x, armature.y, target.x, target.y) )
  
  translate(armature.x, armature.y)
  dy = target.y - armature.y;
  dx = target.x - armature.x;
  th = atan2(dy, dx)
  rotate(th)
  
  h = sqrt(armature.l**2 - (d/2)**2)
  
   // Draw arm with rectangles
  push()
    translate(d/2/2, h/2)
    rotate(atan2(h, d/2))
    rect(0, 0, armature.l, 15)
  pop()
  push()
    translate(d, 0)
    translate(-d/2/2, h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, armature.l, 15)
    rotate(atan2(h, d/2))
    translate(d/2/2, -h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, 25, 25)
  pop()
 
  push()
    translate(d/2/2, h/2)
    rotate(atan2(h, d/2))
    rect(0, 0, armature.l, 15)
  pop()
  push()
    translate(d, 0)
    translate(-d/2/2, h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, armature.l, 15)
    rotate(atan2(h, d/2))
    translate(d/2/2, -h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, 25, 25)
  pop()
  
  resetMatrix()
  
  target.x = x4;
  target.y = y3;
  
  d = min(armature.l*2, dist(armature.x, armature.y, target.x, target.y) )
  
  translate(armature.x, armature.y)
  dy = target.y - armature.y;
  dx = target.x - armature.x;
  th = atan2(dy, dx)
  rotate(th)
  
  h = sqrt(armature.l**2 - (d/2)**2)
  
   // Draw arm with rectangles
  push()
    translate(d/2/2, h/2)
    rotate(atan2(h, d/2))
    rect(0, 0, armature.l, 15)
  pop()
  push()
    translate(d, 0)
    translate(-d/2/2, h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, armature.l, 15)
    rotate(atan2(h, d/2))
    translate(d/2/2, -h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, 25, 25)
  pop()
  
  push()
    translate(d/2/2, h/2)
    rotate(atan2(h, d/2))
    rect(0, 0, armature.l, 15)
  pop()
  push()
    translate(d, 0)
    translate(-d/2/2, h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, armature.l, 15)
    rotate(atan2(h, d/2))
    translate(d/2/2, -h/2)
    rotate(-atan2(h, d/2))
    rect(0, 0, 25, 25)
  pop()
  
  
}
```

Luego llegué a [este con la refactorización de chatGPT](https://editor.p5js.org/MichaelZapataA/sketches/jQ5AqE921) y correcciones propias.

```js
let cabeza;

function preload() {
  cabeza = loadImage('cabezaCaballo2.png');
}


let armature = {
  y: 180,
  l: 80
};

let waveAmplitude = 40;
let waveFrequency = -0.05;

let angleOffset = 0;

let x = 0;
let y2 = 0;
let x3 = 100;
let y4 = 100;

let baseY = 180;        // Altura base del cuerpo
let bobTime = 0;        // Control de tiempo para el movimiento vertical
let bobAmplitude = 10;  // Qué tanto sube y baja
let bobSpeed = waveFrequency * 2; // Velocidad del rebote

function setup() {
  createCanvas(600, 400);
  rectMode(CENTER);
  imageMode(CENTER);
}

function draw() {
  background(220);

  // Suelo
  fill(0, 111, 57);
  rect(0, 612, width * 2, 510);

  // Actualizar la altura del cuerpo con función seno
  bobTime += bobSpeed;
  armature.y = baseY + sin(bobTime) * bobAmplitude;

  // Cuerpo
  fill(187, 111, 57);

  rect(width / 2, armature.y, 210, 20);

  // Avanzar en el tiempo para el movimiento ondulatorio de las piernas
  x += 2;
  y2 += 2;
  x3 += 2;
  y4 += 2;

  // Dibujar múltiples pares de piernas
  drawDoubleLeg(200, x, y2, x3, y4);
  drawDoubleLeg(400, x + 150, y2 + 30, x3 + 150, y4 + 30);

  // Cola y cuello
  drawTail(width / 2 + 100, armature.y);
  drawNeck(width / 2 - 100, armature.y);
}

function drawDoubleLeg(armatureX, x, y2, x3, y4) {
  let armatureY = armature.y;

  // Calcular las posiciones de las partículas con función seno
  let y = armatureY + 115 + sin(x * waveFrequency) * waveAmplitude;
  let x2 = armatureX + 20 + cos(y2 * waveFrequency) * waveAmplitude;

  let y3 = armatureY + 110 + sin(x3 * waveFrequency) * waveAmplitude;
  let x4 = armatureX + 20 + cos(y4 * waveFrequency) * waveAmplitude;

  // Dibujar las partículas
  fill(187, 111, 57);
  noStroke();

  // DIBUJAR PRIMERA PIERNA
  drawArm(armatureX, armatureY, x2, y);

  // DIBUJAR SEGUNDA PIERNA
  drawArm(armatureX, armatureY, x4, y3);
}

function drawArm(x0, y0, x1, y1) {
  let l = armature.l;
  let d = min(l * 2, dist(x0, y0, x1, y1));
  let dx = x1 - x0;
  let dy = y1 - y0;
  let th = atan2(dy, dx);
  let h = sqrt(l ** 2 - (d / 2) ** 2);

  push();
  translate(x0, y0);
  rotate(th);

  // Parte superior
  push();
  translate(d / 4, h / 2);
  rotate(atan2(h, d / 2));
  rect(0, 0, l, 15);
  pop();

  // Parte inferior
  push();
  translate(d, 0);
  translate(-d / 4, h / 2);
  rotate(-atan2(h, d / 2));
  rect(0, 0, l, 15);

  // Pie o punto final
  rotate(atan2(h, d / 2));
  translate(d / 4, -h / 2);
  rotate(-atan2(h, d / 2));
  rect(0, 0, 25, 25);
  pop();

  pop();
}

function drawTail(x, y) {
  push();
  translate(x, y);

  noFill();
  stroke(187, 111, 57);
  strokeWeight(20);

  beginShape();
  for (let i = 0; i < 10; i++) {
    let offset = sin(bobTime * 1 + i * 0.5) * 5;
    vertex(i * 10, i * offset/2);
  }
  endShape();

  pop();
}

function drawNeck(x, y) {
  push();
  translate(x, y);
  
  angleOffset += 0.097;
  
  noFill();
  stroke(187, 111, 57);

  strokeWeight(20);

  let neckPoints = [];
  
  beginShape();
  for (let i = 0; i < 4; i++) {
    let px = i * -8;
    let py = - i *10;
    vertex(px, py);
    neckPoints.push(createVector(px, py));
  }
  endShape();

  let end = neckPoints[neckPoints.length - 1];
  rotate((sin(angleOffset) * PI / 30) + PI*1.85); 
  image(cabeza, end.x+5, end.y-40, 100, 130);

  pop();
}

``` 

Le agregué un overlapping de rotación a la cabeza para que no quedara tan tiesa en la animación

[Video de la simulación](https://drive.google.com/file/d/1SzvWx3gaGwtFU9idkwC1wgntQGiyH5IG/view?usp=sharing)


##### Prueba de ver video embed

<iframe src="https://drive.google.com/file/d/1SzvWx3gaGwtFU9idkwC1wgntQGiyH5IG/preview" 
        width="640" 
        height="480" 
        allow="autoplay">
</iframe>
