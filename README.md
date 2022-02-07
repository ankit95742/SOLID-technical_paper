# SOLID_technical_paper
---
In this technical paper we are going to learning about how me make our code more readable, clean and easy to add new feature using the **SOLID**.
---

SOLID is acronym that stand for five design principles.

1. Single responsibility priciple
2. Open-close priciple
3. Liskov substitution priciple
4. Interface segregation priciple
5. Dependecy inversion priciple

let's start

## Single rensponsibility priciple

Single rensponsibity priciple state that, **"a class shold have one, and only one, reason to change."** 

In other why we also say that each class should have one rensponsibility, one single purpose.This mean that a class will do only one job, which leads us to conclude it should have only one reason to change.This priciple state that if we have two reasons to change for a class, we have to split the functionality into two classes.Each class will handle only one responsibility and if in the feature we need to make one change we are going to make it in a the class which handle it.

Example : we have *Rectange* class. In it we have to method *draw()* and *area()*. draw() mwthod is use for drawing the rectnage and area() method is use for calculate the area of rectange.So this class does not follow the Single rensponsibity priciple.

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
Because it has a two rensponsibility. If we split the two method into two diffrent class then we achive the single rensponsibility priciple.

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

## Open-close priciple

**"software entities like classes, modules and functions should be open for extension but closed for modification."**
A cleaver application design and the code writing part should take care of the frequent changes that are done during the development and the maintaning phase of an application.usaually, many changes are involved when a new functionality is added to an application. Those changes is exising code should be minimized, since it's assumed that the exiting code is already unit tested and changes in already written code might affect the existing functionality in an unwanted manner.

The open close priciple states that the design and writing of code should be done in a way that new functionality should be added eith minimum changes in the existing code. The design should be done in a way to allow the adding of new functionality as new classes, keeping as much as possible existing code unchanged.

Example:
```

```
