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

### **5. Clase vs. Objeto vs. Instancia**
- **Clase**: Plantilla o molde que define atributos y métodos (ej: `Punto`).
- **Objeto**: Instancia concreta de una clase (ej: `Punto p = new Punto(3, 4)`).
- **Instancia**: Sinónimo de objeto.
- **No todos los lenguajes usan clases**: Algunos, como JavaScript, usan prototipos.

---

### **6. Almacenamiento de objetos y recolección de basura**
- **Memoria**: Los objetos se almacenan en la **memoria heap** (dinámica).
- **Diferencias entre lenguajes**: En C++ se gestiona manualmente; en Java/Python, el **recolector de basura** libera memoria automáticamente cuando un objeto ya no se usa.

---

### **7. Método y sobrecarga**
- **Método**: Función asociada a un objeto (ej: `calculaDistanciaAOrigen`).
- **Sobrecarga**: Definir varios métodos con el mismo nombre pero distintos parámetros (ej: `suma(int a, int b)` y `suma(double a, double b)`).

---

### **8. Ejemplo de clase `Punto` en Java**
```java
class Punto {
    int x, y;

    double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}

// Uso:
Punto p = new Punto();
p.x = 3;
p.y = 4;
System.out.println(p.calculaDistanciaAOrigen()); // Salida: 5.0
```

---

### **9. Punto de entrada en Java y `static`**
- **Punto de entrada**: El método `public static void main(String[] args)`.
- **`static`**: Indica que el método/atributo pertenece a la **clase**, no a una instancia. Se usa para métodos utilitarios o constantes.
- **`final`**: Combínalo con `static` para definir constantes (ej: `static final double PI = 3.14`).

---

### **10. Compilación y ejecución en Java**
- **Compilar**: `javac MiPrograma.java` (genera un archivo `.class` con **byte-code**).
- **Ejecutar**: `java MiPrograma` (la **máquina virtual de Java (JVM)** interpreta el byte-code).
- **Java es compilado e interpretado**: El byte-code es independiente de la plataforma.

---

### **11. `new` y constructores**
- **`new`**: Crea una nueva instancia de una clase en memoria.
- **Constructor**: Método especial que inicializa objetos (mismo nombre que la clase).

**Ejemplo en `Empleado`:**
```java
class Empleado {
    String dni, nombre, apellidos;

    Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }
}
```

---

### **12. Referencia `this`**
- **`this`**: Hace referencia al objeto actual dentro de la clase. No todos los lenguajes lo llaman igual (ej: en Python es `self`).
- **Ejemplo en `Punto`:**
```java
double distanciaA(Punto otro) {
    return Math.sqrt(Math.pow(this.x - otro.x, 2) + Math.pow(this.y - otro.y, 2));
}
```

---

### **13. Método `distanciaA`**
```java
double distanciaA(Punto otro) {
    return Math.sqrt(Math.pow(this.x - otro.x, 2) + Math.pow(this.y - otro.y, 2));
}
```

---

### **14. Paso de parámetros: por referencia vs. por copia**
- **Objetos (ej: `Punto`)**: Se pasan **por referencia**. Si modificas el objeto dentro del método, los cambios persisten fuera.
- **Tipos primitivos (ej: `int`)**: Se pasan **por copia**. Modificarlos dentro del método no afecta al valor original.

---

### **15. Método `toString()`**
- **`toString()`**: Devuelve una representación en cadena del objeto. Existe en muchos lenguajes (ej: `__str__` en Python).
- **Ejemplo en `Punto`:**
```java
@Override
public String toString() {
    return "Punto(" + x + ", " + y + ")";
}
```

---

### **16. `struct` en C vs. clase**
- **Diferencia clave**: Un `struct` en C solo agrupa datos, mientras que una clase en POO también incluye **métodos** y soporta **herencia** y **encapsulamiento**.

---
