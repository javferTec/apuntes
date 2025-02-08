
# getAll

```scss
BaseController.getPageSize(Integer)
└── Integer.parseInt(String)

BookGetAllUseCase.execute(int, int)
└── BookGetAllUseCaseImpl.execute(int, int)
    └── BookService.getAll()
        └── BookServiceImpl.getAll()
            └── BookRepository.getAll()
                └── BookRepositoryJdbc.getAll()
                    └── GenericDaoDb.getAll()
                        ├── PublisherDaoJdbc.getAll()
                        │   └── BaseDaoJdbc.getAll()
                        ├── AuthorDaoJdbc.getAll()
                        │   └── BaseDaoJdbc.getAll()
                        ├── CategoryDaoJdbc.getAll()
                        │   └── BaseDaoJdbc.getAll()
                        ├── GenreDaoJdbc.getAll()
                        │   └── BaseDaoJdbc.getAll()
                        ├── BookDaoJdbc.getAll()
                        │   └── BaseDaoJdbc.getAll()
                        └── BaseDaoJdbc.getAll()
                            ├── EntityMetadataExtractor.getSelectTable()
                            ├── JdbcTemplate.query(String, RowMapper<T>)
                            ├── AuthorDaoJdbc.getAll()
                            ├── PublisherDaoJdbc.getAll()
                            ├── CategoryDaoJdbc.getAll()
                            ├── BookDaoJdbc.getAll()
                            └── GenreDaoJdbc.getAll()

ModelMapper.map(Object, Class<D>)

BookCountUseCase.execute()
└── BookCountUseCaseImpl.execute()
    └── BookService.count()
        └── BookServiceImpl.count()
            └── BookRepository.count()
                └── BookRepositoryJdbc.count()
                    └── GenericDaoDb.count()
                        ├── BaseDaoJdbc.count()
                        │   ├── EntityMetadataExtractor.getTableName()
                        │   │   └── EntityMetadataExtractor.getTableName(Class<?>)
                        │   ├── JdbcTemplate.queryForObject(String, Class<T>)
                        │   ├── CategoryDaoJdbc.count()
                        │   ├── GenreDaoJdbc.count()
                        │   ├── AuthorDaoJdbc.count()
                        │   ├── PublisherDaoJdbc.count()
                        │   └── BookDaoJdbc.count()
                        ├── CategoryDaoJdbc.count()
                        │   └── BaseDaoJdbc.count()
                        ├── GenreDaoJdbc.count()
                        │   └── BaseDaoJdbc.count()
                        ├── AuthorDaoJdbc.count()
                        │   └── BaseDaoJdbc.count()
                        ├── PublisherDaoJdbc.count()
                        │   └── BaseDaoJdbc.count()
                        └── BookDaoJdbc.count()
                            └── BaseDaoJdbc.count()

BaseController.getAll(int, Integer, Function<Integer, List<Entity>>, Function<Entity, Collection>, int, String)
├── BaseController.getPageSize(Integer)
│   └── Integer.parseInt(String)
├── Function.apply(T)
│   ├── apply methods from various sources (e.g., jdk, Spring, other libraries)
└── Collection.stream()
    ├── stream() methods from various sources (e.g., Collections, Java Stream API)
    └── Stream.map(Function<? super T, ? extends R>)
        └── ReferencePipeline.map(Function<? super P_OUT, ? extends R>)
            └── Stream.toList()
                └── ReferencePipeline.toList()

BaseController.createPaginatedResponse(List<T>, int, int, int, String)
├── PaginatedResponse.PaginatedResponse(List<T>, int, int, int, String)
└── ResponseEntity.ResponseEntity(T, HttpStatusCode)

```

---

# getById

```scss
BookGetByIsbnUseCase.execute(String)
 └── BookGetByIsbnUseCaseImpl.execute(String)
      └── BookService.getByIsbn(String)
           └── BookServiceImpl.getByIsbn(String)
                └── BookRepository.getByIsbn(String)
                     └── BookRepositoryJdbc.getByIsbn(String)
                          ├── BookDaoCache.getByIsbn(String)
                          │    └── BookDaoCacheImpl.getByIsbn(String)
                          │         ├── SystemLogHandler.println(String)
                          │         └── BookDaoDb.getByIsbn(String)
                          │              └── BookDaoJdbc.getByIsbn(String)
                          ├── GenericDaoCache.save(T)
                          │    └── BookDaoCacheImpl.save(Book)
                          │         ├── Book.java (domain model)
                          │         └── Map.put(K, V)
                          │              └── [Various implementations in java.util and external libraries]
                          ├── System.currentTimeMillis()
                          ├── Optional.ifPresent(Consumer)
                          └── Optional.or(Supplier)

ResourceNotFoundException (extends RuntimeException)
 └── Thrown in case of missing entity

BaseController.getByIsbn(String, Function<String, Entity>, Function<Entity, Detail>)
 ├── Function.apply(T)
 │    └── [Various implementations in java.util.function and external libraries]
 └── ResponseEntity(T, HttpStatusCode)

```

---
# insertAuthors

```scss
BookInsertAuthorsUseCase.execute(Integer, List<Author>)
 └── BookInsertAuthorsUseCaseImpl.execute(Integer, List<Author>)
     └── BookService.getById(long)
         └── BookServiceImpl.getById(long)
             └── BookRepository.getById(long)
                 └── BookRepositoryJdbc.getById(long)
                     └── GenericDaoDb.getById(long)
                         ├── BaseDaoJdbc.getById(long)
                         │   ├── EntityMetadataExtractor.getSelectTable()
                         │   ├── BaseDaoJdbc.queryForOptional(String, Object...)
                         │   ├── GenreDaoJdbc.getById(long)
                         │   ├── PublisherDaoJdbc.getById(long)
                         │   ├── BookDaoJdbc.getById(long)
                         │   ├── AuthorDaoJdbc.getById(long)
                         │   └── CategoryDaoJdbc.getById(long)
                         └── ResourceNotFoundException.ResourceNotFoundException(String)
                             └── RuntimeException.RuntimeException(String)
 └── AuthorService.getAllById(List<Author>)
     └── AuthorServiceImpl.getAllById(List<Author>)
         └── Collection.stream()
             ├── stream() in UnmodifiableEntrySet in UnmodifiableMap in Collections
             ├── stream() in ListFromStream in ListAssert
             ├── stream() in ReverseOrderLinkedListView in LinkedList
             └── ...
 └── List.size()
     └── ...
 └── BookService.addAuthor(Book, Author)
     └── BookServiceImpl.addAuthor(Book, Author)
         ├── Book.java
         ├── ArrayList.ArrayList()
         ├── List.contains(Object)
         │   ├── contains(Object) in SingletonList in Collections
         │   └── ...
         └── ResourceAlreadyExistsException.ResourceAlreadyExistsException(String)
             └── RuntimeException.RuntimeException(String)
 └── Iterable.forEach(Consumer<? super T>)
     └── ...
 └── BookService.save(Book)
     └── BookServiceImpl.save(Book)
         └── BookRepository.save(Book)
             └── BookRepositoryJdbc.save(Book)
                 ├── Book.java
                 ├── GenericDaoDb.update(T)
                 │   ├── PublisherDaoJdbc.update(Publisher)
                 │   ├── ...
                 ├── GenericDaoDb.insert(T)
                 │   ├── BookDaoJdbc.insert(Book)
                 │   └── ...
                 ├── Book.java
                 └── GenericDaoCache.clearCache()
                     └── BookDaoCacheImpl.clearCache()
ResponseEntity.ResponseEntity(HttpStatusCode)
```


---
# insertGenres

```scss
BookInsertGenresUseCase.execute(Integer, List<Genre>)
 └── BookInsertGenresUseCaseImpl.execute(Integer, List<Genre>)
     └── BookService.getById(long)
         └── BookServiceImpl.getById(long)
             └── BookRepository.getById(long)
                 └── BookRepositoryJdbc.getById(long)
                     └── GenericDaoDb.getById(long)
                         ├── GenreDaoJdbc.getById(long)
                         │   └── BaseDaoJdbc.getById(long)
                         ├── PublisherDaoJdbc.getById(long)
                         │   └── BaseDaoJdbc.getById(long)
                         ├── BaseDaoJdbc.getById(long)
                         │   ├── EntityMetadataExtractor.getSelectTable()
                         │   ├── BaseDaoJdbc.queryForOptional(String, Object...)
                         │   ├── GenreDaoJdbc.getById(long)
                         │   ├── PublisherDaoJdbc.getById(long)
                         │   ├── BookDaoJdbc.getById(long)
                         │   ├── AuthorDaoJdbc.getById(long)
                         │   └── CategoryDaoJdbc.getById(long)
                         └── BookDaoJdbc.getById(long)
                             └── BaseDaoJdbc.getById(long)
                         ├── AuthorDaoJdbc.getById(long)
                         │   └── BaseDaoJdbc.getById(long)
                         └── CategoryDaoJdbc.getById(long)
                             └── BaseDaoJdbc.getById(long)
 └── ResourceNotFoundException.ResourceNotFoundException(String)
     └── RuntimeException.RuntimeException(String)
 └── Optional.orElseThrow(Supplier<? extends X>)
 └── GenreService.getAllById(List<Genre>)
     └── GenreServiceImpl.getAllById(List<Genre>)
         └── Collection.stream()
             ├── stream() in UnmodifiableEntrySet in UnmodifiableMap in Collections
             ├── stream() in ListFromStream in ListAssert
             ├── stream() in ReverseOrderLinkedListView in LinkedList
             ├── stream() in SynchronizedCollection in Collections
             ├── stream() in SetFromMap in Collections
             ├── ReverseOrderDequeView.stream()
             ├── stream() in UnmodifiableEntrySet in UnmodifiableMultiValueMap
             ├── stream() in CopiesList in Collections
             ├── stream() in UnmodifiableCollection in Collections
             ├── stream() in AsLIFOQueue in Collections
             ├── ReverseOrderListView.stream()
             ├── stream() in Reversed in CopyOnWriteArrayList
             ├── ReverseOrderSortedSetView.stream()
             ├── stream() in UnmodifiableValueCollection in UnmodifiableMultiValueMap
             ├── stream() in ViewCollection in AbstractMap
             └── stream() in CheckedCollection in Collections
 └── Genre.java
 └── Stream.map(Function<? super T, ? extends R>)
     └── ReferencePipeline.map(Function<? super P_OUT, ? extends R>)
 └── Stream.toArray(IntFunction<A[]>)
     └── ReferencePipeline.toArray(IntFunction<A[]>)
 └── GenreRepository.getAllById(Long[])
     └── GenreRepositoryJdbc.getAllById(Long[])
 └── List.size()
     └── ...
 └── BookService.addGenre(Book, Genre)
     └── BookServiceImpl.addGenre(Book, Genre)
         ├── Book.java
         ├── ArrayList.ArrayList()
         ├── List.contains(Object)
         │   ├── contains(Object) in SingletonList in Collections
         │   ├── contains(Object) in CopiesList in Collections
         │   ├── FastList.contains(Object)
         │   ├── XSObjectListImpl.contains(Object)
         │   ├── AutoPopulatingList.contains(Object)
         │   ├── Vector.contains(Object)
         │   ├── ArrayList.contains(Object)
         │   └── ...
         └── ResourceAlreadyExistsException.ResourceAlreadyExistsException(String)
             └── RuntimeException.RuntimeException(String)
 └── Iterable.forEach(Consumer<? super T>)
     └── ...
 └── BookService.save(Book)
     └── BookServiceImpl.save(Book)
         └── ResponseEntity.ResponseEntity(HttpStatusCode)
```


---
# insert

```scss
BookInsertUseCase.execute(Book)
 └── BookInsertUseCaseImpl.execute(Book)
     ├── Book.java (2 usages)
     ├── BookService.getByIsbn(String)
     │   └── BookServiceImpl.getByIsbn(String)
     ├── Optional.isPresent()
     ├── ResourceAlreadyExistsException.ResourceAlreadyExistsException(String)
     │   └── RuntimeException.RuntimeException(String)
     └── BookRelationHandlerImpl.resolveRelations(Book)
         ├── Book.java (2 usages)
         ├── Publisher.java
         ├── PublisherService.getById(Long)
         │   └── PublisherServiceImpl.getById(Long)
         ├── Publisher.java
         ├── ResourceNotFoundException.ResourceNotFoundException(String) (2 usages)
         │   └── RuntimeException.RuntimeException(String)
         ├── Optional.orElseThrow(Supplier<? extends X>) (2 usages)
         ├── Book.java
         ├── Book.java (2 usages)
         ├── Category.java (2 usages)
         ├── CategoryService.getById(Long)
         │   └── CategoryServiceImpl.getById(Long)
         ├── Book.java
         ├── Book.java
         ├── AuthorService.getAllById(List<Author>)
         │   └── AuthorServiceImpl.getAllById(List<Author>)
         ├── Book.java
         ├── Book.java
         └── GenreService.getAllById(List<Genre>)
             └── GenreServiceImpl.getAllById(List<Genre>)
 └── BookService.save(Book)
     └── BookServiceImpl.save(Book)
         └── BookRepository.save(Book)
             └── BookRepositoryJdbc.save(Book)
                 ├── Book.java
                 ├── GenericDaoDb.update(T)
                 │   ├── PublisherDaoJdbc.update(Publisher)
                 │   ├── CategoryDaoJdbc.update(Category)
                 │   ├── BookDaoJdbc.update(Book)
                 │   ├── AuthorDaoJdbc.update(Author)
                 │   ├── BaseDaoJdbc.update(T)
                 │   └── GenreDaoJdbc.update(Genre)
                 ├── GenericDaoDb.insert(T)
                 │   ├── BookDaoJdbc.insert(Book)
                 │   ├── CategoryDaoJdbc.insert(Category)
                 │   ├── PublisherDaoJdbc.insert(Publisher)
                 │   ├── AuthorDaoJdbc.insert(Author)
                 │   ├── BaseDaoJdbc.insert(T)
                 │   └── GenreDaoJdbc.insert(Genre)
                 ├── Book.java
                 └── GenericDaoCache.clearCache()
                     └── BookDaoCacheImpl.clearCache()
ResponseEntity.ResponseEntity(HttpStatusCode) (org.springframework.http)
```


---
# update

```scss
BookUpdateUseCaseImpl.execute(Book)
 ├── Book.java (2 usages)
 ├── BookService.getById(long)
 │   └── BookServiceImpl.getById(long)
 │       └── BookRepository.getById(long)
 │           └── BookRepositoryJdbc.getById(long)
 │               └── GenericDaoDb.getById(long)
 │                   ├── GenreDaoJdbc.getById(long)
 │                   │   └── BaseDaoJdbc.getById(long)
 │                   ├── PublisherDaoJdbc.getById(long)
 │                   │   └── BaseDaoJdbc.getById(long)
 │                   ├── BaseDaoJdbc.getById(long)
 │                   │   ├── EntityMetadataExtractor.getSelectTable()
 │                   │   ├── BaseDaoJdbc.queryForOptional(String, Object...)
 │                   │   ├── GenreDaoJdbc.getById(long)
 │                   │   ├── PublisherDaoJdbc.getById(long)
 │                   │   ├── BookDaoJdbc.getById(long)
 │                   │   ├── AuthorDaoJdbc.getById(long)
 │                   │   └── CategoryDaoJdbc.getById(long)
 │                   └── BookDaoJdbc.getById(long)
 │                       └── BaseDaoJdbc.getById(long)
 │                   ├── AuthorDaoJdbc.getById(long)
 │                   │   └── BaseDaoJdbc.getById(long)
 │                   └── CategoryDaoJdbc.getById(long)
 │                       └── BaseDaoJdbc.getById(long)
 ├── Optional.isEmpty()
 ├── ResourceNotFoundException.ResourceNotFoundException(String)
 │   └── RuntimeException.RuntimeException(String)
 └── BookRelationHandlerImpl.resolveRelations(Book)
     ├── Book.java (2 usages)
     ├── Publisher.java
     ├── PublisherService.getById(Long)
     │   └── PublisherServiceImpl.getById(Long)
     ├── Publisher.java
     ├── ResourceNotFoundException.ResourceNotFoundException(String) (2 usages)
     │   └── RuntimeException.RuntimeException(String)
     ├── Optional.orElseThrow(Supplier<? extends X>) (2 usages)
     ├── Book.java
     ├── Book.java (2 usages)
     ├── Category.java (2 usages)
     ├── CategoryService.getById(Long)
     │   └── CategoryServiceImpl.getById(Long)
     ├── Book.java
     ├── Book.java
     ├── AuthorService.getAllById(List<Author>)
     │   └── AuthorServiceImpl.getAllById(List<Author>)
     ├── Book.java
     ├── Book.java
     └── GenreService.getAllById(List<Genre>)
         └── GenreServiceImpl.getAllById(List<Genre>)
 └── BookService.save(Book)
     └── BookServiceImpl.save(Book)
         └── BookRepository.save(Book)
             └── BookRepositoryJdbc.save(Book)
                 ├── Book.java
                 ├── GenericDaoDb.update(T)
                 │   ├── PublisherDaoJdbc.update(Publisher)
                 │   ├── CategoryDaoJdbc.update(Category)
                 │   ├── BookDaoJdbc.update(Book)
                 │   ├── AuthorDaoJdbc.update(Author)
                 │   ├── BaseDaoJdbc.update(T)
                 │   └── GenreDaoJdbc.update(Genre)
                 ├── GenericDaoDb.insert(T)
                 │   ├── BookDaoJdbc.insert(Book)
                 │   ├── CategoryDaoJdbc.insert(Category)
                 │   ├── PublisherDaoJdbc.insert(Publisher)
                 │   ├── AuthorDaoJdbc.insert(Author)
                 │   ├── BaseDaoJdbc.insert(T)
                 │   └── GenreDaoJdbc.insert(Genre)
                 ├── Book.java
                 └── GenericDaoCache.clearCache()
                     └── BookDaoCacheImpl.clearCache()
ResponseEntity.ResponseEntity(HttpStatusCode) (org.springframework.http)
```


---
# delete

```scss
BookDeleteUseCase.execute(long)
 └── BookDeleteUseCaseImpl.execute(long)
     ├── BookService.getById(long)
     │   └── BookServiceImpl.getById(long)
     │       └── BookRepository.getById(long)
     │           └── BookRepositoryJdbc.getById(long)
     │               └── GenericDaoDb.getById(long)
     │                   ├── GenreDaoJdbc.getById(long)
     │                   │   └── BaseDaoJdbc.getById(long)
     │                   ├── PublisherDaoJdbc.getById(long)
     │                   │   └── BaseDaoJdbc.getById(long)
     │                   ├── BaseDaoJdbc.getById(long)
     │                   │   ├── EntityMetadataExtractor.getSelectTable()
     │                   │   ├── BaseDaoJdbc.queryForOptional(String, Object...)
     │                   │   ├── GenreDaoJdbc.getById(long)
     │                   │   ├── PublisherDaoJdbc.getById(long)
     │                   │   ├── BookDaoJdbc.getById(long)
     │                   │   ├── AuthorDaoJdbc.getById(long)
     │                   │   └── CategoryDaoJdbc.getById(long)
     │                   └── BookDaoJdbc.getById(long)
     │                       └── BaseDaoJdbc.getById(long)
     │                   ├── AuthorDaoJdbc.getById(long)
     │                   │   └── BaseDaoJdbc.getById(long)
     │                   └── CategoryDaoJdbc.getById(long)
     │                       └── BaseDaoJdbc.getById(long)
     ├── ResourceNotFoundException.ResourceNotFoundException(String)
     │   └── RuntimeException.RuntimeException(String)
     ├── Optional.orElseThrow(Supplier<? extends X>)
     └── BookService.delete(long)
         └── BookServiceImpl.delete(long)
             └── BookRepository.delete(long)
                 └── BookRepositoryJdbc.delete(long)
                     └── GenericDaoDb.delete(long)
                         ├── BaseDaoJdbc.delete(long)
                         ├── GenreDaoJdbc.delete(long)
                         ├── BookDaoJdbc.delete(long)
                         ├── PublisherDaoJdbc.delete(long)
                         ├── CategoryDaoJdbc.delete(long)
                         └── AuthorDaoJdbc.delete(long)
                     └── GenericDaoCache.clearCache()
                         └── BookDaoCacheImpl.clearCache()
ResponseEntity.ResponseEntity(HttpStatusCode) (org.springframework.http)
```

