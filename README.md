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
## Deploy Heroku: https://soy-glucosa-project.herokuapp.com/
- El package.json en el directorio root se utiliza para el deploy en Heroku. Instruye en heroku que primero debe entrar al directorio de react y hacer el build de la app, y luego debe ir al directorio del server a iniciar el servidor, el cual esta configurado con el modelo Data on Wire, las rutas para renderizar vistas apuntan al build de React.
- La capa de server esta diseñada para enviar todas las peticiones que no conoce al directorio donde esta el build de react.
## Desarrollo: 
- Cada directorio (client-react y server-express) tiene su package.json
- En el directorio de client-react, las instrucciones npm start y npm build funcionan como en cualquier proyecto de react. Inicia la app en el puerto 3000. Tener en cuenta que no hay proxy configurado, no se puede iniciar el server por un lado y react por otro porque los endpoints no van a funcionar.
- En el directorio server-express hay varias configuraciones; npm start inicia el servidor en el puerto 5000. npm run start-build hace el build de react y luego inicia el servidor en el puerto 5000.
