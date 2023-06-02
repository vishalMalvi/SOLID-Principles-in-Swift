##  Interface Segregation Principle

The Interface Segregation Principle (ISP) is a design principle that suggests breaking down large, monolithic interfaces into smaller, more specialized interfaces. It promotes the idea that clients should not be forced to depend on interfaces they do not use. In simple terms, it encourages the creation of focused and specific interfaces tailored to the needs of each client.

Before applying ISP, let's consider an example where we have a Printer protocol with multiple methods:

```swift
protocol Printer {
    func printDocument()
    func scanDocument()
    func faxDocument()
    func copyDocument()
}

class OfficePrinter: Printer {
    func printDocument() {
        // Implementation
    }
    
    func scanDocument() {
        // Implementation
    }
    
    func faxDocument() {
        // Implementation
    }
    
    func copyDocument() {
        // Implementation
    }
}

class HomePrinter: Printer {
    func printDocument() {
        // Implementation
    }
    
    func scanDocument() {
        // Implementation
    }
    
    func faxDocument() {
        // Implementation
    }
    
    func copyDocument() {
        // Implementation
    }
}
```

In this case, both OfficePrinter and HomePrinter implement the same Printer protocol, which includes methods for printing, scanning, faxing, and copying. However, in practice, a home printer may not have the capability to fax or copy documents. By implementing the complete Printer protocol, we force the home printer to provide empty or irrelevant implementations for those methods.

After applying ISP, we refactor the interfaces to be more specific:

```swift
protocol Printable {
    func printDocument()
}

protocol Scanable {
    func scanDocument()
}

protocol Faxable {
    func faxDocument()
}

protocol Copyable {
    func copyDocument()
}

class OfficePrinter: Printable, Scanable, Faxable, Copyable {
    func printDocument() {
        // Implementation
    }
    
    func scanDocument() {
        // Implementation
    }
    
    func faxDocument() {
        // Implementation
    }
    
    func copyDocument() {
        // Implementation
    }
}

class HomePrinter: Printable, Scanable {
    func printDocument() {
        // Implementation
    }
    
    func scanDocument() {
        // Implementation
    }
}
```
By applying ISP, we have segregated the functionalities into separate protocols: Printable, Scanable, Faxable, and Copyable. Now, both OfficePrinter and HomePrinter can implement only the protocols they need. The HomePrinter class doesn't need to implement the unnecessary Faxable and Copyable protocols.

This segregation allows each class to be focused on its specific responsibilities, leading to cleaner and more maintainable code. It also prevents clients from depending on methods they don't use, reducing the chance of errors and unnecessary coupling

