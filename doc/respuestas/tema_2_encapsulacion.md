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


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Respuesta


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### Respuesta


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado. Añade además cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta
