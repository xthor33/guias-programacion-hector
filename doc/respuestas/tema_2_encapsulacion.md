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

 * Encapsulación: agrupar datos (atributos) y comportamiento (métodos) en una misma unidad (la clase/objeto) y controlar cómo se accede a esos datos.

* Ocultación de información: esconder los detalles internos (cómo está implementado por dentro) y exponer sólo lo necesario mediante una interfaz.

Ventajas típicas de ocultar información:

1. Evita estados inválidos: obligas a pasar por métodos que validan.

2. Menos errores: impides que el código externo “toquetee” campos críticos.

3. Mantenimiento más fácil: puedes cambiar la implementación interna sin romper a quien usa la clase.

4. Código más modular: cada clase se ocupa de su responsabilidad.

5. Menos acoplamiento: otras partes dependen de “lo que haces”, no de “cómo lo haces”


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

La interfaz pública de una clase/objeto es el conjunto de miembros accesibles desde fuera: normalmente, los métodos public (y a veces constantes public), es decir, lo que “ofreces” al mundo para usar tu objeto.

Relación con la ocultación:

La interfaz pública es “lo visible”.

La ocultación es “lo interno” (private) que no quieres que toquen.

La idea es que el usuario use la interfaz pública sin necesitar conocer (ni depender de) los detalles internos.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

Porque la interfaz pública es como un contrato: si otros programas/clases la usan, dependen de ella.

Si cambias nombres, parámetros o eliminas métodos public, puedes romper código que ya funcionaba.

En general, no es fácil cambiarla si ya está en uso: implica actualizar todo lo que dependa de esa interfaz.

Por eso conviene diseñarla pensando en:

simplicidad,

claridad,

lo mínimo necesario,

y estabilidad.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

Las invariantes de clase son condiciones o reglas lógicas que siempre deben cumplirse para que un objeto se considere en un estado válido (ejemplo: edad >= 0, radio > 0, saldo >= límite_mínimo, etc.).
La ocultación de información ayuda porque:

Impide que código externo modifique directamente los atributos y rompa las invariantes.
Obliga a que cualquier cambio de estado pase por métodos controlados (constructores, setters, otros métodos), donde se pueden validar y garantizar que las invariantes se mantengan.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

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

    public double getX() { return x; }
    public double getY() { return y; }
}

Interfaz pública de Punto (lo que se puede usar desde fuera):

Punto(double x, double y) (constructor público)

calcularDistanciaAOrigen()

getX(), getY()

public:

Accesible desde cualquier clase (según reglas de paquetes/módulos, pero “en general” es público total).

private:

Accesible sólo dentro de la misma clase (Punto).

Ni otras clases ni clases hijas pueden acceder directamente a esos campos.


## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

En Java se aplican a:

Clases: pueden ser public o package-private (sin modificador). Ojo: una clase “top-level” (en su propio archivo) no puede ser private.

Atributos (campos): public, private, etc.

Métodos: public, private, etc.

Constructores: public, private, etc.

Clases internas (nested/inner classes): ahí sí puedes usar private, protected, etc.


## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

Sí, suele haber más.

En Java hay 4 niveles:

public (visible desde cualquier lugar)

protected (visible en el mismo paquete y en subclases)

(sin modificador) package-private (visible sólo dentro del mismo paquete)

private (visible sólo dentro de la clase)

En otros lenguajes:

C++: public, private, protected.

C#: además de public/private/protected, hay internal, protected internal, etc.

Python: no hay privacidad “fuerte” igual; se usa convención (_atributo) y mecanismos, pero se puede acceder igual.


## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

En Java, un miembro private está oculto para otras clases, pero no está oculto para otras instancias de la misma clase, porque el acceso se decide por clase, no por “objeto”.

Ejemplo:

public class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAPunto(Punto otro) {
        double dx = this.x - otro.x; // esto SÍ se permite
        double dy = this.y - otro.y; // aunque x e y sean private
        return Math.sqrt(dx * dx + dy * dy);
    }
}


Explicación:

otro.x se permite porque el código que accede (Punto) está dentro de la clase Punto.

Da igual que otro sea “otra instancia”: sigue siendo la misma clase.

Respuesta correcta: (a) otras clases.


## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

Son métodos para leer y modificar atributos privados de forma controlada:

Getter: devuelve el valor (getX()).

Setter: cambia el valor (setX(double x)), normalmente con validación.

Ejemplo:

public double getX() { return x; }

public void setX(double x) {
    this.x = x;
}


Importante: no siempre conviene poner setters para todo; a veces rompen invariantes o hacen el objeto demasiado “modificable”.


## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

No. Aquí “seguridad” significa robustez y protección contra mal uso dentro del propio programa:

evitar cambios accidentales,

evitar estados inválidos,

reducir errores,

controlar el acceso y la modificación.

No es una medida de ciberseguridad tipo “anti-hackers”; es más bien seguridad del diseño y de la corrección del software.


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

Miembro de instancia: pertenece a cada objeto. Cada instancia tiene su propia copia.

Ej: x e y de un Punto.

Miembro de clase: pertenece a la clase (una sola copia compartida por todas las instancias). En Java se hace con static.

Ej: un contador de cuántos Punto se han creado.

¿Se pueden ocultar los miembros de clase? Sí.
Un miembro static también puede ser private, protected, etc. (mismas reglas de visibilidad).


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

Sí. Se usan cuando quieres controlar cómo se crean los objetos, por ejemplo:

Singleton (una única instancia).

Métodos factoría (static) que validan, cachean, redondean, etc.

Para impedir que se cree la clase desde fuera (solo dentro del paquete o de la clase).


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

Con static.

Ejemplo (idea: guardar el mayor x e y vistos en cualquier Punto creado):

public class Punto {
    private double x, y;

    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    public static double getMaxX() { return maxX; }
    public static double getMaxY() { return maxY; }

    public double getX() { return x; }
    public double getY() { return y; }
}


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

public static Punto crearRedondeado(double x, double y) {
    return new Punto(Math.round(x), Math.round(y));
}
Sí, usa static porque es un método de clase: lo llamas como Punto.crearRedondeado(...).


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

public class Punto {
    private final double[] coords = new double[2]; // coords[0]=x, coords[1]=y

    public Punto(double x, double y) {
        coords[0] = x;
        coords[1] = y;
    }

    public double getX() { return coords[0]; }
    public double getY() { return coords[1]; }

    public double calcularDistanciaAOrigen() {
        double x = coords[0], y = coords[1];
        return Math.sqrt(x * x + y * y);
    }
}
La interfaz pública (constructor, getters, método distancia) puede quedarse igual; cambia solo el “por dentro”.


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

Aunque tengas get/set públicos, no conviene hacer el atributo público porque:

Con setters puedes validar (ej: no permitir valores inválidos).

Puedes cambiar la implementación interna (como el array de coords) sin romper código externo.

Puedes controlar cuándo y cómo cambia el estado.

Convención habitual: atributos private (encapsulación) y exponer lo necesario con métodos.

Sí, está relacionado con invariantes de clase: si dejas atributos públicos, cualquiera puede romper el estado válido sin pasar por validaciones.

## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

Clase inmutable: una vez creado el objeto, su estado no cambia.

Ej típico: String en Java.

Método modificador: método que cambia el estado interno del objeto (modifica atributos).

¿Un modificador es siempre un setter? No.

setX(...) es modificador, pero también lo sería mover(dx, dy) o normalizar(), etc.

Ventajas de inmutabilidad:

Más fácil razonar (no cambia “por sorpresa”).

Muy útil en concurrencia/hilos (menos problemas de sincronización).

Puedes compartir objetos sin miedo a efectos colaterales.

Menos bugs por estados intermedios inválidos.


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

No. Poner setters “por defecto” suele ser mala idea:

Debilita encapsulación.

Facilita romper invariantes.

Hace la clase demasiado “editable” desde fuera.

Mejor: exponer solo las operaciones que tengan sentido (métodos con intención), y usar setters solo cuando realmente sea necesario.


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

String en Java es inmutable.

Al concatenar (a + b), se crea una nueva cadena (nuevo objeto String) con el resultado.

Si vas a concatenar muchas veces en un bucle, usa:

StringBuilder (normalmente lo recomendado),

o StringBuffer si necesitas sincronización (más raro hoy).


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

En POO puedes comparar:

Identidad: “¿son el mismo objeto?” (misma referencia).

En Java: == para referencias.

Contenido: “¿tienen los mismos datos?”

En Java: normalmente con equals.

equals en Java:

Es un método de Object.

Por defecto (si no lo sobreescribes), se comporta como identidad (similar a ==).

Comparar dos String en Java:

Por contenido: s1.equals(s2) (o equalsIgnoreCase si procede).

== en String compara referencias, no el texto (puede “parecer” que funciona a veces por interning, pero no debes depender de eso).


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

Wrapper: clase que “envuelve” un tipo primitivo para tratarlo como objeto.
En Java:

int → Integer

double → Double

boolean → Boolean, etc.

¿Cómo se hace?

Manual: Integer x = Integer.valueOf(5);

Automático: autoboxing: Integer x = 5;
y unboxing: int y = x;

Ventajas:

Usarlos en colecciones genéricas (List<Integer>).

Permiten null (a veces útil, a veces peligroso).

Tienen métodos útiles (Integer.parseInt, etc.).

¿Todos los lenguajes OO tienen primitivos y wrappers?

No. Algunos lenguajes tratan “todo como objeto” (o lo simulan) y no necesitan wrappers como tal.

En Java sí existen primitivos por eficiencia y por historia del lenguaje.


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

Un tipo enumerado (enum) es un tipo con un conjunto finito de valores posibles (ej: meses, días, colores).

En Java, un enum es una clase especial: cada valor (por ejemplo ENERO) es una instancia de ese enum.

Ventajas de encapsulación en Java:

Puedes tener atributos privados, constructores, métodos dentro del enum.

Evitas valores inválidos (no existe “mes 13” si modelas con enum).

Centralizas lógica: “días del mes”, “estación”, etc. dentro del propio tipo.


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado. Añade además cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

public enum Mes {
    ENERO(1, 31),
    FEBRERO(2, 28),
    MARZO(3, 31),
    ABRIL(4, 30),
    MAYO(5, 31),
    JUNIO(6, 30),
    JULIO(7, 31),
    AGOSTO(8, 31),
    SEPTIEMBRE(9, 30),
    OCTUBRE(10, 31),
    NOVIEMBRE(11, 30),
    DICIEMBRE(12, 31);

    private final int ordinalEnAnio; // 1..12
    private final int dias;

    private Mes(int ordinalEnAnio, int dias) {
        this.ordinalEnAnio = ordinalEnAnio;
        this.dias = dias;
    }

    public int getDias() {
        return dias;
    }

    public int getOrdinalEnAnio() {
        return ordinalEnAnio;
    }

    public boolean esDePrimavera(boolean enHemisferioNorte) {
        // Norte: Mar-Abr-May. Sur: Sep-Oct-Nov
        return enHemisferioNorte
                ? (this == MARZO || this == ABRIL || this == MAYO)
                : (this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE);
    }

    public boolean esDeVerano(boolean enHemisferioNorte) {
        // Norte: Jun-Jul-Ago. Sur: Dic-Ene-Feb
        return enHemisferioNorte
                ? (this == JUNIO || this == JULIO || this == AGOSTO)
                : (this == DICIEMBRE || this == ENERO || this == FEBRERO);
    }

    public boolean esDeOtoño(boolean enHemisferioNorte) {
        // Norte: Sep-Oct-Nov. Sur: Mar-Abr-May
        return enHemisferioNorte
                ? (this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE)
                : (this == MARZO || this == ABRIL || this == MAYO);
    }

    public boolean esDeInvierno(boolean enHemisferioNorte) {
        // Norte: Dic-Ene-Feb. Sur: Jun-Jul-Ago
        return enHemisferioNorte
                ? (this == DICIEMBRE || this == ENERO || this == FEBRERO)
                : (this == JUNIO || this == JULIO || this == AGOSTO);
    }
}



