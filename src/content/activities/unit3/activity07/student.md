#### Actividad 7

Si asumimos tener masa, implica que la aceleración es igual a (la sumatoria de fuerzas) sobre la masa.

En el caso planteado en la unidad, se está haciendo la sumatoria de (fuerza sobre la masa), que aunque puede parecer más o menos lo mismo es bien diferente jajaja.

Para solucionar el problema habría que dividir sobre la masa luego de aplicar todas las fuerzas. siento que sería más o menos así.

```js
mover.applyForce(wind);
mover.applyForce(gravity);
mover.acceleration.div(mover.masa);
```

```js
applyForce(force) {
    this.acceleration.add(force);
}
```

Además, en la propuesta se modifica el vector wind y gravity ya que está siendo pasado por referencia al ser un P5.vector, entonces a menos que en cada frame se reasigne la gravedad y el viento, que sería super ineficiente, se perjudicaría el código base.