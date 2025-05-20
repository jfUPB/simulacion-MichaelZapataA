#### Actividad 1

La suma de vectores funciona sumando sus componentes una a una.

$$(x_1,y_1) + (x_2,y_2)  = (x_1+x_2,y_1+y_2)$$

---

La linea ```position = position + velocity;``` no funciona porque al usar las variables de esta forma se realiza una concatenación de las cadenas de texto con los apuntadores hacia los espacios de memoria donde están guardados los vectores.

Una forma un poco más rústica que se podría utilizar sería:

```js
position.x = position.x + velocity.x;
position.y = position.y + velocity.y;
```

Sin embargo, esto no es necesario gracias a la funcion ```vector.add();``` que se encuentra implementada en P5.JS.