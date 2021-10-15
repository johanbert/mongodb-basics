En el disco local C debemos crear una carpeta llamada data. Dentro de esta carpeta crearemos una carpeta llamada db.
Es acá donde se guardarán todas nuestras bases de datos, colecciones y documentos.


Usaremos dos terminales de consola. La primera se encargará de levantar el servidor, la segunda de levantar el cliente

Levantamiento del Servidor - Daemon
Start up MongoDb

"C:\Program Files\MongoDB\Server\4.2\bin\mongod.exe" --dbpath="c:\data\db"



Levantamiento del Cliente
"C:\Program Files\MongoDB\Server\4.2\bin\mongo.exe"


También podemos configuar ambos comandos como variables de entorno.



COMANDOS:
show dbs
use nombreDB
db.createCollection('nombreColeccion')
show collections
db.getCollection('nombreColeccion').find()
db.nombreColeccion.find()
db.nombreColeccion.findOne()
db.nombreColeccion.findOne( { nombre: "Luis" })
db.nombreColeccion.find( {edad: { $ne: 21 } })
db.nombreColeccion.find( {}, { nombre:1 } )


CAMBIAR DE BD
 use fullstackPM
switched to db fullstackAPM

//Al momento de realizar este cambio de BD, si dicha BD no existe se creará automáticamente.




CREAR DOCUMENTO
documento =  hace referencia a una variable que almacena el objeto que queremos guardar en nuestra bd 

documento = {nombre: "Kamilo", edad:28, fecha: new Date()}
{
        "nombre" : "Kamilo",
        "edad" : 28,
        "fecha" : ISODate("2019-06-04T01:38:44.310Z")
}


El objeto new Date() devuelve de manera exacta la fecha y hora con los milisegundos.



AGREGAR DOCUMENTO EN COLECCIÓN
//db.colección.insert(documento)

// Al no existir la colección, ésta se crea automáticamente cuando se inserte el documento.
db.clase.insert(documento)
WriteResult({ "nInserted" : 1 })





-- COMO FUNCIONA EL ID --
Si no existe el id lo crea, si existe, lo trata de manera única.
El id puede ser ObjectId o de cualquier tipo de dato que queramos

variable = {_id: "texto", clave: valor}

Siempre va _id

Crear id

new ObjectID()
tiene un string de 24 caracteres, 12bits representado en un string alfanúmerico
primeros 4 bytes = timespan
3 bytes = identificador único de la maquina
2 bytes = hash proceso actual
4 bytes = numero autoincrementable propio de mongo

Ya es un atributo indexado







AGREGAR MULTIPLES DOCUMENTOS
uno = {nombre: "Juan", edad: 30}
dos = {nombre: "Pepe", edad: 30}
tres = {nombre: "Carlos", edad: 30}


 db.cursos.insert( [uno, dos, tres] )
BulkWriteResult({
        "writeErrors" : [ ],
        "writeConcernErrors" : [ ],
        "nInserted" : 3,
        "nUpserted" : 0,
        "nMatched" : 0,
        "nModified" : 0,
        "nRemoved" : 0,
        "upserted" : [ ]
})





CONSULTAR EN QUÉ BD ESTAMOS UBICADOS
 db
fullstackPM


CONSULTAR COLECCIONES DE LA BD
 show collections
clase


CONSULTAR TODAS LAS BASES DE DATOS
 show databases
local
admin
config
test (oculta)
fullstackPM





TRAER TODOS LOS DOCUMENTOS DE UNA COLECCIÓN
//db.coleccion.find()
db.clases.find()
{ "_id" : ObjectId("5cf5cedc5fd3d1626639e929"), "nombre" : "Pepe", "edad" : "19" }
{ "_id" : ObjectId("5cf5d0a35fd3d1626639e92a"), "nombre" : "Juanito" }




CONDICONALES DE BÚSQUEDA
Encontrar un solo dato
//db.coleccion.findOne()
//db.coleccion.findOne( {condicion} )


Encontrar un dato específico
//db.coleccion.find( {condicion} )
db.cursos.find( {nombre: "Pepe"} )

NOT
Se buscarán todos los datos que no sean similares a los que se especifiquen en la condición
//db.colección.find( {condicion: {$ne: negacion} })
 db.cursos.find( {edad: {$ne:"20"} } )
{ "_id" : ObjectId("5cf5cedc5fd3d1626639e929"), "nombre" : "Pepe", "edad" : "19" }
{ "_id" : ObjectId("5cf5d0a35fd3d1626639e92a"), "nombre" : "Juanito" }
{ "_id" : ObjectId("5cf5cedc5fd3d1626639e929"), "nombre" : "Pepe", "edad" : "19" }





TRAER LOS CAMPOS CON LOS QUEREMOS TRABAJAR
1 = true / 0 = false
db.notas.find( {}, {nombre:1} )
{ "_id" : ObjectId("5cf7384d6ff8ad024d1eab58"), "nombre" : "Juan" }
{ "_id" : ObjectId("5cf7384d6ff8ad024d1eab59"), "nombre" : "Maria" }
{ "_id" : ObjectId("5cf7384d6ff8ad024d1eab5a"), "nombre" : "jose" }
{ "_id" : ObjectId("5cf7384d6ff8ad024d1eab5b"), "nombre" : "mario" }