# ISP Violated

```mermaid
classDiagram

class Shape {
    <<interface>>
    +area() double
    +volume() double
}

class Square {
    -side : double
    +Square(side)
    +area() double
    +volume() double
}

class Rectangle {
    -length : double
    -width : double
    +Rectangle(length,width)
    +area() double
    +volume() double
}

class Cube {
    -side : double
    +Cube(side)
    +area() double
    +volume() double
}

class AreaCalculator {
    +calculateArea()
}

class VolumeCalculator {
    +calculateVolume()
}

Shape <|.. Square
Shape <|.. Rectangle
Shape <|.. Cube

AreaCalculator --> Shape : uses
VolumeCalculator --> Shape : uses
```

**Problem**

- `Square` and `Rectangle` are forced to implement `volume()`.
- `VolumeCalculator` assumes every `Shape` supports volume.
- Some implementations throw exceptions or contain dummy logic.
- Clients depend on methods they do not need.

---

# ISP Followed

```mermaid
classDiagram

class TwoDimensionalShape {
    <<interface>>
    +area() double
}

class ThreeDimensionalShape {
    <<interface>>
    +area() double
    +volume() double
}

class Square {
    -side : double
    +Square(side)
    +area() double
}

class Rectangle {
    -length : double
    -width : double
    +Rectangle(length,width)
    +area() double
}

class Cube {
    -side : double
    +Cube(side)
    +area() double
    +volume() double
}

class AreaCalculator {
    +calculateArea()
}

class VolumeCalculator {
    +calculateVolume()
}

TwoDimensionalShape <|.. Square
TwoDimensionalShape <|.. Rectangle

ThreeDimensionalShape <|.. Cube

AreaCalculator --> TwoDimensionalShape : uses
AreaCalculator --> ThreeDimensionalShape : uses

VolumeCalculator --> ThreeDimensionalShape : uses
```

**Benefit**

- `Square` and `Rectangle` only implement `area()`.
- `Cube` implements both `area()` and `volume()`.
- Clients depend only on the interfaces they actually need.
- No unnecessary methods, exceptions, or dummy implementations.