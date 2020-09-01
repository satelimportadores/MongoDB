//Iniciar el servidor
mongod.exe --dbpath D:\mongodb\data\db

//Abrir shell mongo
cd C:\Program Files\MongoDB\Server\3.6\bin
mongo

//mostrar bases de datos:
show dbs

//crear base de datos:
use misclientes

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



