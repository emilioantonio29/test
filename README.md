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
## GraphQL:
```javascript
    {
        "items": [
            {
                "cantidadComprada": 5,
                "nombre": "Golfeado",
                "categoria": "Golfeados",
                "stockAfterBuy": 25,
                "precio": 220,
                "id": "21qS0AUU1VZm8UHE8OLz"
            }, 
            {
                "precio": 260,
                "id": "6Ir5RjW68DwzlSfjoMtm",
                "categoria": "Mermeladas",
                "cantidadComprada": 4,
                "stockAfterBuy": 8,
                "nombre": "Mermelada de Naranja"
            }],
        "comprador": {
            "nombre": "POSTMAN TEST",
            "telefono": "8484848",
            "email": "POSTMANTEST@test.com"
            },
        "date": {
            "_seconds": 1616461155,
            "_nanoseconds": 478000000
            },
        "total": 2140
    }
```
```javascript
    put  /apiFirebase/productos   | actualiza stock de un producto    | no se utiliza en el Front | se puede probar con postman. Ejemplo (Golfeado):
    
    https://soy-glucosa-project.herokuapp.com/apiFirebase/productos

    {
        "id": "21qS0AUU1VZm8UHE8OLz",
        "cantidad": 50
    }
```
```javascript
    put  /apiFirebase/actualizar20| actualiza a 20 todos los stock    | no se utiliza en el Front | se puede probar con postman. Ejemplo:    
    
    https://soy-glucosa-project.herokuapp.com/apiFirebase/actualizar20
```
```javascript
    post /apiMongo/registro       | graba un user en mongoAtlas       | se utiliza en el Front    | se puede probar con postman. Ejemplo:
    
    https://soy-glucosa-project.herokuapp.com/apiMongo/registro                                   | Dispara un mail a la casilla username

    {
        "nombre": "Name Postman",
        "apellido":"Lastname Postman",
        "username": "testpostman@test.com",
        "password": "12345",
        "provincia": "provinciaString",
        "localidad": "localidadString",
        "calle": "calleString",
        "altura": "alturaString",
        "zip": "zipString",
        "telefono": "telefonoString",
        "tyc": true,
        "fecha": "2022-03-11T00:45:39.157Z"
    }
```
```javascript
    post /apiMongo/login          | envia user/pass y valida user     | se utiliza en el Front    | se puede probar con postman. Ejemplo:     
    
    https://soy-glucosa-project.herokuapp.com/apiMongo/login

    {
        "username": "probarConUserReal@test.com",
        "password": "1234"
    }
```
```javascript
    post /apiMongo/recovery       | envia mail de recupero            | se utiliza en el Front    | se puede probar con postman. Ejemplo:
    
    https://soy-glucosa-project.herokuapp.com/apiMongo/recovery                                   | Dispara un mail a la casilla username con la pass

    {
        "username": "probarConUserReal@test.com"
    }
```
```javascript
    get  /apiMongo/logout         | destruye la sesion                | se utiliza en el Front    | se puede probar con postman     
```
```javascript
    get  /apiMongo/user           | verifica si hay una sesion creada | se utiliza en el Front        
```
- Revisar el resto de los endpoints en la capa ROUTES.

## Endpoints GraphQL: 
- La interfaz del browser esta deshabilitada. Solo se pueden probar desde postman.
- Los endpoints graphQL pegan a las mismas bases de datos (mongo y firestore). Se hizo un desarrollo especifico de graphQL en la siguiente rama: https://github.com/emmartinez29/Coder_Backend/tree/KoaFramework_ApiGrapQL
- Se hizo deploy de los endpoints de graphQL en otro proyecto de Heroku: https://soy-glucosa-project-apigraphql.herokuapp.com/
- NOTA: No habilitar interfaz del browser en este proyecto. Escribeme y te digo el motivo :)

    Endpoint de ordenes: root

    El schema de graphQL tiene 3 metodos:

    1.- mutation para grabar una orden
    2.- query para obtener el listado completo de ordenes realizadas
    3.- query para obtener el listado completo de ordenes de un usuario (se le pasa el mail del comprador)
```javascript
    1) Grabar una orden: la orden se graba en firestore con 4 parametros
    - Un array de items; cada item tiene los 6 parametros que se muestran en el ejemplo.
    - El objeto comprador.
    - El objeto Date.
    - El total de la compra.
    - Despues de grabar una orden, el endpoint te devuelve el nro de orden (doc de la collection en firestore).

    Ejemplo:        
```
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
