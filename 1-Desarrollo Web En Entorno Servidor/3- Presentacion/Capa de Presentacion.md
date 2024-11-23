# CAPA DE PRESENTACIÓN

La capa de presentación en una arquitectura por capas se encarga de gestionar la interacción del usuario con la aplicación. Su principal función es recibir las solicitudes del usuario (normalmente a través de controladores REST o MVC en el caso de aplicaciones web), procesarlas y devolver una respuesta adecuada. Aquí se implementan los controladores que definen los endpoints de la API y, opcionalmente, la lógica de validación básica de las solicitudes.

Esta capa debe ser lo más independiente posible de la lógica de negocio y la persistencia. Se comunica con la capa de dominio o de aplicación para ejecutar los casos de uso requeridos, devolviendo al usuario las respuestas en el formato adecuado (como JSON o HTML). También puede encargarse del manejo de excepciones y la validación básica de los datos de entrada.


**ESTRUCTURA DE CARPETAS CONTROLLER:**

├───**admin**
│   │   BookAdminController.java *// Controlador del admin* 
│   │   
│   └───adminModel *// Modelos únicos del admin*
│       └───book
│               BookAdminCollection.java *// Colección de datos (getAll)*
│               
├───**common**
│   │   BaseController.java *//Controlador con funcionalidades genéricas (herencia)* 
│   │   
│   ├───entity *//Entidades comunes a los roles*
│   │   └───model *//Modelos de datos*
│   │       ├───author
│   │       │       AuthorCollection.java
│   │       │       
│   │       └───publisher
│   │               PublisherCollection.java
│   │   └───mapper */En el caso de tener que mapear entidades comunes a los roles*
│   │               
│   └───pagination *// Paquete que centra la lógica de la paginación*
│           PaginatedResponse.java
│
└───**user**
    │   BookUserController.java *//Controlador de usuario sin privilegios*
    │
    ├───userMapper *//Mapeadores para los modelos específicos de usuario*
    │   └───book
    │           BookUserMapper.java
    │
    └───userModel *//Modelos específicos de usuario*
        └───book
                BookUserCollection.java *//Colección de datos (getAll)*
                BookUserDetail.java *//Respuesta de un registro (getByX)*


---

> [!NOTE]  
> Para mapear entre modelos de Dominio y Presentación (DTO) se utiliza `ModelMapper`. Los tipos de datos simples pueden ser mapeados automáticamente sin necesidad de indicarle el cómo. Sin embargo, si utilizamos tipos de datos personalizados (clases propias), debemos indicarle explícitamente cómo debe hacerlo.
> 
> Para poder utilizar `ModelMapper`, debemos añadir la dependencia correspondiente en el `pom.xml` y crear una instancia. A continuación, bajo se muestra un ejemplo de uso:

```java
private static final ModelMapper modelMapper = new ModelMapper();  
  
public static BookUserDetail toBookDetail(Book book) {  
    // Mapear el libro a BookUserDetail  
    BookUserDetail bookUserDetail = modelMapper.map(book, BookUserDetail.class);  
  
    // Mapea la editorial  
    if (book.getPublisher() != null) {  
        bookUserDetail.setPublisherCollection(new PublisherCollection(  
                book.getPublisher().getId(),  
                book.getPublisher().getName()  
        ));  
    }  
  
    // Mapea los autores  
    if (book.getAuthors() != null) {  
        List<AuthorCollection> authorsCollection = book.getAuthors().stream()  
                .map(author -> new AuthorCollection(author.getId(), author.getName()))  
                .collect(Collectors.toList());  
        bookUserDetail.setAuthorsCollection(authorsCollection);  
    }  
  
    // Mapea los géneros  
    if (book.getGenres() != null) {  
        List<String> genres = book.getGenres().stream()  
                .map(genre -> genre.getName())  
                .collect(Collectors.toList());  
        bookUserDetail.setGenres(genres);  
    }  
  
    // Mapea la categoría  
    if (book.getCategory() != null) {  
        bookUserDetail.setCategory(book.getCategory().getName());  
    }  
  
    return bookUserDetail;  
}
```

