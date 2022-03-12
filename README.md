## Arquitectura: 
- Frontend: React | directorio client-react
- Backend: Node JS - Express | directorio server-express 
- DBs: Mongo (usuarios) | Firestore (productos y compras)
- El backend tiene una arquitectura de 5 capas mas una adicional de test; server-routes-controllers-service-dao | test
- Se implementó el patron DAOS en la capa de persistencia
- La configuracion de envios de mails se consume desde la capa de servicios
- Para correr los TEST, ingresar al directorio del server y ejecutar npm run test: se prueba el endpoint de traer los productos y las conexiones a las bases de datos. Las pruebas estan desarrolladas en el index.test.js.

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
