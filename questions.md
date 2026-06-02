# Preguntas — Arquitectura en Capas

## 1. ¿Qué es un controlador y de qué se encarga?
Es el que recibe las peticiones del cliente (como Postman). Se encarga de capturar las rutas (los endpoints) y decidir a qué servicio mandar esa información para que se procese.

## 2. ¿Qué responsabilidad tiene la capa de servicio?
Ahí va toda la lógica del negocio. Es donde se ponen las reglas y validaciones importantes antes de guardar o mover cualquier dato en el sistema.

## 3. ¿Qué hace el repositorio y de qué se encarga?
Es la capa que se conecta directo con la base de datos. Gracias a Spring Data JPA, nos permite hacer operaciones como guardar, buscar o borrar registros sin escribir código SQL a mano.

## 4. ¿Qué es una entidad y a qué se mapea en la base de datos?
Es una clase normal de Kotlin pero que representa una tabla de la base de datos. Cada objeto que creamos de esa clase equivale a una fila en esa tabla.

## 5. ¿Para qué sirve un DTO y por qué no devolvemos la entidad directamente?
Sirve para controlar qué datos entran y salen de la API. No se devuelve la entidad directo por seguridad y para no mostrar datos innecesarios o internos que el cliente no necesita ver.

## 6. ¿Cuál es la diferencia entre un Request y un Response DTO?
El Request es el molde para los datos que nos envían (por ejemplo, al crear un libro no mandamos el ID porque lo crea la base de datos). El Response es el molde de lo que nosotros le devolvemos al cliente, ya con su ID asignado.

## 7. ¿Por qué separamos la aplicación en capas? Menciona una ventaja.
Para que el código esté ordenado y cada parte haga una sola cosa. La gran ventaja es el mantenimiento: si cambias la base de datos, solo tocas la capa del repositorio y el resto del proyecto sigue funcionando igual.

## 8. ¿Qué anotación se usa para marcar un controlador REST? ¿Y un servicio?
Para el controlador usamos `@RestController` y para el servicio usamos `@Service`. Así Spring sabe qué es cada cosa y las puede inyectar.

## 9. ¿Qué hace @RequestBody en un endpoint?
Agarra el JSON que manda el cliente en el cuerpo de la petición y lo convierte automáticamente en un objeto de Kotlin para que podamos usar sus datos.

## 10. ¿Cuál es el flujo que sigue un request desde que llega hasta que se guarda en la base de datos?
Llega el JSON al **Controller**, este lo pasa al **Service** donde se revisa la lógica, el Service lo convierte en una entidad y se lo pasa al **Repository**, y el Repository finalmente lo guarda en la base de datos **H2**.