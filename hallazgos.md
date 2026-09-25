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

Los desarrolladores suelen equivocarse con operadores de comparación (`<` y `<=`, `>` y `>=`) justo en el borde de un rango. Un ejemplo de algo muy común es cuando se trata de un arreglo (Siempre empiezan de 0 a X) por lo que al poner un limite en el valor length o largo del arreglo siempre se pasará por uno al darnos el valor contando a partir de 1 a X .por lo que siempre se usa -1 en los indexadores de arreglos.

## Explora otros recursos

| Rutas descubiertas | Recursos                                                                                                     |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| /albums            | Retorna un objeto con multiples elementos de un albun                                                        |
| /users             | Retorna un objeto con multiples elementos y sub-elementos de usurarios como nombre, correo, dirección, ect. |

Una ruta anidada es "Posts/1/comments", se encuenta en la documentación de la página web, pero por el link de la ruta se puede saber que hace referencia a que esta buscando los comentarios del post con id número 1.

## Automatiza la verificación

pm.test("El estado es 200", function () {    pm.response.to.have.status(200);});

muestra en verde 200 se se cumple la condición de la respuesta, por otro lado si se cambia a 201 y se la respuesta vuelve a llegar 200 entonces mostrará error.

### ¿por qué es importante ver una prueba fallar antes de confiar en ella?



Un equipo puede tener cientos de pruebas, pero si esas pruebas nunca fueron probadas para fallar, esa validación puede ser mentira. Causando problemas a futuro con algun error en el servidor o API real.


## Tus propias pruebas



| Prueba                                                                                                        | ¿Que hace?                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| pm.test("Tiene el campo title", function () { pm.expect(pm.response.json()).to.have.property("title");});    | Comprueba si existe un valor dentro del registro de nombre "Title".                                                                                  |
| pm.test("Responde en menos de 500ms", function () { pm.expect(pm.response.responseTime).to.be.below(500);}); | Comprueba que la respuesta del servidor debe demorar menos de 500ms, de lo contrario saldrá en rojo.                                                 |
| pm.test("El estado es 404", function (){ pm.response.to.have.status(404);});                                 | Comprueba esperar un error a proposito de registro no encontrado, por lo que debe mostrar verde si no se encuentra registro en un id fuera de limite. |
