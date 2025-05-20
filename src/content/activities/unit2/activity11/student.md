#### Actividad 11

Después de mucha prueba y error, pude llegar al resultado deseado

##### [Link a P5JS](https://editor.p5js.org/MichaelZapataA/sketches/ggA4nyQF_)

![Resultado](../../../../assets/unit2/act11_resultado.gif)


##### Código

###### sketch.js

```js
let shaderTry

let pos;
let vel;

function preload() {
  shaderTry = loadShader('shader.vert', 'shader.frag');
}


function setup() {
  createCanvas(600, 600, WEBGL);
  
  shader(shaderTry);
  
  noStroke();
  
  shaderTry.setUniform('iResolution', [width, height]);
  pos = createVector(0, 0, 0);
  vel = createVector(.05,.05,.05);
  acc = createVector(0,0,0);
  
}

function draw() {
  pos.add(vel);
  vel.add(acc);
  
 
  shaderTry.setUniform('iMouse', [mouseX, mouseY]);
  shaderTry.setUniform('iTime', millis()/1000.);
  shaderTry.setUniform('posiBola', [pos.x, pos.y, pos.z]);
  
  clear();
  //Rectangulo de shader
  rect(0, 0, width, height);
  
  if (pos.x > 2 || pos.x < -2) {
    vel.x *= -1;
  }
  if (pos.y > 2 || pos.y < -2) {
    vel.y *= -1;
  }
  if (pos.z > 1 || pos.z < -1) {
    vel.z *= -1;
  }
  
}

function keyPressed() {
  if (keyCode === LEFT_ARROW) {
    acc.sub(createVector(.01,.01,.01));
  } else if (keyCode === RIGHT_ARROW) {
    acc.add(createVector(.01,.01,.01));
  } else if(keyCode === DOWN_ARROW){
    vel.sub(vel);
    acc.sub(acc);
  }else if(keyCode === UP_ARROW){
    vel = createVector(.05,.05,.05);
    acc = createVector(0,0,0);
  } else if(keyCode === 32){
    pos = createVector(0, 0, 0);
    vel = createVector(.05,.05,.05);
    acc = createVector(0,0,0);
  }
  // Uncomment to prevent any default behavior.
  // return false;
}
```

---
En este caso el .js no hace mucho más que la implementación del motion 101 y encargarse de los inputs, pero a grandes rasgos lo único que hace es enviarle algunas variables que cambian al .frag.

---

###### Shader.vert

```cs
attribute vec3 aPosition;
attribute vec2 aTexCoord;

varying vec2 pos;

void main() {
  pos = aTexCoord;
  
  
  vec4 position = vec4(aPosition, 1.0);
  position.xy = position.xy * 2. - 1.;
  
  gl_Position = position;
}
```

---
Este es el código más simple donde solo se mapean las coordenadas y se le pasan al .frag que es el que hace la magia

---

###### Shader.frag

```cs
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 iResolution;
uniform float iTime;
uniform vec2 iMouse;
uniform vec3 posiBola;

//Funciones generales
float smin(float a, float b, float k){
  float h = max( k-abs(a-b), 0.)/k;
  return min(a, b) - h*h*h*k*(1./6.);
}

mat2 rot2D(float angle){
  float s = sin(angle);
  float c = cos(angle);
  return mat2(c, -s, s, c);
}

// Función de paleta de colores
vec3 palette(float t) {
    vec3 a = vec3(0.5, 0.5, 0.5);
    vec3 b = vec3(0.5, 0.5, 0.5);
    vec3 c = vec3(1.0, 1.0, 1.0);
    vec3 d = vec3(0.263, 0.416, 0.557);

    return a + b * cos(6.28318 * (c * t + d));
}

//Figuras
float sdOctahedron( vec3 p, float s)
{
  p = abs(p);
  return (p.x+p.y+p.z-s)*0.57735027;
}


float sdSphere(vec3 p, float s){
  return length(p) - s;
}

float sdBoxFrame( vec3 p, vec3 b, float e )
{
       p = abs(p  )-b;
  vec3 q = abs(p+e)-e;
  return min(min(
      length(max(vec3(p.x,q.y,q.z),0.0))+min(max(p.x,max(q.y,q.z)),0.0),
      length(max(vec3(q.x,p.y,q.z),0.0))+min(max(q.x,max(p.y,q.z)),0.0)),
      length(max(vec3(q.x,q.y,p.z),0.0))+min(max(q.x,max(q.y,p.z)),0.0));
}
/* //Mapeo de area completa
float map(vec3 p){
  
  vec3 spherePos = vec3(cos(iTime)*2., 0., 0.);
  float sphere = sdSphere(p - spherePos, .3);
  
  vec3 q = p;
  
  q.y -= iTime;
  
  q = fract(p) - .5;
  
  float boxFrame = sdBoxFrame(q, vec3(.1,.1,.1), 0.0025 );
  
  //return smin(sphere, boxFrame, 2.);
  
  float piso = p.y + 1.2;
  
  return smin(piso, smin(sphere, boxFrame, 2.), 2.);
}
*/

float map(vec3 p){
  
  
  p.z += iTime * .4;
  
  
  p.xy = fract(p.xy) - 0.5;
  p.z = mod(p.z, 0.25) - .125;
  
  p.xz *= rot2D(iTime);
  p.xy *= rot2D(iTime);
  float fig = sdBoxFrame(p, vec3(.1,.1,.1), 0.015 );
  
  
  //float fig = sdOctahedron(p, .15);
  
  return fig;
}

float map2(vec3 q, vec3 posB){
  
  return sdSphere(q - posB, .3);
}

void main(){
  
  //Normalizar valores de 0 a 1 en valores de resolucion
  vec2 uv = (gl_FragCoord.xy * 1. - iResolution.xy) / iResolution.y;
  vec2 mouse = (iMouse.xy * 1. - iResolution.xy) / iResolution.y*6.;
  
  //inicializar
  
  vec3 ro = vec3(0., 0., -3.);
  vec3 rd = normalize(vec3(uv*1., 1.));
  vec3 col = vec3(1.);
  
  float t = 0.;
  
  
  /*
  //Rotar camara en vertical
  ro.yz *= rot2D(-mouse.y + 200.) ;
  rd.yz *= rot2D(-mouse.y + 200.) ;
  
  //Rotar camara en horizontal
  ro.xz *= rot2D(-mouse.x);
  rd.xz *= rot2D(-mouse.x);
  */
  
  //raymarching
  float j;
  for (int i = 0; i < 80; i+=1){
    vec3 p = ro + rd * t;
    
    p.xy *= rot2D(t*.2 * (mouse.x/5.));
    p.yz *= rot2D(t*.2 * (mouse.y/5.));
    
    p.y += sin(t)/2.;
    //p.x += cos(t)/2.;

    float d = map(p);
    float bola = map2(p, posiBola);
    t += smin(d, bola, 1.5);
    
    if (t<0.001 || t>50.) {
      j = float(i);
      break;
    }
  }
  
  col = palette(t*.3 + j*.002);
  gl_FragColor = vec4(col, 1.);
  
}
```

---
Aquí es donde sucede realmente todo, donde se generan los objetos en un espacio 3d y se calcula su posición con raymarching. con fractales de un boxFrame genera las figuras del fondo y con la función map2 se genera la pelota que rebota en el espacio.

---