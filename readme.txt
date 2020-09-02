//Iniciar el servidor
mongod.exe --dbpath D:\mongodb\data\db

//Abrir shell mongo
cd C:\Program Files\MongoDB\Server\3.6\bin
mongo

//mostrar bases de datos:
show dbs

//crear base de datos:
use misclientes

//ver colecciones - "tablas"
show collections

//Crear usuario:
db.createUser({user: 'Juan',pwd: '123',roles: ['readWrite','dbAdmin']})

//Crear coleccion e insertar:
db.customers.insert({firstName: 'Isaac',last_Name: 'Asimov'})

//ver dato insertado:
db.customers.find()
/*{ "_id" : ObjectId("5f4e9d401ec7ee96d5c4505c"), "firstName" : "Isaac", "last_Nam
e" : "Asimov" }*/

//Insertar mas de un datos Arrays:
db.customers.insert([
	{firstName: 'Isaac02',last_Name: 'Asimov02'},
	{firstName: 'Isaac03',last_Name: 'Asimov03'},
	{firstName: 'Isaac04',last_Name: 'Asimov04'}
])

//Busqueda de datos
db.customers.find({firstName: 'Isaac04'})

//Editar y agregar datos nuevos:
db.customers.update(
	{firstName: 'Isaac'},
		{
			firstName:'Isaac01',
			last_Name: 'Asimov01',
			gender: 'Male'
		}
)

//Organizar mostar datos como objetos:
db.customers.find({firstName: 'Isaac01'}).pretty()

//Buscar y Modificar datos por ID:
db.customers.find({_id: ObjectId("5f4e9d401ec7ee96d5c4505c")})

db.customers.update(
	{_id: ObjectId("5f4e9d401ec7ee96d5c4505c")},
		{
			firstName: 'Isaac01',
			last_Name: 'Asimov01',
			gender: 'Male',
			profesion: 'Ingenier'
		}
)

	//Modificar solo un dato sin escribir todo de nuevo: $set
	db.customers.update(
		{_id: ObjectId("5f4e9d401ec7ee96d5c4505c")},
			{
				$set: {age: 45}
			}
		)
	
	//Incrementar o disminuir (...1,-1...) un dato ejemplo la edad: $int 
		db.customers.update(
		{_id: ObjectId("5f4e9d401ec7ee96d5c4505c")},
			{
				$inc: {age: 5}
			}
		)

	//Quitar el dato de un registro: $unset
		db.customers.update(
		{_id: ObjectId("5f4e9d401ec7ee96d5c4505c")},
			{
				$unset: {age: 1}
			}
		)
		
		//Cambiar el nombre $rename
		db.customers.update(
		{firstName: 'Isaac01'},
			{
				$rename: {'firstName':'primerNombre'}
			}
		)
		

	//Eliminar datos
	db.customers.remove(
		{firstName: "Isaac02"}
	)
	
		//Eliminar solo un dato de todos los que coinciden:
		db.customers.remove(
			{firstName: "Isaac"}, {justOne: true}
		)
		
//Busquedas Elavoradas:

	//Busqueda de nombre que cumplan con alguna de las condiciones: $or
	db.customers.find(
		{$or: [{firstName: "Elena"}, {firstName: "Isaac"}]}
	)
	
	//Buscar por otro atributo
	db.customers.fid(
		{gender: "male"}
	)
	
	//Buscar las personas que tengan mas de 40 años: $gt Grader Thant 
	db.customers.find(
		{age: {$gt: 40}}
	)
	
	//Buscar las personas que tengan menos de 40 años: $lt Less Thant 
	db.customers.find(
		{age: {$lt: 40}}
	)
	
	//Buscar las personas que esten dentro de un rango 30 y 90 años:
	db.customers.find(
		{age: {$gt: 30, $lt: 90}}
	)
	
	//Buscar en datos anidados
	db.customers.find(
		{"address.city": "Boston"}
	)
	
	//Buscar por expresiones regulares:
	db.customers.find(
		{name: {$regex: 'ston'}}
	)
	
//Ordenamiento sort:

	//Ordenar de menor a mayor
	db.customers.find().sort({lastName: 1})
	
	//Ordenar de mayor a menor
	db.customers.find().sort({lastName: -1})
	
	//Contar los datos "Registros"
	db.customers.find().count()
	
	//Contar todos los datos con genero:
	db.customers.find({gender: "male"}).count()
	
	//limitar las busquedas
		
		//Ver solo tres 3 datos:
		db.customers.find().limit(3)
		//Ver solo tres datos y ordenarlos:
		db.customers.find().limit(3).sort({lastName: -1})
	
	//Utilizar metodos de JavaScript
	
		//Recorrer todos los datos, esto devuelve un documento con datos:
		//se imprimira los nombre que encuentre.
		db.customers.find().forEach(function(doc) {
			print("Customer Name" + doc.firstName);
		})
		
//Interfaz grafica MongoBooster,RoboMongo
	
//Copias de seguridad:
	
	//Nos ubicamos en CMD en la carpeta donde queremos que quede
		mongodump
	//Se Crearan carpetas con el nombre de las bases de datos
	//Se crearan archivos de extencion bson y metadata
	
//Restaurar:

	//Se borrara una base de datos de pruebas:
		use mitiendavirtual
		show collections
		
			db.dropDatabase()
	
	//Se restaura y ubica en la carpeta superior donde esta el backup "dump"
		mongorestore 
		//Restaurar solo una bd
		mongorestore --db mitiendavirtual /dump/mitiendavirtual
		//Restaurar solo la collecion de una bd
		mongorestore --db mitiendavirtual --collection usuarios /dump/mitiendavirtual/usuarios.bson
		
	
	
		
	
		
	










