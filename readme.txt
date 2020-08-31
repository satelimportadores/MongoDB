Iniciar el servidor
mongod.exe --dbpath D:\mongodb\data\db

Abrir shell mongo
cd C:\Program Files\MongoDB\Server\3.6\bin
mongo

mostrar bases de datos:
show dbs

crear base de datos:
use misclientes

Crear usuario:
db.createUser({user: 'Juan',pwd: '123',roles: ['readWrite','dbAdmin']})

