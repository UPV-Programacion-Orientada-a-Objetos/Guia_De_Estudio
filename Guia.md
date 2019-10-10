# Guía de estudio
## Unidad 1
### Rebeca González Batista
----
-----

## Interfaces
Es una descripción de las acciones que puede hacer un objeto ... por ejemplo, cuando se activa un interruptor de luz, la luz se enciende, no importa cómo, solo eso. La finalidad de la interfaz es de obligar a una clase a tener ciertas funciones y definir estas funciones de una manera especifica.

  - Son mecanismos para que puedan interactuar varios objetos no relacionados entre si.
  - Obligan la herencia.
  - Contienen las declaraciones de los métodos, pero no su implementación.
  - Son plantillas de comportamiento que deben ser implementados por otras clases.
  - Sus metodos son abstractos y publicos
  - Pueden heredar de otras interfaces.
  - La implementación se proporciona de las clases que hereden de la clase actual.
  - No llevan los modificadores public, virtual o abstract.
    
Un ejemplo del uso de las interfaces:

   ---<img width="250" height="400" src="Images/Captura de pantalla (86).png">

Un ejemplo de una interfaz:
```javascript
public interface Pelota {
    void rebotar ();
}
```
------
------
## Clases abstractas
Es una clase normal pero al menos uno de sus métodos debe ser abstracto para considerar a la clase abstracta, también puede contener métodos no abstractos.
   - Son mecanismos que obligan la herencia.
   - No se pueden instanciar.
   - Se utilizan solamente para heredar de ellas.
   - Se antepone la palabra abstract al nombre de la clase.
   - Obliga a la herencia.
   - Los métodos abstractos deben implemnetarse en la clase que extiende de la clase abstracta.
   - Pueden heredar de otras clases e interfaces.
   - Puede tener elementos abstractos.
   - Se utiliza abstract para definir elementos abstractos (solo dentro de clases abstractas).
   - Los elementos abstractos NO proporcionan implementación; solo declaraciones.
   - En la subclase, se utiliza “override” para realizar la implementación correspondiente.
   
   
   
Un ejemplo de una clase abstracta:   
``` java   
   abstract class Drawing
{
   abstract void miMetodo(int var1, int var2);
   String miOtroMetodo( ){ ... }
}
```
------------------------
----------------------
## Interfaces en conflicto
### Colision de nombres

Una colisión de nombres tiene lugar cuando un intento de resolver un nombre usado en un espacio de nombre privado.

``` java
interface I1 { void f(); }
interface I2 { int f(int i); }
interface I3 { int f(); }

class C { public int f() { return 1; } }

class C2 implements I1, I2 {
    public void f();
    public int f(int i) { return 1; } 
}

class C4 extends C implements I3 {
    // Idéntico, no hay problema
    public int f() { return 1; }
}

class C5 extends C impelents I1 {} // Error
interface I4 extends I1, I3 {}``


```

La firma de las interfaces I1 e I3 son iguales, al querer implementar estas en la interfaz I4 se crea una colicion de nombres.


------

### Clases internas
Es una clase dentro de otra clase, a estas se es pueden llamar clase interna y clase externa respectivamente.

Una clase interna tiene acceso a todas las variables y métodos de su clase externa y puede referirse a ellos directamente de la misma manera que lo hacen otros miembros no estáticos de la clase externa.

Ejemplo de una clase interna:

```java
public class Parcell {
    class Contents {
        private int i = 11;
        public int value() { return i; }
    }
    
    
```
Para construir un objeto de una clase interna se debe especificar el objeto como *NombreClaseExterna.ClaseInterna*.
Pero al declarar un objeto de una clase interna se debe tomar en cuenta que esta declaración no debe ser dentro de un método no estático de la clase externa.

Cuando se crea un objeto de la clase interna también se crea un enlace con la clase ecterna, por lo que puede acceder a los metodos de esta sin ningun metodo especial. 

También existen las *clases internas anonimas*
``` java
public class Parcel7 {
    public Contents contents() {
        return new contents() { // Inserte una definición de clase
            private int i = 11;
            public int value() { return i; }
        }; // En este caso SI hace falta un punto y coma
    }

```
Se utilizan normalmente en situaciones en las que es necesario poder crear una clase de peso ligero que se pase como parámetro. Esto normalmente se hace con una interfaz. Pero tienen algunas debilidades como que pueden extender de una clase o implementar una interfaz, pero no pueden hacer ambas cosas al mismo timepo. Y, si se implementamenta una interfaz, solo queda en eso, *UNA*.

-------------
### Clases anidadas
Si no es necesaria una conexión entre el objeto de la clase interna y el objeto de la clase externa, puede abrir paso a una clase anidada. En esta no es necesario un objeto de una clase externa para crear uno de una clase interna. Sin embargo no puede acceder a un objeto no estatico de la clase externa con un objeto de una clase anidada. 

*Punto importante:* Las clases internas solo pueden tener elementos estaticos. 

``` java
public class Parcel11 {
    private static class ParcelContents implements Contents {
        private int i=11;
        public int value() { return i; }
    }

    protected static class ParcelDestination implements Destination {
        private String label;
        private ParcelDestination(String whereTo) {
            label = whereTo;
        }
        public String readLabel() { return label; }

     
        public static void f() {}
        static int x = 10;
        static class AnotherLevel {
            public static void f() {}
            static int x = 10;
        }
    }
    
  ```
-------------
-------------
## Genericidad

### Clase Object
Es la clase mamá raíz de todo el árbol de la jerarquía de clases Java, y proporciona un cierto número de métodos de utilidad general que pueden utilizar todos los objetos. Algunos de las funciones son:

////////imagen de metodos

---------
### Estándar de nombre en tipos genéricos
Realmente se le puede dar el nombre que se quiera pero con cierto estandar es más facíl y general su comprención. Los más usados son:

- E  (Elemento): Esta se usa para cuando se tienen colecciones de datos como por ejemplo vectores, listas, etc. 
- N  (Número):   Se especifica que solo se quiere de un tipo númerico.
- T  (Tipo)  :   No especifica el tipo de valor así que puede ser cualquiera.
-----------

### Clases genéricas
Si queremos realizar una operación específica dentro de esta nueva clase, sea cual sea el tipo de datos que va a recibir, podemos hacer uso de los tipos genéricos. 

Se definen así: 
``` java
public class Alo<T> {
  private T t;
  public void set(T t) { this.t = t; }
  public T get() { return t; }
}
```
Como se puede ver se esta utilizando un tipo T o sea que la clase puede utilizar cualquier tipo de dato.

-----------------

### Interfaces genéricas
Es lo mismo pero en interfaz bro
``` java

public interface Comparable<T> {
  int compareTo(T o);
}
```
-----------

### Métodos vacios
Son lon métodos que introducen sus propios parámetros pero el alcance esta limitado al método donde fue declarado, tanto los métodos estáticos como no estáticos  y constructores son permitidos.

``` java
public void setKey(K key) {
  this.key = key; 
  }
```
---------------

### Paŕametros acotados
Hay ocasiones en las que queremos que un método sólo acepte ciertos tipos como parámetros.  Y para eso se utilizan los parametros acotados.
``` java
       public <U extends Number> void inspect(U u){
             System.out.println("T: " + t.getClass().getName());
             System.out.println("U: " + u.getClass().getName());
         }

```
Este método acepta todo tipo de datos pero restringidos a númericos y lo hace utilizando la declaración *<U extends Number>*
  
--------
  
### Wildcards
Vamos a suponer un ejemplo sencillo en el que tenemos dos clases. La clase Persona y la clase Deportista.

``` java
import java.util.ArrayList;
import java.util.List;
      public class PrincipalDeportista {
              public static void main(String[] args) {
                  List<Deportista> listaPersonas=new ArrayList<Deportista>();
                  listaPersonas.add(new Persona("pepe"));
                  listaPersonas.add(new Persona("maria"));
                  imprimir(listaPersonas);
}

       public static void imprimir(List<Persona> lista) {
              for(Persona p:lista) {
                System.out.println(p.getNombre());
                }
        }
}
```

El siguiente código imprime la lista Persona el cual esta definido especificamente para aquellos objetos de la clase Deportista y siendo así yo no puedo agregar otros objetos de clases que deriven de la clase Persona como por ejemplo abogado, arquitecto, QUIBO_ESTO_YA_QUEDO.

El caracter Wildcard(?) da una solución a este problema.
``` java
    public static void imprimir(List<? extends Persona> lista) {
         for(Persona p:lista) {
             System.out.println(p.getNombre());
           }
     }
     
```
De esta manera un wildcard nos puede ayudar a ser más flexibles y poder ingresar a cualquier objeto de una clase que herede de la clase Persona a la lista. Es el genérico pero en un signo.
