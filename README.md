## Test Readme
```javascript
    _________    _____________________________________________________    ______________
    |       | -> |                     BACK                          | -> |  DBs       |
    | front |    |                                 ________________  |    |            |
    |       | <- |   ------    ------    ------    |  ----- ----- |  | <- | mongoAtlas |
    ---------    |   |    | -> |    | -> |    | -> |  |   | |   | |  |    | firestore  |
                 |   |    |    |    |    |    |    |  | c | | m | |  |    --------------
                 |   |____| <- |____| <- |____| <- |  |___| |___| |  |
                 |                                 |______________|  |
                 |   routes  controller  service          DAO        |
                 ---------------------------↑-------------------------
                            ↓       ↑       |_________
                    --------------------------        ↓         
                    |                        |     ---------
                    |       TEST LAYER       |     |mailing|
                    |________________________|     |_______|                 
```
## Title
- text
- text
## Endpoints GraphQL:    
```javascript
    mutation{
        addOrden(
            comprador: {
                nombre: "GRAPHQL TESTING",
                telefono: "8484848",
                email: "GRAPHQLTESTING@hotmail.com"
            },
            items: [
            {
                cantidadComprada: 5,
                nombre: "Golfeado",
                categoria: "Golfeados",
                stockAfterBuy: 25,
                precio: 220,
                id: "21qS0AUU1VZm8UHE8OLz"
            }, 
            {
                precio: 260,
                id: "6Ir5RjW68DwzlSfjoMtm",
                categoria: "Mermeladas",
                cantidadComprada: 4,
                stockAfterBuy: 8,
                nombre: "Mermelada de Naranja"
            }],
            date: {
                _seconds: 1616461155,
                _nanoseconds: 478000000
            },
            total: 2140
        )
        {
            id
        }
    }       
```
```javascript
    query{
        orders{
        id,
        comprador{
            nombre,
            email,
            telefono
        },
        date{
            _seconds,
            _nanoseconds
        },
        items{
            cantidadComprada,
            nombre,
            categoria,
            stockAfterBuy,
            precio,
            id
        },
        total
        }
    }      
```
```javascript
    query{
        ordersByUser(email: "emilio_antonio29@hotmail.com")
        {
            id,
            comprador{
                nombre,
                email,
                telefono
            },
            date{
                _seconds,
                _nanoseconds
            },
            items{
                cantidadComprada,
                categoria,
                precio,
                nombre,
                id,
                stockAfterBuy,
            }
            total
        }
    } 
```
## Title:
- text
- text
- test2
