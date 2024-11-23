# CAPA DE DOMINIO

En una arquitectura limpia, la capa de dominio es el corazón de la aplicación. Aquí es donde se encuentran las reglas de negocio y la lógica fundamental que define el comportamiento del sistema. Esta capa debe estar **completamente aislada de cualquier detalle de implementación o infraestructura, como bases de datos, frameworks o herramientas de persistencia**. Esto permite que los cambios en estos detalles no afecten la lógica central del negocio.

**ESTRUCTURA DE CARPETAS DOMAIN:**

├───**model** *//Entidades o modelos de la aplicación*
│       Author.java 
│       Book.java 
│       Category.java
│       Genre.java
│       Publisher.java 
│
├───**repository** *//Interfaces de repositorio*
│       AuthorRepository.java 
│       BookRepository.java
│       CategoryRepository.java
│       GenreRepository.java
│       PublisherRepository.java
│
├───**service** *//Interfaces de los servicios*
│   │   AuthorService.java
│   │   BookService.java 
│   │   CategoryService.java 
│   │   GenreService.java 
│   │   PublisherService.java 
│   │
│   └───impl *//Implementación de los servicios*
│           AuthorServiceImpl.java
│           BookServiceImpl.java 
│           CategoryServiceImpl.java 
│           GenreServiceImpl.java 
│           PublisherServiceImpl.java
│
└───**useCase** *//Casos de uso. Dividido por entidades y dentro de este por los roles*
    └───**book**
        ├───**admin** *//Interfaces de los casos de uso de admin*
        │   │   BookDeleteUseCase.java 
        │   │   BookInsertAuthorsUseCase.java 
        │   │   BookInsertGenresUseCase.java
        │   │   BookInsertUseCase.java 
        │   │   BookRelationHandler.java *//Maneja las relaciones uno a uno, uno a muchos y                                                              muchos a muchos en INSERT, UPDATE y DELTE (para                                                            no repetir código en cada caso de uso)*
        │   │   BookUpdateUseCase.java 
        │   │
        │   └───impl *//Implementaciones de los casos de uso de admin*
        │           BookDeleteUseCaseImpl.java 
        │           BookInsertAuthorsUseCaseImpl.java
        │           BookInsertGenresUseCaseImpl.java a un libro*
        │           BookInsertUseCaseImpl.java
        │           BookRelationHandlerImpl.java 
        │           BookUpdateUseCaseImpl.java 
        │
        ├───**common** *//Interfaces de los casos de uso comunes*
        │   │   BookCountUseCase.java 
        │   │   BookGetAllUseCase.java 
        │   │   BookGetByIsbnUseCase.java 
        │   │
        │   └───impl *//Implementaciones de los casos de uso comunes* 
        │           BookCountUseCaseImpl.java 
        │           BookGetAllUseCaseImpl.java 
        │           BookGetByIsbnUseCaseImpl.java
        │
        └───**user** *//Interfaces de los casos de uso de user*

---

>[!NOTE]
>Movemos las interfaces del repositorio a Dominio para la **INYECCIÓN DE DEPENDENCIAS EN LA CAPA DE DOMINIO**. 

> [!NOTE]
> Los **CASOS DE USO SON COMUNES**, por lo tanto las entidades también, mapeamos en el controlador.
> Los casos de uso son los encargados de llamar a los servicios para realizar las acciones correspondientes. Los servicios de momento solo hacen acciones básicas sobre los recursos. Los controladores llaman a los casos de uso.

