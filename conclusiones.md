## Las cabeceras de la respuesta

| Key                              | Value                           | Definición                                                                                                         | Función                                                                                                                                        |
| -------------------------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Content-Type                     | application/json; charset=utf-8 | Es la propiedad de cabecera (header) usada para indicar el media type del recurso.                                  | Permite al receptor o cliente saber cómo tratar la petición recibida, puede tratarse de archivos, imágenes, texto plano, o textos tipo JSON. |
| Access-Control-Allow-Credentials | true                            | Cabecera de CORS que indica si la respuesta puede exponerse cuando la petición se hizo con credenciales incluidas. | Le dice al navegador si exponer la respuesta al código JavaScript (del frontend) cuando el modo credenciales en la petición es incluido.      |
| Server                           | cloudflare                      | Cabecera que identifica el software del servidor que atendió la solicitud.                                         | Contiene la información acerca del software usado por el servidor original encargado de la solicitud.                                          |


[developer.mozilla.org/es/docs/Web/HTTP/Reference/Headers](https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Headers)


## Porque es importante "Content-Type" al momento de realizar prueba en una API?


Porque es el que indica primero al servidor como tratar con el formato del contenido de la petición, sin el, el servidor simplemente no entenderia que hacer con la información entrante, en caso esperar un JSON como respuesta y le llega una imagen "image/png" probablemente retornara un error el servidor o causaria un error.
