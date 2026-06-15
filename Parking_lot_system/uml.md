classDiagram

    %% Enums and Interfaces

    class DurationType {
        <<enumeration>>
        HOURS
        DAYS
    }

    class ParkingFeeStrategy {
        <<interface>>
        +calculateFee(vehicleType, duration, durationType) Double
    }

    class PaymentStrategy {
        <<interface>>
        +processPayment(amount) Void
    }

    %% Strategy Implementations

    class BasicHourlyRateStrategy {
        +calculateFee(vehicleType, duration, durationType) Double
    }

    class CreditCardPayment {
        +processPayment(amount) Void
    }

    class CashPayment {
        +processPayment(amount) Void
    }

    %% Vehicle Hierarchy

    class Vehicle {
        <<abstract>>
        -licensePlate : String
        -vehicleType : String
        -feeStrategy : ParkingFeeStrategy
        +calculateFee(duration, durationType) Double
    }

    class CarVehicle

    class BikeVehicle

    %% Parking Spot Hierarchy

    class ParkingSpot {
        <<abstract>>
        -spotNumber : int
        -isOccupied : boolean
        -spotType : String
        -vehicle : Vehicle
        +canParkVehicle(vehicle) Boolean
        +parkVehicle(vehicle) Void
        +vacate() Void
    }

    class CarParkingSpot {
        +canParkVehicle(vehicle) Boolean
    }

    class BikeParkingSpot {
        +canParkVehicle(vehicle) Boolean
    }

    %% Main Management Class

    class ParkingLot {
        -parkingSpots : List~ParkingSpot~
        +findAvailableSpot(vehicleType) ParkingSpot
        +parkVehicle(vehicle) ParkingSpot
        +vacateSpot(spot, vehicle) Void
    }

    %% Relationships

    ParkingFeeStrategy <|.. BasicHourlyRateStrategy

    PaymentStrategy <|.. CreditCardPayment
    PaymentStrategy <|.. CashPayment

    Vehicle <|-- CarVehicle
    Vehicle <|-- BikeVehicle

    Vehicle o-- ParkingFeeStrategy : uses

    ParkingSpot <|-- CarParkingSpot
    ParkingSpot <|-- BikeParkingSpot

    ParkingSpot o-- Vehicle : parks

    ParkingLot *-- ParkingSpot : manages