# Registro de Errores

Completar una fila por cada error detectado.

| N | Archivo | Problema encontrado | Como lo detectaron | Solucion aplicada |
|---|---------|---------------------|--------------------|-------------------|
| 1 | src/ejemplo.js | El token no se verificaba | Prueba manual de ruta protegida | Se uso jwt.verify con manejo de excepcion |

## Guia de calidad para el informe

No alcanza con escribir "habia un error y lo arreglamos".

En cada caso expliquen:

1. Que ocurria.
2. Por que ocurria.
3. Como se soluciono.
4. Como validaron que quedo funcionando.

| N | Archivo | Problema encontrado | Como lo detectaron | Solucion aplicada |
|---|---------|---------------------|--------------------|-------------------|
|1  |src/app.js| no podia leer el body que pasaba por postman debido a que no se usaba express| lei la devolucion del postman | app.use(express.json()) 
|2  |src/utils/token.js| no se exportaba el sign token| cuando mandaba el request me decia que no se encontraba el signToken, por ende o no se exportaba el signToken o no se importaba bien, el import (require) era correcto, entonces habia un error en el export | faltaba una 's' en el .export
|3  |src/data/db.js| agregue un mensaje distinto en los return del login para distinguir en en que condicional entraba, asi me di cuenta que no habia ningun user a pesar de que lo haya registrado, entonces hay algo que pasa en el registrarse que no actualiza la lista de usuarios, al tener el users.push el registrarse considere que haya un error con la lista en si. Me di cuenta que era una constante asi que la cambie para que se pueda actualizar | cambie el const por un let|
|4  |src/controllers/authController.js | ahora fallaba al entrar al condicional del match, diciendo que no hay un match. Justo arriba de esa funcion se declaraba match, por ende el error debia ser ahi. googlee como funciona el bcrypt.compare y me di cuenta que es estrictamente posicional, quiere decir que primero si o si tiene que ir la contraseña y luego la que tengo guardada en users | intercambie el orden de los parametros|
|5  |src/controllers/userController.js| decia que no podia leer lo que se le pasaba | cambie req.USERS.id por req.body.id porque se lo paso por body, luego me fije de que no encontraba un usuario, lo cual era raro, por algun motivo no encontraba el id, me di cuenta que tenia una comparacion de triple igual, entonces debia ser de que postman pasaba un string y yo tenia guardado el id tipo int y al no ser exactamente iguales no lo encontraba | elimine un ´=´ para que discrimine el tipo de dato
|6 |src/controllers/userController.js| me decia que no encontraba el usuario, tenia el mismo error del exactamente igual. despues de solucionar ese error aparecia de que no se cambiaba el nombre y me di cuenta que era porque la variable estaba entre llaves, lo que me llamaba la atencion | elimine un '=' y elimine las llaves del const name
