## EXAMEN DE RECUPERACIÓN DEL 2º TRIMESTRE DEL MÓDULO DE ACCESO A DATOS

En este examen de recuperación deberás demostrar que has adquirido las destrezas 
suficientes para poner en marcha una API REST, para configurar una serie de endpoints básicos,
de implementar lógica de negocio básica y de gestionar los posibles errores que se generen en la API.

# 1. Puesta en marcha del proyecto

Deberás configurar los siguientes aspectos:
- **Generación de llaves pública y privada**: Genera las llaves pública y privada que servirán como mecanismo de encriptación y desencriptación del token JWT
- **Generación de URI de conexión a MongoDB**: Establece una URI de conexión para conectarte a MongoDB. Esta URL deberá estar en un fichero .env.properties obligatoriamente y se llamará *MONGO_URI*.

# 2. Entidades y DTOs
- **Usuario**: Crea una entidad usuario con los siguientes campos:
  - id: String -> Clave primaria de la colección
  - username: String -> (obligatorio y **único**)
  - password: String -> entre 5 y 20 caracteres (obligatorio)
  - roles: String -> por defecto a "USER"
  - fecha_creacion: LocalDateTime -> por defecto la fecha y hora de hoy
- **Reserva**: Crea una entidad reserva con los siguientes campos:
  - id: String -> Clave primaria de la colección
  - titulo: String -> (obligatorio)
  - descripcion: String
  - fecha_reserva: LocalDateTime -> (obligatorio)
  - fecha_fin_reserva: LocalDateTime
  - username: String -> identificador del usuario al que pertenece la reserva
- **DTOs**: Deberás crear los DTOs necesarios para cada caso.

# 2. Gestión de usuarios
Deberás realizar los endpoints siguientes para controlar la gestión de usuarios:
- **Login**: Realiza un endpoint de login que devuelva un token JWT si el login es exitoso.
- **Registro**: Realiza un endpoint de registro de usuario con las siguientes restricciones:
  - El campo **username** es único en la colección.
  - El campo **password** deberá tener entre 5 y 20 carácteres, y sólo puede contener valores alfanuméricos (es decir, sólo letras y números)
  - El campo **roles** se pone por defecto a "USER" y el único valor diferente permitido es "ADMIN"
  - El campo **fecha_creacion** se pone por defecto al día y hora de hoy.

# 3. Gestión de reservas
Deberás realizar los endpoints siguientes para controlar la gestión de reservas:
- **Realizar una reserva**: Realiza un endpoint para dar de alta una reserva en el sistema con las siguientes restricciones:
  - El campo **titulo** es obligatorio
  - El campo **fecha_reserva** es obligatorio y no puede ser anterior al día de hoy.
  - El campo **fecha_fin_reserva** es opcional.
    - Si el campo viene relleno, la *fecha_fin_reserva* no puede ser anterior al campo *fecha_reserva*
    - Si el campo viene vacío, la *fecha_fin_reserva* se pondrá a 2 semanas a partir del día de hoy.
  - El campo **username** es opcional para usuarios con rol "USER" y obligatorio para usuarios con rol "ADMIN"
    - Si el usuario que realiza la petición es tiene rol "ADMIN", el campo *username* es obligatorio y vendrá en el DTO.
    - Si el usuario que realiza la petición tiene el rol "USER", el campo es opcional y este campo vendrá dado por el token JWT.
- **Eliminar una reserva**: Realiza la eliminación de una reserva por su **id**.

# 4. Restricciones de acceso
Deberás implementar una serie de restricciones de acceso a los diferentes endpoints:
- **Login** -> libre acceso al endpoint
- **Registro** -> libre acceso al endpoint
- **Realizar una reserva** -> el usuario debe estar autenticado
- **Eliminar una reserva** -> el usuario debe tener rol "ADMIN"

# 5. Gestión de errores
La API deberá controlar los errores correctamente bajo una clase con la anotación **@ControllerAdvice**

# APROBAR EL EXAMEN
Para aprobar el exámen deberán estar terminados todos los endpoints ya que no son muchos y son cosas que ya hemos hecho en clase muchas veces.
Entrega un pantallazo con Insomnia de las pruebas de cada endpoint para probar que se ha realizado correctamente.

# NO SE PUEDE USAR CHATGPT
Puedes consultar código propio y buscar por internet lo que quieras. Pero QUEDA TOTALMENTE PROHIBIDO EL USO DE CHATGPT. 
Si se identificara el uso de esta herramienta durante cualquier momento del exámen, este quedará directamente anulado.

