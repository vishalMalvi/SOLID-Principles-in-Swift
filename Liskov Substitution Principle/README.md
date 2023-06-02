## Liskov Substitution Principle

The Liskov Substitution Principle (LSP) is a fundamental principle in object-oriented programming that states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In simpler terms, it means that we should be able to use a derived class wherever we expect the base class and everything should still work correctly.

Let's consider an example to better understand LSP. Suppose we have a superclass called Shape that has a method called calculateArea to calculate the area of a shape. We also have two subclasses: Rectangle and Square. The Rectangle class has a length and width, while the Square class has only a side length. Here's an example of how the classes might look without applying LSP:

```swift 
class Shape {
    // Method to calculate area
    func calculateArea() -> Double {
        fatalError("Must be overridden")
    }
}

class Rectangle: Shape {
    var length: Double
    var width: Double
    
    init(length: Double, width: Double) {
        self.length = length
        self.width = width
    }
    
    override func calculateArea() -> Double {
        return length * width
    }
}

class Square: Shape {
    var sideLength: Double
    
    init(sideLength: Double) {
        self.sideLength = sideLength
    }
    
    override func calculateArea() -> Double {
        return sideLength * sideLength
    }
}
```
Now, let's say we have a function that expects an instance of Shape and calls its calculateArea method:

```swift 
func printArea(shape: Shape) {
    let area = shape.calculateArea()
    print("Area: \(area)")
}
```

This code works fine until we try to pass a Square object to the printArea function:

```swift 
let rectangle = Rectangle(length: 5, width: 3)
printArea(shape: rectangle) // Output: Area: 15

let square = Square(sideLength: 4)
printArea(shape: square) // Output: Area: 16
```

In this case, even though the output is correct, the Square object doesn't fully conform to the behavior expected by the Shape superclass. The Liskov Substitution Principle tells us that the subclasses should be able to substitute the superclass without causing any issues.

To fix this, we can refactor the code to properly adhere to the LSP. One possible solution is to use composition instead of inheritance:

```swift 
protocol Shape {
    // Method to calculate area
    func calculateArea() -> Double
}

struct Rectangle: Shape {
    var length: Double
    var width: Double
    
    func calculateArea() -> Double {
        return length * width
    }
}

struct Square: Shape {
    var sideLength: Double
    
    func calculateArea() -> Double {
        return sideLength * sideLength
    }
}
```
Now, the Shape protocol defines the contract for calculating the area and both Rectangle and Square implement the protocol. We can modify the printArea function accordingly:

```swift 
func printArea(shape: Shape) {
    let area = shape.calculateArea()
    print("Area: \(area)")
}
``` 

With this refactored code, we can safely pass both Rectangle and Square objects to the printArea function, satisfying the Liskov Substitution Principle:

```swift 
let rectangle = Rectangle(length: 5, width: 3)
printArea(shape: rectangle) // Output: Area: 15

let square = Square(sideLength: 4)
printArea(shape: square) // Output: Area: 16
```
Mow, the code adheres to the LSP because we can substitute the superclass (Shape) with its subclasses (Rectangle and Square) without any issues.
