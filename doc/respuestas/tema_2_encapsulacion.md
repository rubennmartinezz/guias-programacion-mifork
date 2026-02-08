<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

### Respuesta

La encapsulación, en esencia, busca agrupar los datos (atributos) con las operaciones que actúan sobre ellos (métodos) dentro de una misma unidad, la clase. La ocultación de información, íntimamente relacionada, consiste en restringir el acceso directo a ciertos datos internos del objeto, exponiendo únicamente la interfaz necesaria para interactuar con él. De esta forma, se establece una separación clara entre lo que el usuario de la clase necesita conocer y cómo internamente se implementan las funcionalidades.

Entre las ventajas de la ocultación de información destaca la posibilidad de modificar la implementación interna sin afectar al código que utiliza la clase, siempre que la interfaz pública permanezca igual. Esto proporciona flexibilidad y facilita el mantenimiento y evolución del código. Además, permite proteger la consistencia de los datos, asegurando que solo se realizan operaciones válidas sobre ellos. También mejora la legibilidad del código al indicar claramente cuál es la responsabilidad de cada componente y reduce la complejidad aparente de una clase ocultando los detalles innecesarios.


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### Respuesta

La interfaz pública de una clase es el conjunto de métodos y, ocasionalmente, atributos que están disponibles para ser utilizados por otros programadores o partes del programa. Representa el "contrato" que la clase ofrece, indicando qué funcionalidades se pueden invocar y cómo hacerlo. Es lo que el programador que usa la clase necesita conocer para trabajar con ella correctamente.

La ocultación de información está directamente relacionada con la interfaz pública. Mientras que la interfaz pública muestra lo que es accesible, la ocultación determina qué no lo es. Los atributos y métodos privados quedan ocultos, forzando al usuario de la clase a interactuar únicamente a través de la interfaz pública disponible. De esta manera, se asegura que se utiliza la clase de forma controlada, como el diseñador de la clase ha previsto, sin permitir acceso directo a datos internos que podrían comprometer la consistencia del objeto.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### Respuesta

La interfaz pública de una clase es lo que otros programadores verán y usarán, por lo que su diseño debe ser cuidadoso desde el inicio. Una interfaz mal diseñada puede resultar en código complicado de usar o que no refleje adecuadamente las responsabilidades de la clase. Además, una vez que la interfaz pública se ha utilizado en otros lugares del programa o, aún peor, en código utilizado por otros desarrolladores, modificarla se vuelve muy problemático.

Cambiar la interfaz pública de una clase es difícil porque requiere modificar también todo el código que la depende, potencialmente afectando a muchas partes del programa. Por esta razón, es fundamental pensar bien desde el inicio en qué métodos debe ofrecer la clase, cómo deben denominarse y qué parámetros requieren. Un buen diseño inicial evita costosos cambios futuros.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Respuesta

Las invariantes de clase son condiciones que deben cumplirse siempre en un objeto durante toda su vida útil. Por ejemplo, en una clase que representa una Cuenta Bancaria, una invariante podría ser que el saldo nunca sea negativo, o que la edad de una Persona siempre sea un número positivo. Son restricciones lógicas que definen cuándo un objeto se encuentra en un estado válido.

La ocultación de información ayuda a proteger las invariantes de clase porque impide que el código externo acceda directamente a los atributos y los modifique de forma arbitraria. Al mantener los atributos como privados y proporcionar solo métodos públicos controlados, se puede asegurar que siempre se comprueban las condiciones antes de cualquier modificación. De esta manera, es imposible que factores externos dejen el objeto en un estado inconsistente o inválido.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### Respuesta

```java
public class Punto {
    private double x;
    private double y;
    
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
```

En esta clase, los atributos `x` e `y` están marcados como `private`, lo que significa que solo pueden ser accedidos desde dentro de la propia clase. Esto impide que código externo modifique las coordenadas directamente, garantizando que el estado del punto se mantenga consistente. La palabra clave `public`, aplicada al constructor y al método, indica que estos son accesibles desde cualquier lugar del programa, formando la interfaz pública.

La interfaz pública de la clase `Punto` está formada por el constructor `Punto(double, double)` y el método `calcularDistanciaAOrigen()`. El `public` permite que cualquier código use estos elementos, mientras que `private` los restricta únicamente al interior de la clase. Esta combinación logra que la clase sea segura y controlada, exponiendo solo lo necesario para su uso correcto.


## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### Respuesta

Los modificadores `public` y `private` en Java se pueden aplicar tanto a atributos (variables miembro) como a métodos. También se pueden aplicar a las clases internas (inner classes), aunque esto es un concepto más avanzado. Sin embargo, una clase de nivel superior (no interna) solo puede ser `public` o no tener modificador de visibilidad; no puede ser `private`.


## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Respuesta

Existen más niveles de visibilidad además de público y privado. En Java, además de `public` y `private`, existen `protected` y el acceso de paquete (sin modificador). El acceso `protected` permite que miembros sean accesibles dentro de la clase, sus subclases, y otras clases en el mismo paquete. El acceso de paquete (cuando no se especifica ningún modificador) restringe el acceso a clases dentro del mismo paquete, siendo más restrictivo que `public` pero menos que `private`.

Otros lenguajes presentan variaciones en estos niveles. C++ utiliza `public`, `private` y `protected`, siendo muy similar a Java aunque el acceso de paquete no existe. Python no utiliza modificadores de visibilidad en el sentido estricto, pero emplea convenciones como guiones bajos para indicar miembros privados. C# implementa `public`, `private`, `protected`, `internal` y combinaciones como `protected internal`. Estas diferencias reflejan los distintos enfoques de cada lenguaje hacia el control de visibilidad.


## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Respuesta

```java
public class Punto {
    private double x;
    private double y;
    
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double calcularDistanciaAPunto(Punto otro) {
        double dx = this.x - otro.x;  // Acceso a otro.x
        double dy = this.y - otro.y;  // Acceso a otro.y
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```

La respuesta es que los miembros privados están ocultos para **(a) otras clases**, no para otras instancias de la misma clase. En el método `calcularDistanciaAPunto`, se accede directamente a los atributos privados `x` e `y` del objeto `otro`, aunque sea privado. Esto es posible porque el método pertenece a la clase `Punto`, y en Java, los miembros privados son accesibles desde cualquier método de la misma clase, independientemente de la instancia a la que pertenezcan.

Esta característica tiene sentido: si dos objetos de la misma clase no pudieran acceder a los datos privados del otro, sería imposible implementar métodos que comparen o trabajen con múltiples instancias. El nivel `private` restringe el acceso a otras clases, pero no a otras instancias de la propia clase.


## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Respuesta

Los métodos getter son métodos públicos que permiten consultar (leer) el valor de un atributo privado. Por convención en Java, suelen nombrase anteponiendo `get` al nombre del atributo, por ejemplo, `getX()` para obtener el valor de `x`. Los métodos setter, por el contrario, son métodos públicos que permiten modificar (escribir) el valor de un atributo privado, usando la convención `set` seguido del nombre del atributo, como `setX(double valor)`.

Estos métodos son fundamentales en la encapsulación porque proporcionan un control granular sobre el acceso a los atributos. A través de un getter, se puede permitir la lectura sin modificación del estado. A través de un setter, se pueden aplicar validaciones antes de permitir que se modifique un atributo, asegurando que las invariantes de clase se mantienen. Por ejemplo, en una clase que representa una edad, un setter podría validar que la edad introducida sea positiva, evitando valores inválidos.


## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Respuesta

No, el concepto de "seguridad" en el contexto de la ocultación de información no se refiere a protección contra ataques informáticos o "hacking" en el sentido tradicional. Se refiere más bien a la seguridad lógica y la integridad del programa, es decir, a evitar que partes del código realicen acciones no permitidas o inconsistentes con el diseño previsto.

La ocultación de información mejora la seguridad al impedir que se acceda o modifique indebidamente el estado interno de los objetos desde lugares no autorizados. Esto protege contra errores de programación, inconsistencias de datos y comportamientos inesperados. Por ejemplo, evita que alguien modifique accidentalmente una coordenada de un `Punto` de forma inválida, o que anule el estado consistente de un objeto. Es una forma de "seguridad" desde el punto de vista de la calidad del código y la robustez de las estructuras de datos, no de protección contra ataques malintencionados.


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Respuesta

Un miembro de instancia es un atributo o método que pertenece a cada objeto individual creado a partir de la clase. Cada instancia tiene su propia copia del miembro de instancia con valores potencialmente diferentes. Por el contrario, un miembro de clase (también llamado miembro estático) pertenece a la clase misma, no a las instancias individuales. Existe una única copia compartida por todas las instancias de la clase, independientemente de cuántos objetos se creen.

En Java, los miembros de clase se declaran con la palabra clave `static`. Un ejemplo sencillo: si se tiene un contador de cuántas instancias de una clase se han creado, ese contador sería un miembro de clase porque es compartido. Los miembros de clase también se pueden ocultar usando los modificadores `private`, `public`, `protected`, etc., de la misma forma que los miembros de instancia. La ocultación funciona idénticamente: un miembro de clase privado solo es accesible desde dentro de la clase, mientras que uno público es accesible desde cualquier lugar.


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta

Sí, los constructores privados tienen sentido en ciertos contextos. El caso más común es cuando se desea evitar que el constructor sea llamado directamente desde código externo. Esto puede combinarse con métodos factoría estáticos (métodos públicos que crean y devuelven instancias) para controlar cómo se crean los objetos.

Por ejemplo, en una clase que representa un Singleton (un patrón de diseño donde solo debe existir una única instancia), el constructor se declara privado para garantizar que no se pueden crear múltiples instancias. Otro caso es cuando se desea forzar a que los objetos se creen únicamente a través de métodos factoría que aplican validaciones o transformaciones previas, como redondear coordenadas antes de crear un `Punto`.


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta

```java
public class Punto {
    private double x;
    private double y;
    private static double xMaximo = Double.NEGATIVE_INFINITY;
    private static double yMaximo = Double.NEGATIVE_INFINITY;
    
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
        if (x > xMaximo) xMaximo = x;
        if (y > yMaximo) yMaximo = y;
    }
    
    public static double getXMaximo() {
        return xMaximo;
    }
    
    public static double getYMaximo() {
        return yMaximo;
    }
}
```

Los miembros de clase en Java se indican con la palabra clave `static` antes del tipo de dato. En el ejemplo anterior, `xMaximo` e `yMaximo` son miembros de clase, lo que significa que son compartidos por todas las instancias de `Punto`. Cada vez que se crea un nuevo punto, el constructor actualiza estos valores máximos si es necesario.

Para acceder a miembros de clase desde fuera de la clase, se utiliza el nombre de la clase seguido de un punto, por ejemplo `Punto.getXMaximo()`. Nótese que no es necesario tener una instancia para acceder a estos miembros. Los miembros de clase son especialmente útiles para mantener información compartida que afecta a toda la clase, como contadores, valores globales o constantes.


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Respuesta

```java
public static Punto crearPuntoRedondeado(double x, double y) {
    double xRedondeado = Math.round(x);
    double yRedondeado = Math.round(y);
    return new Punto(xRedondeado, yRedondeado);
}
```

Sí, se ha usado `static`. Un método factoría es un método estático que actúa como alternativa a los constructores para crear instancias. En este caso, el método `crearPuntoRedondeado` es estático, lo que permite invocarlo sin necesidad de una instancia preexistente usando `Punto.crearPuntoRedondeado(5.7, 3.2)`. El método redondea las coordenadas antes de pasar al constructor, asegurando que el `Punto` creado tenga siempre coordenadas enteras. Este patrón es útil cuando se desea aplicar transformaciones, validaciones o lógica especial antes de la creación del objeto.


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta

```java
public class Punto {
    private double[] coordenadas;
    
    public Punto(double x, double y) {
        coordenadas = new double[2];
        coordenadas[0] = x;
        coordenadas[1] = y;
    }
    
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(coordenadas[0] * coordenadas[0] + 
                         coordenadas[1] * coordenadas[1]);
    }
}
```

Esta es una demostración práctica de la ventaja de la encapsulación: al mantener los datos privados, es posible cambiar completamente la implementación interna sin afectar al código que utiliza la clase. La interfaz pública permanece idéntica (constructor con dos `double` y método `calcularDistanciaAOrigen`), pero internamente se utiliza un array en lugar de dos atributos individuales.

Desde la perspectiva del usuario de la clase, nada ha cambiado: se sigue invocando `new Punto(3.0, 4.0)` y se puede llamar a `calcularDistanciaAOrigen()` de la misma forma. Este cambio es posible porque el usuario nunca accedió directamente a `x` e `y`; solo interactuaba a través de la interfaz pública. Este es un ejemplo perfecto de por qué la encapsulación es valiosa: permite flexibilidad interna sin romper el contrato con los clientes de la clase.


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta

No, aunque a primera vista parece lo mismo, tener un atributo privado con getter y setter públicos ofrece ventajas que un atributo público no proporciona. Un atributo público permite lecturas y escrituras sin restricciones, mientras que un setter permite insertar lógica de validación. Por ejemplo, un setter para una edad puede verificar que el valor sea positivo, algo que no es posible si el atributo es público.

La convención más habitual en Java es que los atributos sean privados y se expongan únicamente a través de getters y setters públicos. Esto es considerado una buena práctica de encapsulación. Esta convención está directamente relacionada con las invariantes de clase: un atributo privado permite garantizar que las invariantes se mantienen mediante validaciones en los setters. Por ejemplo, si la invariante es que la edad debe ser no negativa, el setter puede rechazar valores inválidos. Si el atributo fuera público, cualquier código externo podría violar la invariante asignando un valor negativo directamente, comprometiendo la integridad del objeto.


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta

Una clase inmutable es aquella cuyos objetos no pueden ser modificados después de su creación. Una vez se crea una instancia, su estado permanece constante durante toda su vida útil. Un método modificador es cualquier método que cambia el estado interno de un objeto. Un setter es un tipo específico de método modificador, pero no todo método modificador es un setter. Por ejemplo, un método `redimensionar()` que cambia el tamaño de un rectángulo es un modificador, pero no es un setter en el sentido tradicional.

Hay varias ventajas de tener clases inmutables. Primero, son más seguras para usar en entornos multihilo, ya que no hay riesgo de que un hilo modifique el estado mientras otro lo lee. Segundo, permiten optimizaciones del compilador y pueden ser compartidas sin problemas. Las clases inmutables también son más fáciles de razonar sobre ellas: su comportamiento es predecible. En Java, ejemplos de clases inmutables incluyen `String`, `Integer`, y `LocalDate`. Para crear una clase inmutable, se declaran los atributos `private final`, se inicializan solo en el constructor, y se proporciona únicamente getters sin setters.


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta

No, no es recomendable incluir setters para todos los atributos de forma automática. Los setters deben incluirse únicamente cuando tiene sentido permitir que un atributo sea modificado después de la creación del objeto. Si un atributo es esencial para la identidad o la integridad del objeto y no debe cambiar, no se debe proporcionar setter alguno.

La decisión de incluir un setter debe ser consciente y debe responder a la pregunta: ¿Tiene sentido que este valor cambie después de la creación del objeto? Por ejemplo, en una clase `Persona`, la edad puede cambiar a lo largo del tiempo, por lo que un setter tiene sentido. Sin embargo, el identificador único de la persona probablemente no debería cambiar, así que no se proporcionaría un setter. Proporcionar setters innecesarios debilita la encapsulación y permite que el código externo modifique el objeto de formas que el diseñador de la clase quizás no tuvo en cuenta, violando potencialmente las invariantes de clase.


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta

La clase `String` en Java es inmutable. Una vez que se crea un objeto `String`, su contenido no puede ser modificado. Cuando se concatenan dos cadenas usando el operador `+`, por ejemplo `"Hola" + " Mundo"`, lo que realmente ocurre es que Java crea un nuevo objeto `String` que contiene el resultado de la concatenación, y el original permanece sin cambios. Los objetos `String` originales no son modificados.

Esta característica de inmutabilidad tiene implicaciones importantes para el rendimiento. Si se va a construir una cadena muy larga concatenando muchas veces dentro de un bucle, el uso repetido del operador `+` crear muchos objetos `String` intermedios, lo que es ineficiente. Para este caso, Java proporciona la clase `StringBuilder`, que es mutable y permite construir cadenas de forma eficiente. Se puede utilizar `StringBuilder` para acumular el contenido y, al final, llamar a `toString()` para obtener el resultado como un `String` inmutable. Usar `StringBuilder` en lugar de concatenación con `+` en bucles puede mejorar significativamente el rendimiento cuando se trabaja con cadenas largas.


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### Respuesta

Por defecto, los objetos se comparan por identidad, no por contenido. Esto significa que dos objetos se consideran iguales únicamente si son exactamente el mismo objeto en memoria, es decir, si apuntan a la misma dirección de memoria. El operador `==` comprueba justamente esto: identidad. Si se crea dos objetos `Punto` con las mismas coordenadas, `punto1 == punto2` será falsopor que son objetos distintos en memoria, aunque tengan el mismo contenido.

El método `equals` en Java es un método heredado de la clase `Object` (la clase base de todas las clases Java) que por defecto también compara por identidad, haciendo exactamente lo mismo que `==`. Sin embargo, muchas clases sobreescriben (override) el método `equals` para proporcionar una comparación por contenido. Por ejemplo, `String.equals()` compara el contenido de las cadenas, no su identidad en memoria.

Para comparar dos cadenas en Java, se debe usar siempre el método `equals()`, nunca el operador `==`. `"Hola".equals("Hola")` retorna `true`, mientras que dos variables de tipo `String` que contienen "Hola" podrían regresar `false` con `==` porque podrían ser objetos distintos en memoria. Si se desea una comparación sin distinción entre mayúsculas y minúsculas, se puede usar `equalsIgnoreCase()`.


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta

Las clases wrapper (envolventes) son clases que "envuelven" los tipos primitivos de Java, proporcionando una interfaz orientada a objetos para trabajar con ellos. Los tipos primitivos en Java (`int`, `double`, `boolean`, etc.) no son objetos y, por tanto, no tienen métodos. Las clases wrapper corresponden: `Integer` para `int`, `Double` para `double`, `Boolean` para `boolean`, etc. Permiten convertir un valor primitivo en un objeto, dotándolo de funcionalidades adicionales como métodos para conversión de tipos o comparación.

En Java, el proceso de empaquetar un primitivo en su wrapper se llama "autoboxing" y es automático. El compilador realiza la conversión de forma transparente cuando es necesario. Por ejemplo, `Integer numero = 5;` encapsula automáticamente el `int` 5 en un objeto `Integer`. Las clases wrapper proporcionan ventajas como la capacidad de usar tipos primitivos en colecciones (que requieren objetos), métodos útiles para conversión y manipulación, y la posibilidad de representar un valor "nulo" (las clases wrapper pueden ser `null`, los primitivos no).

No todos los lenguajes orientados a objetos tienen tipos primitivos. Algunos lenguajes como Python o Ruby tratan todo como objetos, incluso los números. Otros, como C++, tienen un sistema de tipos más complejo. Java optó por mantener los tipos primitivos por razones de rendimiento (los primitivos son más rápidos que los objetos), pero proporciona las clases wrapper para situaciones donde se necesita la funcionalidad de objetos.


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta

Un tipo de dato enumerado, o enumeración, es un tipo de dato que define un conjunto finito y predeterminado de valores posibles. En lugar de permitir cualquier valor (como en un `int`), especifica explícitamente las únicas opciones válidas. Por ejemplo, un enumerado para los días de la semana tendría exactamente siete valores: LUNES, MARTES, MIÉRCOLES, etc. Los enumerados son útiles para representar conceptos que naturalmente tienen un conjunto limitado de opciones.

En Java, un tipo de dato enumerado es efectivamente una clase especial. Java proporciona la palabra clave `enum` para definir enumeraciones de forma sencilla. Los valores del enumerado son instancias estáticas de la clase, lo que significa que hay un único objeto para cada valor. En términos de encapsulación, los enumerados ofrecen ventajas significativas: garantizan que una variable solo puede tomar uno de los valores predefinidos, eliminando la posibilidad de valores inválidos. Esto protege las invariantes de clase y previene errores en tiempo de ejecución. Además, los enumerados pueden tener atributos privados, métodos y constructores privados, permitiendo un control completo sobre su contenido interno, como en cualquier clase regular.


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado. Añade además cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta

```java
public enum Mes {
    ENERO(31, 1),
    FEBRERO(28, 2),
    MARZO(31, 3),
    ABRIL(30, 4),
    MAYO(31, 5),
    JUNIO(30, 6),
    JULIO(31, 7),
    AGOSTO(31, 8),
    SEPTIEMBRE(30, 9),
    OCTUBRE(31, 10),
    NOVIEMBRE(30, 11),
    DICIEMBRE(31, 12);
    
    private final int dias;
    private final int ordinal;
    
    Mes(int dias, int ordinal) {
        this.dias = dias;
        this.ordinal = ordinal;
    }
    
    public int getDias() {
        return dias;
    }
    
    public int getOrdinal() {
        return ordinal;
    }
    
    public boolean esDePrimavera(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == MARZO || this == ABRIL || this == MAYO;
        } else {
            return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
        }
    }
    
    public boolean esDeVerano(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == JUNIO || this == JULIO || this == AGOSTO;
        } else {
            return this == DICIEMBRE || this == ENERO || this == FEBRERO;
        }
    }
    
    public boolean esDeOtoño(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
        } else {
            return this == MARZO || this == ABRIL || this == MAYO;
        }
    }
    
    public boolean esDeInvierno(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == DICIEMBRE || this == ENERO || this == FEBRERO;
        } else {
            return this == JUNIO || this == JULIO || this == AGOSTO;
        }
    }
}
```

Este enumerado demuestra las capacidades avanzadas de los enumerados en Java. Cada valor del enumerado (ENERO a DICIEMBRE) es una instancia de la clase `Mes` y se construye utilizando un constructor privado que recibe el número de días y el ordinal. Los atributos `dias` y `ordinal` son privados y se inicializan en el constructor, garantizando que no pueden ser modificados de forma externa.

Los métodos `getDias()` y `getOrdinal()` proporcionan acceso controlado a estos valores. Los cuatro métodos de estación trabajan con lógica condicional para determinar si el mes contiene días de una estación específica, teniendo en cuenta si se está en el hemisferio norte o sur. Esta estructura muestra cómo los enumerados pueden encapsular comportamiento complejo mientras mantienen la garantía de que solo hay doce valores válidos posibles, eliminando completamente la posibilidad de meses inválidos en el programa.
