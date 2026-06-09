# Open Closed Principle (OCP)

## OCP Violated

```mermaid
classDiagram

class ShoppingCartStorage {
    +save(type, cart)
}

class ShoppingCart

ShoppingCartStorage --> ShoppingCart
```

**Problem:**

```text
save(type, cart)
{
    if(type == "SQL") ...
    else if(type == "Mongo") ...
    else if(type == "File") ...
}
```

Every new storage type requires modifying `ShoppingCartStorage`.

---

## OCP Followed

```mermaid
classDiagram

class ShoppingCart

class Persistence {
    <<interface>>
    +save(cart)
}

class SQLPersistence
class MongoPersistence
class FilePersistence

ShoppingCart --> Persistence

Persistence <|.. SQLPersistence
Persistence <|.. MongoPersistence
Persistence <|.. FilePersistence
```

**Benefit:**

```text
class RedisPersistence implements Persistence
{
    save(cart)
}
```

New functionality is added by creating a new class, without modifying existing code.