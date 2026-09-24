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
