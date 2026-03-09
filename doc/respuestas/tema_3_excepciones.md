<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

### Respuesta

En C no hay excepciones, por lo que la forma usual de reportar un error desde una función es usando valores de retorno especiales y/o parámetros de salida adicionales. Una opción consiste en que la función devuelva un valor que indique el error (por ejemplo, `-1` o `NAN`) y dejar que el llamador compruebe ese valor antes de usarlo.

Otra opción es trabajar con un parámetro de salida adicional (por referencia) que lleve el resultado, mientras que la función devuelve un código de estado (0 = éxito, distinto de 0 = error). De esta manera, el llamador decide cómo informar al usuario sin que la función `raiz` tenga que imprimir nada.

```c
#include <stdio.h>
#include <math.h>
#include <errno.h>

/* Opción 1: devolver un valor especial (NAN) */
double raiz1(double x) {
    if (x < 0.0) {
        return NAN; /* El llamador debe verificar isnan */
    }
    return sqrt(x);
}

/* Opción 2: usar un parámetro de salida y devolver código de error */
int raiz2(double x, double *out) {
    if (x < 0.0) {
        return -1; /* error */
    }
    *out = sqrt(x);
    return 0; /* ok */
}

int main(void) {
    double x = -4.0;
    double r;

    double r1 = raiz1(x);
    if (isnan(r1)) {
        printf("Error: entrada negativa\n");
    } else {
        printf("Raiz: %f\n", r1);
    }

    if (raiz2(x, &r) != 0) {
        printf("Error: entrada negativa\n");
    } else {
        printf("Raiz: %f\n", r);
    }
    return 0;
}
```

## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Respuesta

Una excepción es un mecanismo para señalar que ha ocurrido una condición anómala durante la ejecución de un programa, de forma que el flujo normal se interrumpe y la situación puede propagarse hasta un lugar que sepa manejarla. En lenguajes como Java, las excepciones son objetos que describen el error y pueden incluir detalles como un mensaje o una causa.

El programador utiliza excepciones para separar la lógica normal de la lógica de error: cuando se implementa una función, se lanza (throw) una excepción para indicar que no se puede continuar con el resultado, y cuando se llama a esa función, se puede capturar (catch) la excepción para tomar decisiones de recuperación o mostrar un mensaje al usuario.

## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### Respuesta

En Java se suele encapsular la lógica en clases. Se puede crear una clase `Calculadora` con un método `raiz` que lanza una excepción si el argumento es negativo. Desde `main` se llama a ese método dentro de un bloque `try` y se controla la excepción en un bloque `catch`.

```java
public class Calculadora {
    public static double raiz(double x) {
        if (x < 0) {
            throw new IllegalArgumentException("No se puede calcular la raíz de un número negativo");
        }
        return Math.sqrt(x);
    }

    public static void main(String[] args) {
        double x = -4.0;
        try {
            double r = raiz(x);
            System.out.println("Raiz: " + r);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Respuesta

Lanzar una excepción (throw) es crear un objeto de excepción y detener inmediatamente el flujo normal de ejecución para buscar un manejador adecuado. Controlar o capturar una excepción consiste en tener un bloque `catch` que se activa cuando se lanza una excepción compatible, permitiendo ejecutar código de recuperación o de informe.

Propagar una excepción significa que, si una función lanza una excepción y no tiene ningún `catch` que la capture, la excepción sube a la función que la llamó, y así sucesivamente por la pila de llamadas hasta llegar al `main` o hasta que se encuentra un manejador. Las funciones intermedias no se reanudan después de que la excepción pasa por ellas: se abandonan inmediatamente y su ejecución no continúa después del punto donde se lanzó la excepción.

En el ejemplo de `Calculadora.raiz`, cuando se lanza `IllegalArgumentException`, el método se detiene, vuelve al `main`, y el bloque `catch` en el `main` captura la excepción. Si no hubiera un `catch` en el `main`, la excepción se propagaría fuera del programa y terminaría con un mensaje de error.

## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### Respuesta

La propagación natural evita que cada función intermedia tenga que comprobar manualmente el valor de retorno y reenviar códigos de error, lo que reduce la complejidad del código y disminuye la probabilidad de olvidos. En C, cada llamada debe revisar el resultado y decidir cómo reaccionar o reenviar el error, lo que genera mucho código repetitivo.

Con excepciones, la lógica de manejo puede centralizarse en un lugar adecuado (por ejemplo, en el nivel más alto de la aplicación), lo que facilita mantener un flujo de control claro y permite al código de negocio concentrarse en la funcionalidad principal sin mezclarlo con comprobaciones de error constantes.

## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### Respuesta

En Java, las excepciones son instancias de clases que heredan de `Throwable` (normalmente `Exception` o `RuntimeException`). Como objetos, pueden empaquetar datos (mensaje, causa, estado) y proporcionar métodos para acceder a ellos, lo que ayuda a encapsular la información del error.

Esta encapsulación permite que el código que lanza la excepción no tenga que conocer cómo se va a manejar: simplemente crea la excepción con los detalles relevantes y el manejador puede inspeccionarla mediante sus métodos públicos. Además, se pueden crear excepciones personalizadas (heredando de `Exception` o `RuntimeException`) para transmitir significados específicos de dominio o capas de la aplicación.

## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Respuesta

Un objeto excepción en Java suele llevar al menos un mensaje descriptivo (por ejemplo, `"No se puede calcular la raíz de un número negativo"`) y una traza de pila (stack trace) que indica dónde se lanzó la excepción. También puede incluir una causa (`Throwable cause`) que referencia otra excepción que originó el problema.

Esa información es útil para el manejador porque permite distinguir entre diferentes errores (mediante el tipo de excepción), obtener detalles de qué ocurrió (mensaje) y saber dónde en el código se produjo (traza). En C no existe un objeto unificado, por lo que el llamador tendría que construir manualmente esa información si quiere algo similar.

## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### Respuesta

Sí, en Java se pueden encadenar varios bloques `catch` después de un mismo bloque `try`. Cada `catch` puede capturar un tipo diferente de excepción. Sin embargo, cuando se lanza una excepción, solo se ejecuta el primer `catch` cuyo tipo coincide con la excepción lanzada (o con un supertipo).

Los demás bloques `catch` no se ejecutan una vez que uno ha capturado la excepción. El flujo continúa después del último `catch` (y del `finally`, si existe).

## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### Respuesta

En Java se utiliza un bloque `finally` asociado a un `try`. El código dentro de `finally` se ejecuta siempre, ya haya ocurrido o no una excepción, y aunque la excepción se propague fuera del método. Esto permite liberar recursos (cerrar ficheros, sockets, etc.) de forma segura.

En el ejemplo se muestra primero un `try` con `catch` y `finally`, y después un `try` con `finally` sin `catch`, donde la excepción se propaga pero el cierre se ejecuta igualmente.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class EjemploFinally {
    public static void main(String[] args) {
        BufferedReader reader = null;
        try {
            reader = new BufferedReader(new FileReader("datos.txt"));
            String linea = reader.readLine();
            System.out.println(linea);
        } catch (IOException e) {
            System.out.println("Error leyendo el fichero: " + e.getMessage());
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException ignored) {
                    // no hay mucho más que hacer
                }
            }
        }

        // Ejemplo sin catch, la excepción se propaga pero finally sigue ejecutándose
        try {
            reader = new BufferedReader(new FileReader("otro.txt"));
            System.out.println(reader.readLine());
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException ignored) {
                    // incluso aquí se puede ignorar
                }
            }
        }
    }
}
```

## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta

Sí, en Java se puede tener un bloque `try` con `finally` sin ningún `catch`. En ese caso, si ocurre una excepción dentro del `try`, se ejecuta el `finally` y luego la excepción se propaga hacia arriba. Si no ocurre ninguna excepción, también se ejecuta el `finally` antes de continuar con el resto del método.

Incluso si hay un `return` dentro del `try`, el bloque `finally` se ejecuta antes de que el método devuelva el valor. Por lo tanto, `finally` es un lugar fiable para liberar recursos o realizar acciones de limpieza, independientemente de cómo se salga del bloque `try`.

## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta

En Java, las excepciones controladas (checked exceptions) son aquellas que el compilador fuerza a declarar con `throws` o a capturar con `try-catch`. Están pensadas para condiciones que el código puede manejar razonablemente, como errores de E/S. Las excepciones no controladas (unchecked exceptions) heredan de `RuntimeException` y no requieren declaración ni captura; se usan para errores de programación que normalmente no se corrigen en tiempo de ejecución.

`RuntimeException` es la clase base para las excepciones no controladas; su presencia indica que el error es del tipo «nunca debería ocurrir si el código es correcto». Ejemplos comunes: `NullPointerException`, `IndexOutOfBoundsException`, `IllegalArgumentException`.

Ejemplos típicos:
- Controladas: `IOException` (lectura/escritura de ficheros), `SQLException` (acceso a bases de datos), `ClassNotFoundException` (carga dinámica de clases), `FileNotFoundException`.
- No controladas: `NullPointerException`, `IllegalArgumentException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException`.

Situaciones donde suele preferirse cada una:
- Excepciones controladas (se espera manejar):
  1. Acceso a ficheros externos.
  2. Operaciones de red (timeout, desconexión).
  3. Conversión de formatos (parseo con posibilidad de fallar).
  4. Interacción con el usuario (entrada inválida en un formulario).
- Excepciones no controladas (errores de programación):
  1. Índice fuera de rango al acceder a un array.
  2. Uso de `null` donde se requiere un objeto.
  3. División por cero en operaciones enteras.
  4. Paso de argumentos inválidos a un método público.

## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta

La cláusula `throws` en la firma de un método declara que dicho método puede lanzar una excepción controlada y que el llamador debe ocuparse de ella (capturándola o propagándola también). Es una forma de documentar y obligar en tiempo de compilación que se tenga en cuenta el manejo de ese tipo de error.

Usar `throws` es una alternativa a capturar la excepción dentro del mismo método cuando este no puede determinar la mejor forma de recuperarse. En ese caso, se delega la responsabilidad al nivel superior, que quizá tenga más contexto para decidir cómo actuar.

## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta

En este ejemplo se muestra un método `leerPrimeraLinea` que declara `throws IOException`. El método no captura la excepción de apertura de fichero; en cambio, se asegura de cerrar el recurso en `finally` (o bien con try-with-resources, pero aquí se presenta la forma clásica con `finally`). El llamador decide cómo manejar la excepción.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FicheroUtil {
    public static String leerPrimeraLinea(String ruta) throws IOException {
        BufferedReader reader = null;
        try {
            reader = new BufferedReader(new FileReader(ruta));
            return reader.readLine();
        } finally {
            if (reader != null) {
                reader.close();
            }
        }
    }
}

// Llamador:
// try {
//     String linea = FicheroUtil.leerPrimeraLinea("datos.txt");
// } catch (IOException e) {
//     // Manejo o mensaje de error
// }
```

## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta

Sí, técnicamente se puede declarar `throws RuntimeException` (o cualquier subtipo), pero no es obligatorio. Dado que las excepciones no controladas no están sujetas a verificación del compilador, el método llamador no tiene que capturarlas ni declararlas.

Capturarlas puede tener sentido cuando se desea proteger una frontera de la aplicación (por ejemplo, en el `main` de un programa o en una capa de red, GUI o servidor) para evitar que un error de programación no manejado haga caer toda la aplicación. En ese caso, se trata de añadir seguridad en tiempo de ejecución, más que de cumplir una regla del compilador.

## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta

Se recomienda usar excepciones controladas cuando el error es una condición recuperable o previsible que el llamador puede tratar de forma razonable (por ejemplo, un recurso externo no disponible). Las excepciones no controladas se usan para indicar errores de programación (argumentos inválidos, estados inconsistentes) que normalmente deben corregirse durante el desarrollo.

No todos los lenguajes tienen la distinción entre excepciones chequeadas y no chequeadas. Por ejemplo, C++ y Python solo tienen excepciones no controladas (en el sentido de que el compilador no obliga a capturarlas), lo cual es la opción más habitual en muchos entornos. En Java, la distinción existe, pero en otros lenguajes con excepción única (como C++ o Python) se suele trabajar siempre con excepciones que pueden propagarse libremente.

## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta

Sí, lanzar excepciones dentro de un `catch` tiene sentido cuando se desea transformar un error bajo nivel en otro de más alto nivel, o cuando se quiere añadir información adicional antes de seguir propagando el error. También es útil para encapsular detalles internos y no exponerlos fuera de una capa.

Se puede relanzar la misma excepción capturada usando `throw;` (sin argumentos) en Java, lo que es útil cuando se desea ejecutar código adicional (por ejemplo, registrar un mensaje) y luego dejar que el error siga su camino. Otra alternativa es lanzar una nueva excepción, posiblemente con la excepción original como causa.

```java
try {
    // código que puede fallar
} catch (IOException e) {
    // registrar o limpiar algo
    System.err.println("Error de E/S: " + e.getMessage());
    throw e; // relanzar la misma excepción
}

try {
    // código que puede fallar
} catch (IOException e) {
    throw new RuntimeException("No se pudo procesar el archivo", e); // envolver con causa
}
```

## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta

Una excepción puede tener otra excepción como causa para representar que un error de nivel superior fue provocado por un error de nivel inferior. En Java, muchas excepciones aceptan un argumento `Throwable cause` en el constructor; de este modo se preserva la información original mientras se lanza una excepción con un significado más apropiado para el nivel superior.

Cuando se imprime una excepción en pantalla (por ejemplo, con `e.printStackTrace()`), la causa aparece en la traza, mostrando la excepción original y su stack trace anidado debajo de la excepción envolvente.

```java
public class ExcepcionServicio extends Exception {
    public ExcepcionServicio(String msg, Throwable cause) {
        super(msg, cause);
    }
}

public class Servicio {
    public void procesar(String ruta) throws ExcepcionServicio {
        try {
            // código que puede lanzar IOException
            throw new java.io.IOException("No se puede leer el fichero");
        } catch (java.io.IOException e) {
            throw new ExcepcionServicio("Error en el servicio al procesar datos", e);
        }
    }
}

// Al capturar y llamar a e.printStackTrace(), se verá la ExcepcionServicio y, a continuación, la IOException como causa.
```
