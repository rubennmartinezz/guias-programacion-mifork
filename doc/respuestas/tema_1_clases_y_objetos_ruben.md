<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### Respuesta

Las cuatro características fundamentales de la POO son la **encapsulación**, la **herencia**, el **polimorfismo** y la **abstracción**. La encapsulación permite agrupar datos y funciones relacionadas dentro de una clase, ocultando los detalles internos mediante modificadores de acceso (público, privado). Este concepto es comparable a cómo en C se podrían usar estructuras para agrupar datos, pero va más allá al permitir controlar quién puede acceder a qué.

La herencia posibilita que una clase derive de otra, heredando sus atributos y métodos, y permitiendo reutilizar código. La abstracción consiste en definir las características esenciales de un objeto sin incluir los detalles de implementación, permitiendo trabajar con conceptos simplificados. El polimorfismo permite que métodos con el mismo nombre se comporten de forma diferente según el contexto o el tipo del objeto, proporcionando flexibilidad al diseño.


## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Respuesta

Cuatro lenguajes ampliamente utilizados que soportan POO son **Java**, **C++**, **Python** y **C#**. Java es uno de los más populares para aplicaciones empresariales y está diseñado completamente alrededor de POO. C++ extendió C con características orientadas a objetos, permitiendo la combinación de programación procedural y orientada a objetos. Python es un lenguaje versátil con soporte completo para POO y es muy usado en ciencia de datos e inteligencia artificial. C# es un lenguaje moderno creado por Microsoft que combina características de C++ y Java, siendo muy popular para desarrollo con la plataforma .NET.


## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Respuesta

La **programación estructurada** es un paradigma que enfatiza el uso de estructuras de control claras (secuencia, bifurcación y bucles) en lugar de saltos incondicionales (goto). Busca escribir código más legible y mantenible mediante la descomposición de programas en bloques lógicos. En C, por ejemplo, se utilizan funciones y estructuras de control para organizar el código, evitando la spaghetti code que resultaba del uso excesivo de goto.

La **programación modular** es una extensión de la programación estructurada que divide los programas en módulos o unidades independientes, cada una con responsabilidades bien definidas. Cada módulo puede compilarse por separado y reutilizarse en otros proyectos, mejorando la mantenibilidad y la organización. La POO puede verse como una evolución natural de estos paradigmas, incorporando no solo la modularidad sino también la encapsulación y la reutilización de código a través de la herencia.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Respuesta

Los tres elementos que definen a un objeto son **identidad**, **estado** y **comportamiento**. La identidad es lo que hace que un objeto sea único e distinguible de otros objetos, típicamente representada por la dirección en memoria donde reside. El estado se refiere a los valores actuales de los atributos del objeto, es decir, las características o propiedades que lo describen en un momento determinado. El comportamiento es el conjunto de métodos que el objeto puede ejecutar, es decir, las acciones que puede realizar.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta

Una **clase** es un plano o plantilla que define la estructura y el comportamiento de los objetos. Es decir, es un tipo de dato que especifica qué atributos tendrá un objeto y qué métodos podrá ejecutar. Una clase no es lo mismo que un objeto; la clase existe solo en el código como definición, mientras que un objeto es una instancia concreta de esa clase que existe en memoria durante la ejecución del programa. Una **instancia** es precisamente esa realización concreta de una clase con valores específicos para sus atributos.

No todos los lenguajes orientados a objetos manejan explícitamente el concepto de clase. Algunos lenguajes, como JavaScript, utilizan un modelo de **prototipos** donde los objetos se crean a partir de otros objetos (prototipos) sin necesidad de clases formales. Sin embargo, la mayoría de lenguajes OOP populares (Java, C++, Python, C#) sí utilizan clases como concepto fundamental.


## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### Respuesta

En la mayoría de lenguajes orientados a objetos, los objetos se almacenan en el **montículo** (heap), una región de memoria dinámica. Cuando se crea un objeto con `new`, se asigna espacio en el heap y se devuelve una referencia (dirección en memoria) a ese objeto. Las variables que guardan objetos contienen estas referencias, no el objeto en sí. Esta es una diferencia importante respecto a C, donde podrías usar structs en la pila o dinámicamente en el heap con `malloc`.

El almacenamiento varía según el lenguaje: en C y C++ el programador es responsable de liberar la memoria con `free()` o `delete`, lo que puede causar memory leaks. En cambio, la **recolección de basura** es un mecanismo automático que algunos lenguajes (Java, Python, C#) emplean para liberar automáticamente la memoria de objetos que ya no se usan. El recolector de basura identifica objetos sin referencias activas y libera su memoria, eliminando la necesidad de gestión manual pero con cierto costo de rendimiento.


## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Respuesta

Un **método** es una función que pertenece a una clase y define el comportamiento de los objetos de esa clase. Es equivalente a una función en C, pero está asociada a una clase y puede acceder a los atributos del objeto. Los métodos se invocan sobre objetos específicos (instancias) usando la notación de punto.

La **sobrecarga de métodos** (method overloading) es la capacidad de tener múltiples métodos con el mismo nombre dentro de la misma clase, siempre que difieran en el número, tipo o orden de sus parámetros. Por ejemplo, se podría tener un método `calculaDistancia()` que funcione tanto con otro Punto como con coordenadas numéricas individuales. Cuando se invoca el método, el compilador elige la versión correcta basándose en los argumentos pasados. Esto no es directamente posible en C, donde cada función debe tener un nombre único.


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### Respuesta

```java
public class Punto {
    double x;
    double y;
    
    public double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
```

Ejemplo de uso:

```java
public class Main {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3.0;
        p.y = 4.0;
        
        double distancia = p.calculaDistanciaAOrigen();
        System.out.println("Distancia: " + distancia);
    }
}
```


## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### Respuesta

El punto de entrada en Java es el método `main` con la firma `public static void main(String[] args)`. Cuando se ejecuta un programa Java, la máquina virtual busca este método y lo invoca automáticamente. La palabra clave **`static`** indica que el método o variable pertenece a la clase en sí, no a una instancia específica. Esto permite invocar el método sin necesidad de crear una instancia de la clase, lo cual es esencial para `main` ya que necesita un punto de partida antes de que existan objetos.

La palabra `static` se usa también para variables miembro (atributos de clase) que son compartidos por todas las instancias, y para métodos de utilidad que no necesitan acceso a datos específicos de instancias. Cuando se combina `static` con **`final`**, se crea una constante de clase: un valor que pertenece a la clase, es único en toda la ejecución y no puede ser modificado. Por ejemplo, `public static final double PI = 3.14159;` define una constante que todas las instancias pueden usar pero no cambiar.

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta

Java funciona mediante un proceso de compilación de dos pasos. Primero, se compila el código fuente (`.java`) usando `javac`: `javac Punto.java` genera un archivo `Punto.class`. Este archivo no contiene código máquina nativo como en C, sino **byte-code**, un formato intermedio e independiente de la plataforma que es más compacto que el código fuente pero no directamente ejecutable. Luego, para ejecutar el programa se usa: `java Main`, que busca la clase `Main` y ejecuta su método `main`.

Java es considerado un lenguaje "compilado e interpretado" o "compilado en máquina virtual". La **máquina virtual de Java (JVM)** es un programa que interpreta el byte-code y lo traduce a instrucciones nativas del procesador en tiempo de ejecución. Esta arquitectura permite que un mismo `.class` pueda ejecutarse en cualquier máquina que tenga instalada la JVM, proporcionando portabilidad ("escribe una vez, ejecuta en cualquier lugar"), algo que no era tan sencillo con C/C++ donde necesitabas compilar para cada plataforma específica.


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta

La palabra clave **`new`** es responsable de crear una nueva instancia de una clase en el heap y devolver una referencia a ella. Realiza tres acciones: asigna memoria para el nuevo objeto, invoca el constructor y devuelve la referencia. Un **constructor** es un método especial que se ejecuta automáticamente cuando se crea un objeto, inicializando sus atributos. El constructor tiene el mismo nombre que la clase y no retorna nada (ni siquiera void).

Ejemplo de constructor en la clase `Empleado`:

```java
public class Empleado {
    String dni;
    String nombre;
    String apellidos;
    
    public Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }
}
```

Uso: `Empleado emp = new Empleado("12345678X", "Juan", "García López");`


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta

**`this`** es una referencia implícita que apunta al objeto actual sobre el cual se está ejecutando un método. Permite acceder a los atributos y métodos del objeto desde dentro de la clase. Es especialmente útil cuando existe ambigüedad de nombres, como cuando un parámetro del constructor tiene el mismo nombre que un atributo. En C/C++, el equivalente sería usar el puntero `this` (en C++ es similar pero en C habría que pasarlo explícitamente como parámetro).

No todos los lenguajes lo llaman `this`. Por ejemplo, en Python se usa `self`, y en algunos otros lenguajes tiene nombres diferentes. Ejemplo en la clase `Punto`:

```java
public class Punto {
    double x;
    double y;
    
    public Punto(double x, double y) {
        this.x = x;  // this.x se refiere al atributo de la clase
        this.y = y;  // x e y son los parámetros
    }
    
    public double distanciaA(Punto otro) {
        return Math.sqrt(Math.pow(this.x - otro.x, 2) + 
                        Math.pow(this.y - otro.y, 2));
    }
}
```


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta

```java
public class Punto {
    double x;
    double y;
    
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
    
    public double distanciaA(Punto otro) {
        double difX = this.x - otro.x;
        double difY = this.y - otro.y;
        return Math.sqrt(difX * difX + difY * difY);
    }
}
```

Ejemplo de uso: `double dist = punto1.distanciaA(punto2);`


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### Respuesta

En Java, el paso de parámetros es siempre **por valor**, pero el valor de un objeto es su referencia (dirección en memoria). Esto significa que cuando se pasa un `Punto` a un método, se copia la referencia, no el objeto completo. Por lo tanto, los cambios realizados sobre los atributos del Punto dentro del método **sí afectan** al objeto original fuera del método, porque ambas referencias apuntan al mismo objeto en memoria.

Con tipos primitivos como `int`, el comportamiento es diferente. Si se pasa un `int` y se modifica dentro del método, esos cambios **no afectan** al entero original fuera del método, porque se pasó una copia del valor. Esta es una distinción importante: en C/C++ sin orientación a objetos, conseguir el comportamiento de referencia requería pasar explícitamente un puntero, mientras que en Java los objetos se comportan "como por referencia" automáticamente.


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta

El método **`toString()`** es un método heredado de la clase `Object` (la clase base de todas las clases en Java) que retorna una representación textual del objeto como un `String`. Cuando se intenta convertir un objeto a texto (por ejemplo, al imprimirlo con `System.out.println()`), Java invoca automáticamente `toString()`. Por defecto, `toString()` retorna algo poco útil como `Punto@a1b2c3`, pero se puede sobrescribir (override) para proporcionar una representación más significativa.

Concepto similar existe en otros lenguajes: en Python se llama `__str__()`, en C# se llama `ToString()`. Ejemplo de `toString()` en la clase `Punto`:

```java
public String toString() {
    return "Punto(" + x + ", " + y + ")";
}
```

Ahora, al hacer `System.out.println(punto);`, se mostrará algo como `Punto(3.0, 4.0)` en lugar de `Punto@a1b2c3`.


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Respuesta

Una clase es conceptualmente similar a un `struct` en C en cuanto que ambos agrupan datos relacionados en una única estructura. Sin embargo, un `struct` en C es principalmente un contenedor de datos (atributos), mientras que una clase en Java combina datos con comportamiento (métodos). Un `struct` en C es "inerte", no sabe cómo hacer nada con sus datos.

Para que un `struct` sea como una clase, le faltaría principalmente las funciones miembro y los modificadores de acceso (encapsulación). En C, podrías asociar funciones a un struct pasándolo como parámetro explícitamente (como se verá en la siguiente pregunta), pero carece de la integración que proporcionan los métodos. Las variables de tipo struct son instancias en el sentido técnico, pero no tienen identidad ni comportamiento como lo tienen los objetos en POO. Una clase proporciona una forma más integrada y segura de trabajar con estos conceptos, ocultando detalles internos y permitiendo un diseño más modular.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta
En C, se podría emular una clase `Punto` usando un struct y funciones que reciben explícitamente un puntero al struct como parámetro:

```c
#include <math.h>

typedef struct {
    double x;
    double y;
} Punto;

double calculaDistanciaAOrigen(Punto *p) {
    return sqrt(p->x * p->x + p->y * p->y);
}
```

Uso: `Punto p = {3.0, 4.0}; double dist = calculaDistanciaAOrigen(&p);`

La diferencia fundamental es que `this` es implícito en Java. En C, la palabra clave `this` no existe y el programador debe pasar explícitamente el puntero al struct (`&p`) a cada función. En Java, cuando se invoca `p.calculaDistanciaAOrigen()`, el objeto `p` se pasa automáticamente "detrás de escenas", haciendo que el código sea más limpio. El compilador de Java traduce internamente los métodos en funciones C-like que reciben implícitamente la referencia al objeto (equivalente a `this` o al puntero `p` de C).