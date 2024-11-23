# Peticiones y datos a enviar a la API

# getAll

*USER* -> localhost:8080/api/books <font color="#00b050">(Get)</font>
*ADMIN* -> localhost:8080/api/admin/books <font color="#00b050">(Get)</font>

# getByIsbn

*USER* -> localhost:8080/api/books/9780142424179 <font color="#00b050">(Get)</font>
*ADMIN* -> localhost:8080/api/admin/books/9780142424179 <font color="#00b050">(Get)</font>

# inserts 

*(Admin)* -> localhost:8080/api/admin/books <font color="#f79646">(Post)</font>

```json
# BODY
{
    "isbn": "0034",
    "titleEs": "Nuevo ",
    "titleEn": "New book",
    "synopsisEs": "Sinopsis nuevo libro",
    "synopsisEn": "Synopsis new book",
    "price": 12.30,
    "discount": 0.5,
    "cover": "nuevo_libro.jpg",
    "publisher": {
        "id": 2
    },
    "category": {
        "id": 4
    },
    "genres": [
        {
            "id": 1
        },
        {
            "id": 2
        }
    ],
    "authors": [
        {
            "id": 3
        },
        {
            "id": 4
        }
    ]
}
```

*Admin* -> localhost:8080/api/admin/books/88/authors <font color="#f79646">(Post)</font>
         localhost:8080/api/admin/books/88/genres <font color="#f79646">(Post)</font>

```json
# BODY
[
    {
        "id": 5
    }
]
```

# update

*Admin* -> localhost:8080/api/admin/books/8900 <font color="#4bacc6">(Put)</font>

```json
# BODY
{
    "id": 8900,
    "isbn": "0030",
    "titleEs": "hola",
    "titleEn": "hola",
    "synopsisEs": "hola presagios cuenta la historia de un ángel y un demonio que unen fuerzas para evitar el apocalipsis. Ambos han vivido en la Tierra durante siglos y se han encariñado con la humanidad, por lo que harán todo lo posible para detener el fin del mundo.",
    "synopsisEn": "hola Omens tells the story of an angel and a demon who team up to prevent the apocalypse. Both have lived on Earth for centuries and have grown fond of humanity, so they will do everything possible to stop the end of the world.",
    "price": 99,
    "discount": 2,
    "cover": "http://hola.cesguiro.es/books/9780060557912.jpg",
    "publisher": {
        "id": 1
    },
    "category": {
        "id": 1
    },
    "genres": [
        {
            "id": 1
        },
        {
            "id": 2
        }
    ],
    "authors": [
        {
            "id": 1
        },
        {
            "id": 2
        }
    ]
}
```

# delete

*Admin* -> localhost:8080/api/admin/books/89 <font color="#c0504d">(Delete)</font>

