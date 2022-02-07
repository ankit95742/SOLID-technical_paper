# SOLID_technical_paper
---
In this technical paper we are going to learning about how me make our code more readable, clean and easy to add new feature using the **SOLID**.
---

SOLID is acronym that stand for five design principles.

1. Single responsibility principle
2. Open-close principle
3. Liskov substitution principle
4. Interface segregation principle
5. Dependecy inversion principle

let's start

## Single rensponsibility principle

Single rensponsibity principle state that, **"a class shold have one, and only one, reason to change."** 

In other why we also say that each class should have one rensponsibility, one single purpose.This mean that a class will do only one job, which leads us to conclude it should have only one reason to change.This principle state that if we have two reasons to change for a class, we have to split the functionality into two classes.Each class will handle only one responsibility and if in the feature we need to make one change we are going to make it in a the class which handle it.

Example : we have **Rectange** class. In it we have to method *draw()* and *area()*. draw() mwthod is use for drawing the rectange and area() method is use for calculate the area of rectange.So this class does not follow the Single rensponsibity principle.

```
public class Rectange{
        int length;
        int width;
        public void draw(int lenght,int width){
            //It use GUI class for draw the rectange.
        }
        public int area(int lenght, int width){
            return lenght * width;
        }
}
```
Because it has a two rensponsibility. If we split the two method into two diffrent class then we achive the single rensponsibility principle.

```
public abstract Rectange{
        int length;
        int width;
        abstract void draw();
        abstract int area();
}

public class Area extended Rectange{
       public int area(){
          return lenght * width;
       }
}

public abstact Draw extended Rectange{
      public void draw(){
            //using GUI we draw the rectange.
      }
}
```
**SRP benefits:**
1. Reduction in complexity of a code.
2. Increased readability, extensibility and maintence.
3. Reusability and reduced error.
4. Better testability.
5. Reduced coupling.

---

## Open-close principle

**"software entities like classes, modules and functions should be open for extension but closed for modification."**
A clever application design and the code writing part should take care of the frequent changes that are done during the development and the maintaning phase of an application.usaually, many changes are involved when a new functionality is added to an application. Those changes is exising code should be minimized, since it's assumed that the exiting code is already unit tested and changes in already written code might affect the existing functionality in an unwanted manner.

The open close principle states that the design and writing of code should be done in a way that new functionality should be added with minimum changes in the existing code. The design should be done in a way to allow the adding of new functionality as new classes, keeping as much as possible existing code unchanged.

Example: let's say that we have got a Rectangle class. In the Ractangle class we have two method Width and Height.

```public class Rectangle{
    private width;
    private height;
    public double Width { get; set; }
    public double Height { get; set; }
}
```
first the customer want area of rectnagle. So we make new class AreaCalculator. That give as the area of rectangle.
```
public class AreaCalculator
{
    public double Area(Rectangle[] shapes)
    {
        double area = 0;
        foreach (var shape in shapes)
        {
            area += shape.Width*shape.Height;
        }

        return area;
    }
}
```
After that customer change the requirement and add one more request to calculate area of Circle. So we make new class that give us the area of rectangle and circle.
```
public double Area(object[] shapes)
{
    double area = 0;
    foreach (var shape in shapes)
    {
        if (shape is Rectangle)
        {
            Rectangle rectangle = (Rectangle) shape;
            area += rectangle.Width*rectangle.Height;
        }
        else
        {
            Circle circle = (Circle)shape;
            area += circle.Radius * circle.Radius * Math.PI;
        }
    }

    return area;
}
```
The solution works and customer is happy.
But after the one week he come up with new requirement and he want to add area of triangle. So for that we have to modified the Area class. In the real world the changes are frequent. So to solve this problem we have to adopt the Open-close principle.

So the solution of this problem is to make the abstarct class **Shape**. after that extend this class for **Rectange** and **Circle**.
```
public abstract class Shape
{
    public abstract double Area();
}
```
```
public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }
    public override double Area()
    {
        return Width*Height;
    }
}

public class Circle : Shape
{
    public double Radius { get; set; }
    public override double Area()
    {
        return Radius*Radius*Math.PI;
    }
}
```
```
public double Area(Shape[] shapes)
{
    double area = 0;
    foreach (var shape in shapes)
    {
        area += shape.Area();
    }

    return area;
}
```
---

## Liskov substitution principle

The Liskov substitution principle was introduced by Brabara Liskov in her conference keynote "Data Abstraction" in 1987.
**"let Θ(x) be a property provable about object x of type T. Then Θ(y) should be true for object y of type S where S is a subtype of T.**

The principle defines that objects of a superclass shall be replaceble with objects of its subclass without breaking the application.

That requries the objects of your subclass to behave in the same way as the objects of your superclass.

It means that we must make sure that new derived classes are extending the base classes without changing their behaviour.The Liskov substitution principle is an extension of open close principle.

Exmaple:

1. Calculate Area of rectange.
2. Calculate Area of Square as well
So we create Rectange as base class and Squre ass subclass.

```
public class Rectnage{
        protected int width;
        protected int height;
        public void setWidth(int width){
                this.width = width
        }
        public void setHeight(int height){
                this.height = height;
        }
        public int getArea(){
                return width * height;
        }
}
```
```
public class Squre extend Rectange{
        public void setWidth{
                this.width = width;
                this.height = height;
        }
        public void setHeight{
                this.width = width;
                this.height =height;
        }
}
```

In the Squre class we are violating the LSP. because we are change the width = heigth and height = width. It is the violation of LSP.

Solution : Make a abstract class for shape and In this class provied the area() method as abstarct. After that implement other two class Rectange and Squre.

```
public abstract class Shape{
        abstract public int getArea();
}
```
```
public class Rectange extend Shape{
        public int width{get;set;}
        public int height{get;set;}
        
        public int getArea(){
                return width * height;
        }
}
```
```
public class Squre extend Shape{
        pulbic int length{get;set;}
        
        public int getArea(){
                return length ** length;
        }
}
```

---

## Interface segregation principle

**Client should not be forced to depend upon interfaces that they do not use**

When we design an application we should take care how we are going to make abstract a module which contains serveral submodules considering the module implemented by a class, we can have an abstraction of the system done in a interface. But if we want to extend our application adding another module that contains only some of the modules of the original system, we are forced to implement the full interface and to write some dummy methods. such an interface is named fat interface or polluted interface. Having the polluted interface is not good solution and might include in appropriate behaviour in the system.

The Interface segregation principle states that client should not be forced to implement interfaces they do not use. Instead of onr fat interface many small inerfaces are preferred based on groups of methods, each one serving one submodule.

Example :

xerox project
1. We need to create new printer system.
2. printer should have ability to print.
3. Along with printing it should be capable of scanning, faxing and photocopy.

This project we make using the LSP 
So first we make interface **IPrinter**. After this we make all the functionality using differnt classes.

This code is overview of the main code.
```
public interface IPrinter{
        void print(List<item> items);
        void scan(List<item> items);
}
```
```
public interface IFax{
        void fax(List<item> items);
}
public interface IPhotocopy{
        void photocopy(List<item> items);
}

public iterface IDuplex{
        void printDuplex(List<item> items);
}
```
```
public interface IMachine:IPrinter{
        IFax,IPhotocopy,Iduplex
}
```

---

## dependency inversion principle

**"The Dependency inversion principle state that hight level modules/classes should not depend on low-level modules/classes Both should depend upon abstarction."**

Also,abstraction should not depend upon details. Details should depend upon abstraction.the main motto of the DIP is any higher classes should always depend upon the abstraction of the class rather than the deatail.

The aims to reduce the coupling between the classes is achived by introducing abstraction between the layer, thus doesn't care about the real implementaion.
   
