# CAPA DE PERSISTENCIA

En una arquitectura limpia, los **repositorios** tienen la responsabilidad de gestionar el acceso a los datos desde la perspectiva del dominio. Esto significa que trabajan exclusivamente con modelos de dominio, abstrayendo por completo los detalles de cómo y dónde se almacenan los datos. Su objetivo principal es proporcionar una interfaz coherente que permita a la capa de dominio interactuar con los datos sin preocuparse por las particularidades de la persistencia.

Para lograr este aislamiento, los repositorios no deberían implementar directamente las operaciones específicas de almacenamiento o recuperación. Aquí es donde entra en juego la introducción de los **DAOs**, que encapsulan los detalles de persistencia. Por ejemplo, en un sistema que combine una base de datos y un sistema de caché, los repositorios podrían delegar en un DAO el acceso a la caché para recuperar datos rápidamente o almacenar temporalmente resultados, manteniendo así su enfoque en los modelos de dominio.

> [!NOTE]
> Un repositorio puede llamar a varios DAO. Por ejemplo DB y Caché

**DAO (Data Access Object)**

El patrón DAO (Data Access Object) se utiliza para separar y encapsular el acceso a los datos, proporcionando una capa de abstracción que aísla la lógica de acceso a datos del resto de la aplicación. Esto permite que el resto de la aplicación, y en particular la capa de dominio, interactúe con los datos sin preocuparse por los detalles específicos de persistencia. Los DAOs facilitan la delegación de las operaciones de acceso a los datos, de modo que los repositorios se puedan enfocar únicamente en trabajar con los modelos de dominio.

**ESTRUCTURA DE CARPETAS PERSISTENCE:

├───dao
│   ├───cache *//Sistema de acceso a caché (interfaces)*
│   │   │   BookDaoCache.java
│   │   │   GenericDaoCache.java
│   │   │   
│   │   └───impl
│   │           BookDaoCacheImpl.java
│   │           
│   └───db *//Sistema de acceso a base de datos (interfaces)*
│       │   AuthorDaoDb.java
│       │   BookDaoDb.java
│       │   CategoryDaoDb.java
│       │   GenericDaoDb.java *DAO genérico que ya maneja las relaciones en el CRUD* 
│       │   GenreDaoDb.java
│       │   PublisherDaoDb.java
│       │   
│       └───jdbc *//Implementación de las interfaces para JDBC*
│           │   AuthorDaoJdbc.java
│           │   BaseDaoJdbc.java *//Implementación del DAO genérico (existe la herencia)*
│           │   BookDaoJdbc.java
│           │   CategoryDaoJdbc.java
│           │   GenreDaoJdbc.java
│           │   PublisherDaoJdbc.java
│           │
│           ├───mapper *//Mapeadores de ResultSet a las entidades de dominio*
│           │   ├───generic
│           │   │       GenericRowMapper.java *// Mapeador genérico*
│           │   │
│           │   └───specific *//Si alguna clase tuviera algún mapeo especial*
│           │           .gitkeep
│           │
│           └───utils *//Carpeta de utilidades para el mapeador genérico*
│               ├───cache *//Caché para las anotaciones. Al utilizar este sistema mejoramos el                                                     inconveniente de rendimiento de la reflexión*
│               │       ReflectionColumnFieldCache.java *//Para la anotación @Column*
│               │
│               ├───metadata *//Extractor de metadatos*
│               │       EntityMetadataExtractor.java
│               │
│               ├───operation *// Tipos de operaciones que se pueden realizar*
│               │       OperationType.java *//Enum*
│               │
│               ├───relation *//Maneja las relaciones*
│               │       RelationMapperHandler.java *//En el mapeo*
│               │       RelationOperationHandler.java *//En las operaciones INSERT, UPDATE y DELETE*
│               │
│               ├───sql *//Código SQL centralizado*
│               │       SqlBuilderOperation.java *//SQL para las operaciones*
│               │       SqlBuilderRelation.java *//SQL para las relaciones*
│               │
│               └───text *//Métodos para funcionalidades de texto*
│                       StringUtil.java *//Métodos para la clase String*
│
└───repository
    └───impl *//Implementación de las interfaces definidas en dominio*
            AuthorRepositoryJdbc.java
            BookRepositoryJdbc.java
            CategoryRepositoryJdbc.java
            GenreRepositoryJdbc.java
            PublisherRepositoryJdbc.java

---

