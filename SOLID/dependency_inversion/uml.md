classDiagram

%% =========================
%% DIP VIOLATED
%% =========================

class UserService {
    -sqlDb : MySQLDatabase
    -mongoDb : MongoDBDatabase
    +storeUserToSQL(user : String) void
    +storeUserToMongo(user : String) void
}

class MySQLDatabase {
    +saveToSQL(data : String) void
}

class MongoDBDatabase {
    +saveToMongo(data : String) void
}

UserService *-- MySQLDatabase : tightly coupled
UserService *-- MongoDBDatabase : tightly coupled

%% =========================
%% DIP FOLLOWED
%% =========================

class Db {
    <<interface>>
    +save_to_db(data : String) void
}

class SAVE_SQL {
    +save_to_db(data : String) void
}

class SAVE_MDB {
    +save_to_db(data : String) void
}

class App {
    -db : Db
    +main() void
}

Db <|.. SAVE_SQL
Db <|.. SAVE_MDB
App --> Db : uses abstraction

note for UserService
"VIOLATION:
High-level module depends
directly on concrete classes.
Any new database requires
modification in UserService."
end note

note for App
"FOLLOWED:
High-level module depends
only on Db abstraction.
Database implementations
can be swapped easily."
end note