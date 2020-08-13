# Abstract Factory
## Definición
Los patrones de **Abstract Factory** funcionan en torno a una superfábrica que crea otras fábricas. Esta fábrica también se llama fábrica de fábricas. Este tipo de patrón de diseño viene bajo el patrón de creación, ya que este patrón proporciona una de las mejores formas de crear un objeto.

En el patrón **Abstract Factory**, una interfaz es responsable de crear una fábrica de objetos relacionados sin especificar explícitamente sus clases. Cada fábrica generada puede dar los objetos según el patrón de Fábrica.



[![N|Solid](https://www.tutorialspoint.com/design_pattern/images/factory_pattern_uml_diagram.jpg)]
## Codigo del diagrama en JAVA
### Shape.java
~~~
 public interface Shape {
   void draw();
}
~~~
### RoundedRectangle.java
~~~
public class RoundedRectangle implements Shape {
   @Override
   public void draw() {
      System.out.println("Inside RoundedRectangle::draw() method.");
   }
}
~~~
### RoundedSquare.java
~~~
public class RoundedSquare implements Shape {
   @Override
   public void draw() {
      System.out.println("Inside RoundedSquare::draw() method.");
   }
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
### AbstractFactory.java
~~~
public abstract class AbstractFactory {
   abstract Shape getShape(String shapeType) ;
}
~~~
### ShapeFactory.java
~~~ 
public class ShapeFactory extends AbstractFactory {
   @Override
   public Shape getShape(String shapeType){    
      if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();         
      }else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }	 
      return null;
   }
}
~~~
### RoundedShapeFactory.java
~~~
public class RoundedShapeFactory extends AbstractFactory {
   @Override
   public Shape getShape(String shapeType){    
      if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new RoundedRectangle();         
      }else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new RoundedSquare();
      }	 
      return null;
   }
}
~~~
### FactoryProducer.java
~~~
public class FactoryProducer {
   public static AbstractFactory getFactory(boolean rounded){   
      if(rounded){
         return new RoundedShapeFactory();         
      }else{
         return new ShapeFactory();
      }
   }
}
~~~
### AbstractFactoryPatternDemo.java
~~~
public class AbstractFactoryPatternDemo {
   public static void main(String[] args) {
      //get shape factory
      AbstractFactory shapeFactory = FactoryProducer.getFactory(false);
      //get an object of Shape Rectangle
      Shape shape1 = shapeFactory.getShape("RECTANGLE");
      //call draw method of Shape Rectangle
      shape1.draw();
      //get an object of Shape Square 
      Shape shape2 = shapeFactory.getShape("SQUARE");
      //call draw method of Shape Square
      shape2.draw();
      //get shape factory
      AbstractFactory shapeFactory1 = FactoryProducer.getFactory(true);
      //get an object of Shape Rectangle
      Shape shape3 = shapeFactory1.getShape("RECTANGLE");
      //call draw method of Shape Rectangle
      shape3.draw();
      //get an object of Shape Square 
      Shape shape4 = shapeFactory1.getShape("SQUARE");
      //call draw method of Shape Square
      shape4.draw();
      
   }
}
~~~
Con esto queda concluido el patron **Abstract Factory**.
Probando en este repo
