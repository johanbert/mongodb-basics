# MongoDB
	-> Base de Datos No relacional (NoSQL)
	-> Se basa en el lenguaje de JavaScript
	-> Open Source
	-> Es una base de datos flexible
	-> Formato BSON (Binary JSON)

## ¿Qué quiere decir NoSQL?
	Su formato no corresponde al formato tradicional de tablas como lo hace una bd relacional
	como SQL, MySQL etc. Al no existir tablas tampoco existen las relaciones (MER).

	{
		"_id": ObjectID(asdfghjkirew34567ikjh),
		"nombreSerie": "Los Simpsons",
		"temporadas": [
			{
				"temporada1": 20cap,
				"duracionCap": 20min,
				"tiempoEspera": 1año
			},
			{
				"temporada2": 20cap
			}
		]
	}


	{
		"_id": ObjectID(213456789kjhgwascvbji),
		"nombreSerie": "Rick & Morty",
		"temporadas": [
			{
			"temporada1": 10cap
			}
		]
	}


	Al no tener la estructura de tablas, en una bd NoSQL como Mongo, estas se llaman colecciones
	y a cada registro existente, en Mongo se le conoce como documento.
    
    Bases de Datos NO RELACIONALES: MongoDB, Firebase de Google, DynamoDB de AWS (Amazon Web Services).

	Como no existe una relación entre tablas, Mongo las reemplaza por medio de anidación de Json.
	Esto se le conoce como subdocumento.

	Al no existir tablas, mongo maneja los documentos por medio de JSON, dejando de lado que existan datos con valor null a menos que nosotros lo deseemos.

¿Quiénes utilizan Mongo?
	Ebay
	Nokia
	Netflix
	Sega
	Telefónica
	Adobe
	EA sports

El id de Mongo, se genera automáticamente cuando existe un registro. Nosotros podemos crear nuestros
propios ID pero el id que genera mongo por defecto ya consta de un string de 24 caracteres
alfanuméricos o 12 bytes.  _id: ObjectID()

4 -> timespan
3 -> proceso interno de la máquina
2 -> hash (encriptación)
3 -> dato autoincrementable de Mongo
Total = 12 bytes

En el disco local C se debe crear una carpeta llamada data y dentro de esta carpeta se debe crear una
carpeta llamada db. Acá es donde se guardarán los bson de nuestra bd Mongo

Disco C
	|__ data
		|__ db


Usaremos dos terminales (dos consolas):
	La primera se encargará de levantar el servidor de Mongo.
		el servidor de mongo, lo provee el ejecutable mongod.exe
		d - Daemon: Demonio
	La segunda se encargará de levantar el cliente de Mongo.
		el cliente de mongo, lo provee el ejecutable mongo.exe

Entornos de Mongo
	MongoCompass
	MongoAtlas
	Robo 3T


## ---------- CREAR BD --------------------
``` use fullstack ```
switched to db fullstack
al hacer uso de este comando, si la base de datos no existe, se crea automáticamente con el primer
documento que se inserte

## ---------- CONSULTAR BD --------------------
``` show dbs ```
fullstack
admin
config
local

## ---------- CONSULTAR COLECCIONES --------------------
debemos estar ubicados en la base de datos que deseemos
``` show collections ```

## ---------- INSERTAR DOCUMENTO --------------------
podemos guardar los json en una variable y pasarlo como parámetro del método insert()
``` variable = {nombre: "Pepe"} ```
``` db.prueba.insert(variable) ```
Aqui si no existe la collection, la crea y hace la inserción

podemos pasar directamente como parámetro el json al método insert()
``` db.prueba.insert( {nombre: "Perengano"} ) ```
``` Respusta de BD:  WriteResult( {"nInserted" : 1 } ) ```

Siempre al interactuar con insertar, consultar, actualizar y eliminar
debemos indicar 
``` db.coleccion.metodo() ```

Al no existir la colección, se creará automáticamente con el primer documento insertado

## ---------- INSERTAR MÚLTIPLES DOCUMENTOS --------------------

Lo ideal es guardar cada json en variables y enviar como parámetro al método insert() un arreglo con estas variables
``` uno = {nombre: "Lorena"} ```
``` dos = {nombre: "Carlos"} ```
``` tres = {nombre: "Duván"} ```

``` db.prueba.insert( [uno, dos, tres] ) ```

BulkWriteResult( {
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 3,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0, 
	"nRemoved" : 0, 
	"upserted" : [ ] 
} )

## OBTENER TODOS LOS DOCUMENTOS DE UNA COLECCIÓN 
``` db.prueba.find().pretty() ```

## OBTENER DOCUMENTOS ESPECIFICO 
``` db.prueba.find( {nombre: "Pepe"} ).pretty() ```

## OBTENER DOCUMENTOS DISTINTOS A UNA CONDICIÓN 
A partir del operador $ne indicamos que nos traiga todos los documentos de la colección que no sean iguales a
``` db.prueba.find( {nombre: {$ne: "Pepe"} } ).pretty() ```