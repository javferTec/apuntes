# PAQUETE COMÚN A TODA LA APLICACIÓN

**ESTRUCTURA DE CARPETAS <u>COMMON</u>:**

├───annotation *//Anotaciones*
│   ├───common
│   │       Mapper.java *//Usada en Controller y Persistence*
│   │       
│   ├───domain *//Creadas para que el dominio no tenga tanta dependencia con SpringBoot*
│   │       DomainService.java
│   │       DomainTransactional.java
│   │       DomainUseCase.java
│   │       
│   └───persistence *//Relacionadas con BaseDao, el mapeador genérico y los DAOs*
│           Column.java
│           Dao.java
│           ManyToMany.java
│           OneToMany.java
│           OneToOne.java
│           PrimaryKey.java
│           Table.java
│           
├───errorHandler *//Manejador de errores de la API*
│       ApiExceptionHandler.java
│       ErrorMessage.java
│
├───exception *//Excepciones*
│       MappingException.java
│       ResourceAlreadyExistsException.java
│       ResourceNotFoundException.java
│
└───locale *//Para que la aplicación pueda manejar varios idiomas*
        CustomLocaleChangeInterceptor.java
        LanguageUtils.java
        LocaleConfig.java
