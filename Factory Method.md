# Factory Method
## Definición

**Factory Method** hace que un diseño sea más personalizable y solo un poco más complicado. Otros patrones de diseño requieren nuevas clases, mientras que el Método de fábrica solo requiere una nueva operación.

La gente a menudo lo usa como la forma estándar de crear objetos; pero no es necesario si: la clase que se instancia nunca cambia, o la instancia se lleva a cabo en una operación que las subclases pueden anular fácilmente (como una operación de inicialización).


[![N|Solid](https://www.tutorialspoint.com/design_pattern/images/factory_pattern_uml_diagram.jpg)]
## Codigo del diagrama en JAVA
### Shape.java
~~~
 public interface Shape {
   void draw();
}
~~~
### Rectangle.java
~~~
public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}
~~~
### Square.java
~~~
public class Square implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Square::draw() method.");
   }
}
~~~
### Circle.java
~~~
public class Circle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Circle::draw() method.");
   }
}
~~~
### ShapeFactory.java
~~~
public class ShapeFactory {
	
   //use getShape method to get object of type shape 
   public Shape getShape(String shapeType){
      if(shapeType == null){
         return null;
      }		
      if(shapeType.equalsIgnoreCase("CIRCLE")){
         return new Circle();
         
      } else if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();
         
      } else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }
      
      return null;
   }
}
~~~
### FactoryPatternDemo.java
~~~ 
public class FactoryPatternDemo {

   public static void main(String[] args) {
      ShapeFactory shapeFactory = new ShapeFactory();

      //get an object of Circle and call its draw method.
      Shape shape1 = shapeFactory.getShape("CIRCLE");

      //call draw method of Circle
      shape1.draw();

      //get an object of Rectangle and call its draw method.
      Shape shape2 = shapeFactory.getShape("RECTANGLE");

      //call draw method of Rectangle
      shape2.draw();

      //get an object of Square and call its draw method.
      Shape shape3 = shapeFactory.getShape("SQUARE");

      //call draw method of square
      shape3.draw();
   }
}
~~~


Con esto queda concluido el patron **Factory method**.
