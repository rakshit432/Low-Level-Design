# DSP VIOLATED

classDiagram

class MySQLDatabase{
    +saveToSQL(data : String)
}

class MongoDBDatabase{
    +saveToMongo(data : String)
}

class UserService{
    -MySQLDatabase sqlDb
    -MongoDBDatabase mongoDb
    +storeUserToSQL(user : String)
    +storeUserToMongo(user : String)
}

UserService --> MySQLDatabase : direct dependency
UserService --> MongoDBDatabase : direct dependency


 # DSP FOLLOWED

classDiagram

class Db{
    <<interface>>
    +save_to_db(data : String)
}

class SAVE_SQL{
    +save_to_db(data : String)
}

class SAVE_MDB{
    +save_to_db(data : String)
}

class App{
    -Db db
    +main()
}

Db <|.. SAVE_SQL
Db <|.. SAVE_MDB

App --> Db : depends on abstraction