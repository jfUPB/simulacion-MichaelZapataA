#### Actividad 6

```js
let posicion = 0.5;
let vel = 0.008;

let from = 'red'
let to = 'blue'



function setup() {
    createCanvas(400, 400);
}

function draw() {
    background(200);

    let v0 = createVector(mouseX, mouseY);
    let v1 = createVector(width -10 - mouseX, 0);
    let v2 = createVector(0, height - mouseY -10);
    let v3 = p5.Vector.lerp(v1, v2, posicion);
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, lerpColor(from, to, posicion));
    drawArrow(p5.Vector.add(v0,v1), v2.sub(v1), 'green');
    if (posicion <=0){vel = vel*-1;}
    else if (posicion>=1){vel = vel*-1} 
    posicion += vel;
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```
![Resultado](../../../../assets/unit2/act6_resultado.gif)

Para solucionar el problema, cambié las constantes que había antes como valores de los vectores por los valores en X y Y del mouse, de la forma que se requiriera en el caso. asignando la base al mouse y una escala relativa al mouse con 10 pixeles de distancia hasta el borde, con la formula ```height - mouseY - 10```, por ejemplificar.