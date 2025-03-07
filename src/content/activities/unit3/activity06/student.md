#### Actividad 6

Se cambia en applyForce y ahora si se aplica de forma correcta, en vez de reasignar, se está añadiendo al valor de la aceleración

La aceleración debe multiplicarse por 0 después de cada frame porque al estar calculando la aceleración como suma de fuerzas cada vez, si no la seteamos en 0, sumará indefinidamente, y se hace al final de la función para alcanzar a sumarle la aceleración a la velocidad antes de borrarla.