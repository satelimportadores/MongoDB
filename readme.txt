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
		
	










