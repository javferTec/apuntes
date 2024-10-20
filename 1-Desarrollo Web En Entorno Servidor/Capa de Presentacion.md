# CAPA DE PRESENTACIÓN

La capa de presentación en una arquitectura por capas se encarga de gestionar la interacción del usuario con la aplicación. Su principal función es recibir las solicitudes del usuario (normalmente a través de controladores REST o MVC en el caso de aplicaciones web), procesarlas y devolver una respuesta adecuada. Aquí se implementan los controladores que definen los endpoints de la API y, opcionalmente, la lógica de validación básica de las solicitudes.

Esta capa debe ser lo más independiente posible de la lógica de negocio y la persistencia. Se comunica con la capa de dominio o de aplicación para ejecutar los casos de uso requeridos, devolviendo al usuario las respuestas en el formato adecuado (como JSON o HTML). También puede encargarse del manejo de excepciones y la validación básica de los datos de entrada.

## Endpoints



## Modelos de la capa de presentación



## Mapeadores (MapStruct)



## Respuesta (ResposeEntity)



## Tratamiento de excepciones


## Idioma

### LanguageUtils


### Interceptores en Java


### LocaleConfig



## Paginación



## Roles




