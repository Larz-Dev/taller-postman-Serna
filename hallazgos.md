## La diferencia entre PUT y PATCH

Al realizar la petición con PUT se sobreescribió solo el valor indicado "title" y dió como respuesta unicamente el valor modificado junto a su id del elemento, pero esto significaria (Dependiendo del desarrollo del servidor) que no podria pasar nada con los demas valores o se remplazarian por campos vacios.

Al realizar la petición con PATCH PUT se sobreescribió solo el valor indicado "title" y dió como respuesta todos los valores del elemento pero solo con "title" modificado, esto asegura que unicamente fue modificado el valor "title" sin tocar algun otro valor.


| Métodos | Operación               | Función                                              |
| -------- | ------------------------ | ----------------------------------------------------- |
| PUT      | Actualizarción completa | Actualiza o sobreescribe un recurso completo          |
| PATCH    | Actualizarción parcial  | Actualiza o sobreescribe unicamente recuros indicados |


## Idempotencia

Luego de repetir varias veces las operaciones mencionadas se puede notar que GET y PUT siempre darán la misma respuesta,

tambien con DELETE pero hay un caso especial y es que la primera ves no pasa porque se elimina un elemento y retorna que se ha eliminado correctamente, luego de eliminarlo, siempre dará una respuesta de error (En el caso de APIs reales).

Por el contrario, con POST no pasa lo mismo, al repetir una peticion de POST el servidor respondera comunmente con el elemento y dentro de el, un id que irá aumentado cada ves por elemento.

Con PATCH es un caso especial y depende el uso, como el utilizar variables absolutas o relativas.


## Encuentra el límite

| Petición                       | ID  | Detalle                                                                                                          |
| ------------------------------- | --- | ---------------------------------------------------------------------------------------------------------------- |
| El id mas alto que devuelve 200 | 100 | Es el último post registrado en la base de datos.                                                               |
| El primer id que devuelve 404   | 101 | A partir de 100 no hay más post registrados por lo que el servidor regresa 404 al no encontrar ningun registro. |


Este tipo de preubas se llama prueba de valores limite (*boundary value testing* o *boundary value analysis*


[www.geeksforgeeks.org/software-testing/software-testing-boundary-value-analysis](https://www.geeksforgeeks.org/software-testing/software-testing-boundary-value-analysis/)


Los desarrolladores suelen equivocarse con operadores de comparación (`<` vs `<=`, `>` vs `>=`) justo en el borde de un rango. Un ejemplo de algo muy común es cuando se trata de un arreglo (Siempre empiezan de 0 a X) por lo que al poner un limite en el valor length o largo del arreglo siempre se pasará por uno al darnos el valor contando a partir de 1 a X .por lo que siempre se usa -1 en los indexadores de arreglos.
