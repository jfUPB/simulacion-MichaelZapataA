#### Actividad 8

En una de las lineas el valor se pasa por **valor** (La primera linea) y en la otra se pasa por **referencia** (La segunda linea), en el caso de la segunda linea que se pasa por referencia, puede dar problemas de muchas formas, por ejemplo, puede que se necesite modificar la fricción y por el hecho de pasarse como una referencia de la velocidad, al modificar la fricción se modificaría el vector original de la velocidad, y de forma recíproca se modificaría la fricción cuando se altere el valor de la velocidad. Es en definitiva algo que no se quiere ni debería hacer en este caso.


Un dato se pasa por valor cuando se le da (valga la redundancia) el valor que tiene la variable y se genera una nueva copia que no afecta el valor original.

Es por referencia cuando se le entrega el espacio de memoria donde se tiene guardado el objeto original, por lo tanto tiene como un apuntador que lleva al mismo vector original en vez de obtener los datos exactos de este objeto.