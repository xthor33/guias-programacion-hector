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

Aquí tienes las respuestas a tus preguntas sobre **Programación Orientada a Objetos (POO)**:

---

### **1. Características básicas de la POO**
- **Abstracción**: Representar solo los atributos y comportamientos esenciales de un objeto, ocultando detalles complejos.
- **Encapsulamiento**: Proteger los datos internos de un objeto y permitir el acceso solo a través de métodos específicos.
- **Herencia**: Permitir que una clase (hija) herede atributos y métodos de otra (padre), promoviendo la reutilización de código.
- **Polimorfismo**: Capacidad de un objeto para tomar diferentes formas, como métodos con el mismo nombre pero comportamientos distintos según el contexto.

---

### **2. Cuatro lenguajes populares con POO**
- Java
- Python
- C++
- C#

---

### **3. Paradigmas anteriores a la POO**
- **Programación estructurada**: Organiza el código en funciones o procedimientos, usando estructuras de control como `if`, `for`, `while`, etc.
- **Programación modular**: Divide el programa en módulos independientes (archivos o librerías) que se comunican entre sí, facilitando el mantenimiento y la reutilización.

---

### **4. Tres elementos que definen un objeto**
- **Atributos**: Variables que almacenan datos del objeto (ej: `x`, `y` en un punto).
- **Métodos**: Funciones que definen el comportamiento del objeto (ej: `calculaDistanciaAOrigen`).
- **Identidad**: Cada objeto es único, incluso si sus atributos son idénticos.

---

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

Clase: es un “molde/plantilla” que define qué datos (atributos) y qué comportamiento (métodos) tendrán ciertos objetos. No es algo “vivo” por sí mismo: es la definición.

Objeto: es una “cosa concreta” creada a partir de una clase. Tiene valores reales en sus atributos.

Instancia: es básicamente un objeto de una clase. Decir “instancia de Punto” = “objeto creado siguiendo la clase Punto”.

¿Clase = objeto? No.

Clase = definición (el plano).

Objeto/instancia = el resultado construido (la casa).

¿Todos los lenguajes OO tienen clases? No necesariamente.

Hay lenguajes orientados a objetos basados en prototipos (por ejemplo JavaScript), donde no “necesitas” clases como concepto central (aunque hoy exista class, por dentro sigue siendo prototipos).

Otros lenguajes tienen OO sin el modelo clásico de clases o con variaciones (por ejemplo, Rust no es OO clásico; Go tampoco usa clases como Java).


## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

Depende del lenguaje y del tipo de objeto, pero en muchos lenguajes clásicos:

En Java, los objetos creados con new se almacenan en el heap (montón). Las variables que los “guardan” normalmente son referencias (a menudo en stack si son variables locales).

En C++, un objeto puede estar:

en stack (si lo declaras como variable local normal),

en heap (si usas new),

incluso en memoria estática/global.

En JavaScript, conceptualmente los objetos viven en el heap gestionado por el motor (no controlas stack/heap de forma directa como en C/C++).

¿Es igual en todos los lenguajes? No. Cada lenguaje y runtime decide.

Recolección de basura (Garbage Collection, GC):

Es un mecanismo automático que libera memoria de objetos que ya no se pueden usar (por ejemplo, ya no hay referencias accesibles a ellos).

En lenguajes con GC (Java, C#, JavaScript, Python…), tú normalmente no liberas memoria a mano.

En lenguajes sin GC (C, C++ clásico), tú gestionas memoria manualmente (o con smart pointers y RAII en C++ moderno).


## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

Método: es una función definida dentro de una clase, asociada a los objetos (o a la propia clase si es static). Representa comportamiento.

Sobrecarga de métodos (overloading): tener varios métodos con el mismo nombre en la misma clase, pero con diferente lista de parámetros (número o tipos).
Ejemplo conceptual en Java:

suma(int a, int b)

suma(double a, double b)

suma(int a, int b, int c)


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

public class Punto {
    double x; // visibilidad por defecto (package-private)
    double y;

    double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3;
        p.y = 4;

        double d = p.calculaDistanciaAOrigen();
        System.out.println("Distancia al origen: " + d); // 5.0
    }
}



## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

Punto de entrada: normalmente es el método:

public static void main(String[] args)


La JVM empieza por ahí.

static:

Significa que pertenece a la clase, no a una instancia concreta.

Por eso puedes llamarlo sin crear objeto:

Clase.metodoStatic()

¿Sólo para main? No.

Se usa para:

métodos utilitarios (Math.sqrt, por ejemplo),

constantes,

contadores compartidos por todas las instancias,

fábricas (factory methods), etc.

static + final (muy típico):

final = “no se puede cambiar” (en variables).

static final = constante de clase (una sola copia compartida por todos).
Ejemplo:

public static final double PI = 3.141592653589793;

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

Supón un archivo Punto.java:

Compilar:

javac Punto.java


Esto genera Punto.class.

Ejecutar:

java Punto


(Ojo: se pone el nombre de la clase, sin .class.)

¿Java es compilado?

Sí, pero de forma “mixta”:

Compilas a bytecode (.class), no a código máquina nativo.

Luego la JVM ejecuta ese bytecode (interpretándolo y/o compilándolo “al vuelo” con JIT).

Máquina virtual (JVM):

Es el programa que ejecuta el bytecode.

Permite que el mismo .class funcione en distintos sistemas (Windows, Linux, macOS) si hay JVM.

Bytecode:

Es un “código intermedio” que no es directamente el de tu CPU.

Los archivos .class contienen ese bytecode


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

new:

Crea un nuevo objeto en memoria (en Java, en el heap) y devuelve una referencia a ese objeto.

Constructor:

Es un “método especial” que se ejecuta al crear el objeto.

Se llama igual que la clase y no tiene tipo de retorno.

Ejemplo Empleado:

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


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

new:

Crea un nuevo objeto en memoria (en Java, en el heap) y devuelve una referencia a ese objeto.

Constructor:

Es un “método especial” que se ejecuta al crear el objeto.

Se llama igual que la clase y no tiene tipo de retorno.

Ejemplo Empleado:

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

## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

double distanciaA(Punto otro) {
    double dx = this.x - otro.x;
    double dy = this.y - otro.y;
    return Math.sqrt(dx * dx + dy * dy);
}



## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

En Java, todo se pasa por valor (por copia del valor).

Si pasas un int, el “valor” es el número → copiarlo no afecta fuera.

Si pasas un objeto (Punto), el “valor” que se copia es la referencia (la dirección/referencia al objeto).

Consecuencia:

Dentro del método, puedes modificar el objeto (porque la referencia copiada apunta al mismo objeto) y eso se ve fuera.

Pero si dentro del método haces otro = new Punto(...), sólo cambias la referencia local, no la de fuera.

Ejemplo mental:

void cambia(Punto p) { p.x = 99; } // afecta al objeto real
void cambiaInt(int a) { a = 99; }  // NO afecta fuera


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

toString():

Es un método que devuelve una representación en texto del objeto.

Java lo usa mucho automáticamente (por ejemplo, al hacer System.out.println(obj)).

¿Existe en otros lenguajes?

Sí, la idea es muy común:

Python: __str__

JavaScript: toString()

C#: ToString()

Ejemplo en Punto:

@Override
public String toString() {
    return "Punto(" + x + ", " + y + ")";
}


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


Se parecen en que ambos agrupan datos, pero un struct en C:

No tiene métodos asociados “dentro” del tipo (C no tiene métodos como tal).

No tiene encapsulación real (modificadores como private/public).

No tiene constructores/destructores automáticos.

No tiene herencia/polimorfismo como en OO clásica (en C puedes simularlo, pero no está integrado en el lenguaje).

Para parecerse más a una clase, al struct le faltaría ese “paquete completo” de datos + comportamiento + control de acceso + mecanismos OO.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

En C, lo típico es:

Definir el struct.

Definir una función que reciba un puntero al struct (eso “simula” this).

#include <stdio.h>
#include <math.h>

typedef struct {
    double x;
    double y;
} Punto;

double calculaDistanciaAOrigen(const Punto* thisPunto) {
    return sqrt(thisPunto->x * thisPunto->x + thisPunto->y * thisPunto->y);
}

int main() {
    Punto p;
    p.x = 3;
    p.y = 4;

    printf("Distancia al origen: %f\n", calculaDistanciaAOrigen(&p));
    return 0;
}


¿Qué pasó con this?

En C no existe automáticamente.

Lo sustituyes pasando explícitamente el “objeto” a la función:

En vez de p.calculaDistanciaAOrigen()

haces calculaDistanciaAOrigen(&p)

Ese parámetro thisPunto es, en la práctica, el this manual

