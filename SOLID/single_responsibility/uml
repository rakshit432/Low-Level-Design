# Single Responsibility Principle (SRP)

## SRP Violated

```mermaid
classDiagram

class Product {
    +name
    +price
}

class ShoppingCart {
    +addProduct()
    +getProducts()
    +calculateTotal()
    +printInvoice()
    +saveToDatabase()
}

ShoppingCart o-- Product : contains
```

**Issue:** ShoppingCart handles cart logic, invoice printing, and database storage.

---

## SRP Followed

```mermaid
classDiagram

class Product {
    +name
    +price
}

class ShoppingCart {
    +addProduct()
    +getProducts()
    +calculateTotal()
}

class ShoppingCartPrinter {
    +printInvoice()
}

class ShoppingCartStorage {
    +saveToDatabase()
}

ShoppingCart o-- Product : contains
ShoppingCartPrinter --> ShoppingCart : uses
ShoppingCartStorage --> ShoppingCart : uses
```

**Benefit:**
- ShoppingCart → Cart management
- ShoppingCartPrinter → Invoice printing
- ShoppingCartStorage → Database operations

**SRP:** Each class has only one responsibility and one reason to change.