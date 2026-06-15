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
        -String licensePlate
        -String vehicleType
        -ParkingFeeStrategy feeStrategy
        +calculateFee(duration, durationType) Double
    }

    class CarVehicle {
    }

    class BikeVehicle {
    }

    %% Parking Spot Hierarchy
    class ParkingSpot {
        <<abstract>>
        -int spotNumber
        -boolean isOccupied
        -String spotType
        -Vehicle vehicle
        +canParkVehicle(vehicle)* Boolean
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
        -List~ParkingSpot~ parkingSpots
        +findAvailableSpot(vehicleType) ParkingSpot
        +parkVehicle(vehicle) ParkingSpot
        +vacateSpot(spot, vehicle) Void
    }

    %% Relationships
    ParkingFeeStrategy <|.. BasicHourlyRateStrategy : implements
    PaymentStrategy <|.. CreditCardPayment : implements
    PaymentStrategy <|.. CashPayment : implements

    Vehicle <|-- CarVehicle : extends
    Vehicle <|-- BikeVehicle : extends
    Vehicle o-- ParkingFeeStrategy : uses strategy

    ParkingSpot <|-- CarParkingSpot : extends
    ParkingSpot <|-- BikeParkingSpot : extends
    ParkingSpot o-- Vehicle : parks 0..1

    ParkingLot *-- ParkingSpot : manages 1..*