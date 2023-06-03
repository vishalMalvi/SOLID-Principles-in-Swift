## Single Responsibility Principle

The Single Responsibility Principle (SRP) is a software design principle that states that a class or module should have only one reason to change. In simpler terms, it means that each class should have a single responsibility or task and should not be responsible for multiple unrelated tasks.

Before applying the SRP, let's consider an example. Suppose we have a class called Employee in a payroll system. This class is responsible for storing employee information, calculating their salaries and generating payslips. Here's what the class might look like:

```swift 

class Employee {
    var name: String
    var id: String
    var salary: Double
    
    init(name: String, id: String, salary: Double) {
        self.name = name
        self.id = id
        self.salary = salary
    }
    
    func calculateSalary() {
        // Calculate salary logic
    }
    
    func generatePayslip() {
        // Generate payslip logic
    }
    
    // Other methods related to employee management
}

```
In this example, the Employee class violates the SRP because it has multiple responsibilities. It not only stores employee information but also performs salary calculations and generates payslips. This can make the class harder to maintain and modify in the future. If there are changes in the payroll calculation logic or payslip generation, we would need to modify this class.

To adhere to the SRP, we can separate the responsibilities into distinct classes. Here's an example of how the code might look after applying the SRP:

```swift 

class Employee {
    var name: String
    var id: String
    
    init(name: String, id: String) {
        self.name = name
        self.id = id
    }
}

class SalaryCalculator {
    func calculateSalary(employee: Employee) -> Double {
        // Calculate salary logic
    }
}

class PayslipGenerator {
    func generatePayslip(employee: Employee) {
        // Generate payslip logic
    }
}

```

In the updated code, the Employee class now only handles the responsibility of storing employee information. The SalaryCalculator class is responsible for calculating the salary and the PayslipGenerator class handles the generation of payslips. Each class has a single responsibility and can be modified independently without affecting the others.

By separating the responsibilities, we achieve better code organization, maintainability and flexibility. If there are changes in the salary calculation or payslip generation logic, we can modify the respective classes without impacting the Employee class. This modular approach makes the code easier to understand, test, and maintain in the long run, which is the essence of the Single Responsibility Principle.

