
## Open/Closed Principle 

The Open/Closed Principle is a design principle that states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This means that you should be able to add new functionality or behavior to a class without modifying its existing code.

Before applying the Open/Closed Principle:
let's consider an example. Suppose we have a class called Shape, which has a calculateArea() method. Initially, it only supports calculating the area of a rectangle:

```swift
class Shape {
    func calculateArea(length: Double, width: Double) -> Double {
        return length * width
    }
}
```
Now, Suppose we want to add support for calculating the area of a circle. Without following the Open/Closed Principle, we might be tempted to modify the existing Shape class and add a new method calculateArea(radius: Double):

```swift
class Shape {
    func calculateArea(length: Double, width: Double) -> Double {
        return length * width
    }
    
    func calculateArea(radius: Double) -> Double {
        return 3.14 * radius * radius
    }
}
```
The problem with this approach is that we have modified the existing class, which can introduce bugs and impact the existing code that relies on the Shape class.

After applying the Open/Closed Principle:
To adhere to the Open/Closed Principle, we can create an abstract base class or protocol called Shape and then define concrete classes that implement specific shapes. Here's an example:

```swift
protocol Shape {
    func calculateArea() -> Double
}

class Rectangle: Shape {
    let length: Double
    let width: Double
    
    init(length: Double, width: Double) {
        self.length = length
        self.width = width
    }
    
    func calculateArea() -> Double {
        return length * width
    }
}

class Circle: Shape {
    let radius: Double
    
    init(radius: Double) {
        self.radius = radius
    }
    
    func calculateArea() -> Double {
        return 3.14 * radius * radius
    }
}
```
In this approach, the Shape protocol defines the common behavior of all shapes and each concrete class (e.g. Rectangle and Circle) implements the calculateArea() method according to their specific shape's logic. If we need to add support for a new shape, we can create a new class that conforms to the Shape protocol without modifying any existing code.

By following the Open/Closed Principle, we can easily extend our software with new functionality without the risk of introducing bugs or breaking existing code.
