# Violation (M-1)

classDiagram

class Main_M1
class Vehicle
class Car
class Truck

Vehicle <|.. Car
Vehicle <|.. Truck

Main_M1 --> Car : new Car()
Main_M1 --> Truck : new Truck()


# Violation (M-2)

classDiagram

class Main_M2
class Vehicle
class Car
class Bike
class Truck

Vehicle <|.. Car
Vehicle <|.. Bike
Vehicle <|.. Truck

Main_M2 --> Car : if(type=="Car")
Main_M2 --> Bike : if(type=="Bike")
Main_M2 --> Truck : if(type=="Truck")

# Ultimate Factory Design Pattern

classDiagram

class Main
class VehicleFactory

class Vehicle {
    <<interface>>
}

class Car
class Bike
class Truck

Vehicle <|.. Car
Vehicle <|.. Bike
Vehicle <|.. Truck

Main --> VehicleFactory : getVehicle()
Main --> Vehicle : use

VehicleFactory --> Car : creates
VehicleFactory --> Bike : creates
VehicleFactory --> Truck : creates