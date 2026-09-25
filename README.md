# Taller de APIs y Postman

**Estudi****ante:** Javier Andrés Serna Bañol

**Asignatura:** Ingeniería de Software II — Cotecnova


## Marco conceptual

### ¿Qué es una API REST?

Una API de REST es una interfaz de programación de aplicaciones (API) que sigue los principios de diseño del estilo de la arquitectura REST.

Una API es un grupo de protocolos que se usa para crear e integrar sistemas de software a una o más aplicaciones. REST hace referencia a un conjunto de reglas o la arquitectura que se ajusta a las necesidades de las aplicaciones móviles y los servicios web, pero puede depender mucho de los desarrolladores su implementación.

[www.redhat.com/es/topics/api/what-is-a-rest-api](https://www.redhat.com/es/topics/api/what-is-a-rest-api)

## Métodos HTTP

| Método | Operación CRUD          | Qué hace                                             |
| ------- | ------------------------ | ----------------------------------------------------- |
| GET     | Leer                     | Recupera recursos                                     |
| POST    | Crear                    | Crea recursos                                         |
| PUT     | Actualizarción completa | Actualiza o sobreescribe un recurso completo          |
| PATCH   | Actualizarción parcial  | Actualiza o sobreescribe unicamente recuros indicados |
| DELETE  | Elimiar                  | Elimina un recurso                                    |

[learn.microsoft.com/es-es/iis-administration/api/crud](https://learn.microsoft.com/es-es/iis-administration/api/crud)

## Códigos de estado

| Familia de error | Significado               | Ejemplo                                                                                                                                             |
| ---------------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1xx              | Respuestas informativas   | El servidor ha recibido una solicitud por lo que ha empezado a cargar o procesar                                                                    |
| 2xx              | Respuestas satisfactorias | El servidor a respondido correctamente a una solicitud ( Crear una cuenta en una página web)                                                       |
| 3xx              | Redirecciones             | El servidor ha redirigido al cliente porque el recurso solicitado ya no se encuentra en el lugar actual, y lo reenvia a el nuevo lugar.             |
| 4xx              | Errores de los clientes   | El servidor ha recibido la solicitud correctamente pero no puede interpretarla debido a un mal diligenciamiento (links o formularios mal escritos). |
| 5xxz             | Errores de los servidores | El cliente intenta acceder al servidor pero este no se encuentra en servicio o en mantenimiento por lo que notifica al cliente.                     |

[developer.mozilla.org/es/docs/Web/HTTP/Reference/Status](https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Status)

## Experimentando con la API

| # | Petición       | Código esperado | Código obtenido | ¿Coincide? |
| :-: | --------------- | ---------------- | ---------------- | ----------- |
| 1 | GET /posts/1    | 2xx              | 200              | Sí         |
| 2 | GET /posts      | 2xx              | 200              | Sí         |
| 3 | GET /posts/9999 | 4xx              | 404              | Sí         |
| 4 | POST /posts     | 4xx              |                  |             |
| 5 | PUT /posts/1    | 4xx              |                  |             |
| 6 | PATCH /posts/1  | 4xx              |                  |             |
| 7 | DELETE /posts/1 | 2xx              |                  |             |

Luego de realizar las peticiones 1 y 2 he obtenido lo siguiente:

|                                      | GET /posts/1 | GET /posts |
| ------------------------------------ | ------------ | ---------- |
| Código de estado                    | 200          | 200        |
| Cuántos elementos trae la respuesta | 1            | 100        |
| Qué campos tiene cada elemento      | 4            | 4          |

### ¿En qué se diferencian los criterios de aceptación cuando pides un recurso y cuando pides una colección?

En el número de elementos de respuestas obtenidas, si se especifica un valor, este es interpretado como el identificador para obtener un solo recurso especifico, en cambio, si no se especifica un indicador, se obtendra el valor máximo de elementos que esté configurado por el servidor.

### Petición 3 - ¿Este caso de prueba pasó o falló?

Falló por parte del cliente al intentar buscar en el servidor un elemento con un identificador inexistente en la base de datos.

### ¿Qué pasaría si esa misma petición hubiera devuelto 200 con un cuerpo vacío?

Se trataria de una mala configuración de respuestas en el servidor y podria causar el colapso del mismo.

### ¿Sería un defecto?

Si, pues se esperaba que la respuesta hubiese sido un error 4xx ya que el cliente intenta buscar algo que no existe.

## Crea un recurso con POST

| Veces | ¿Que pasó?                                                                                          | id | Código HTML  |
| ----- | ----------------------------------------------------------------------------------------------------- | :-: | ------------- |
| 1     | Ha retornado el mismo elemento enviado junto al id asignado en la base de datos luego de almacenarlo. | 101 | 201 - Created |
| 2     | Ha retornado el mismo elemento enviado junto al id asignado en la base de datos luego de almacenarlo. | 101 | 201 - Created |
| 3     | Ha retornado el mismo elemento enviado junto al id asignado en la base de datos luego de almacenarlo. | 101 | 201 - Created |
| 4     | Ha retornado el mismo elemento enviado junto al id asignado en la base de datos luego de almacenarlo. | 101 | 201 - Created |
| 5     | Ha retornado el mismo elemento enviado junto al id asignado en la base de datos luego de almacenarlo. | 101 | 201 - Created |

### ¿Qué observaste?

La respuesta del servidor es siempre la misma, y el id del elemento tambien se repite

### ¿Por qué crees que ocurre eso?

Se debe a que es una API de prueba y esta solo simula que llegó la información correctamente, mas no la escribe o almacena en una base de datos real para luego ser consultada.

### ¿Cómo comprobarías, en una API real, que el recurso se creó de verdad?

Usando la ruta de consulta en este caso ( GET /posts/101 ) o revisando la base de datos

## La diferencia entre PUT y PATCH

### ¿Qué diferencia encontraste entre ambas respuestas?

Al realizar la petición con PUT se sobreescribió solo el valor indicado "title" y dió como respuesta unicamente el valor modificado junto a su id del elemento, pero esto significaria (Dependiendo del desarrollo del servidor) que no podria pasar nada con los demas valores o se remplazarian por campos vacios.

Al realizar la petición con PATCH PUT se sobreescribió solo el valor indicado "title" y dió como respuesta todos los valores del elemento pero solo con "title" modificado, esto asegura que unicamente fue modificado el valor "title" sin tocar algun otro valor.

| Métodos | Operación               | Función                                              |
| -------- | ------------------------ | ----------------------------------------------------- |
| PUT      | Actualizarción completa | Actualiza o sobreescribe un recurso completo          |
| PATCH    | Actualizarción parcial  | Actualiza o sobreescribe unicamente recuros indicados |

### ¿Cuál usarías para corregir un error de escritura en un solo campo, y por qué?

PATCH, pues quiero asegurarme que no voy a modificar o remplazar algo mas, solo el valor que quiero.
