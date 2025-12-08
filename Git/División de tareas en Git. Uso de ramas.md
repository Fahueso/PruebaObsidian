Este tutorial está pensado para el trabajo individual alternando roles. Instruye en el rol A de Integrador, y rol B de Programador.

## Generación del esqueleto y diseño de las tareas (Rol Integrador)

Crea un proyecto Java en  IntelliJ, inicializando el repositorio. Recuerda, que de momento vamos a utilizar siempre la consola. 

Edita el archivo `FrutasApp.java` con el siguiente contenido base:

```java
import java.util.ArrayList;
import java.util.Scanner;

public class FrutasApp {

    public static void main(String[] args) {
        ArrayList<String> frutas = new ArrayList<>();
        Scanner sc = new Scanner(System.in);
        int opcion;

        do {
            mostrarMenu();
            opcion = leerEntero(sc);

            switch (opcion) {
                case 1:
                    verFrutas(frutas);
                    break;
                case 2:
                    System.out.println("Función aún no implementada.");
                    break;
                case 3:
                    System.out.println("Función aún no implementada.");
                    break;
                case 4:
                    System.out.println("Función aún no implementada.");
                    break;
                case 5:
                    System.out.println("Función aún no implementada.");
                    break;
                case 0:
                    System.out.println("Adiós.");
                    break;
                default:
                    System.out.println("Opción no válida.");
            }

        } while (opcion != 0);

        sc.close();
    }

    /* ---------- Funciones ---------- */

    public static void mostrarMenu() {
        System.out.println("\n--- MENÚ PRINCIPAL ---");
        System.out.println("1. Ver frutas");
        System.out.println("2. Añadir fruta");
        System.out.println("3. Borrar fruta por nombre");
        System.out.println("4. Buscar fruta");
        System.out.println("5. Ver cantidad total");
        System.out.println("0. Salir");
        System.out.print("Elige una opción: ");
    }

    public static int leerEntero(Scanner sc) {
        int valor = sc.nextInt();
        sc.nextLine(); // limpiar buffer
        return valor;
    }

    public static void verFrutas(ArrayList<String> frutas) {
        System.out.println("\nFrutas actuales:");
        if (frutas.isEmpty()) {
            System.out.println("(vacío)");
        } else {
            for (String f : frutas) {
                System.out.println("- " + f);
            }
        }
    }

    /* ---------- Funciones pendientes ---------- */

    public static void añadirFruta(ArrayList<String> frutas, Scanner sc) {
        // Pendiente
    }

    public static void borrarFruta(ArrayList<String> frutas, Scanner sc) {
        // Pendiente
    }

    public static void buscarFruta(ArrayList<String> frutas, Scanner sc) {
        // Pendiente
    }

    public static void verCantidad(ArrayList<String> frutas) {
        // Pendiente
    }
}
```

Se deja preparado 5 funciones que serán completadas por el equipo de desarrolladores. Para ello se han generado las funciones vacías y se ha dejado el menú pendiente de enlazar el método (sólo hay un print en lugar de la llamada a la función)
Hacemos el primer `commit`:

```bash
git add .
git commit -m "Versión inicial con ArrayList de frutas"
git tag v1.0-esqueleto
```

Ahora hay que repartir la tarea de realizar cada una de las funciones que quedan pendientes de completar. Es posible repartir cada una de estas funciones a un programador diferente. De momento al trabajar sólo con Git el trabajo es individual, sin embargo, potencialmente cada tarea podría ser entregada a un desarrollador diferente.
Cada función a desarrollar se va a separar en el desarrollo empleando una nueva rama de trabajo. Por lo tanto, va a ser posible trabajar en todas ellas en paralelo:

| Tarea | Rol           | Alumno   | Rama             | Función a implementar |
| ----- | ------------- | -------- | ---------------- | --------------------- |
| 1     | Desarrollador | El mismo | `feature-añadir` | `añadirFruta()`       |
| 2     | Desarrollador | ???      | `feature-borrar` | `borrarFruta()`       |
| 3     | Desarrollador | ???      | `feature-buscar` | `buscarFruta()`       |
| 4     | Desarrollador | ???      | `feature-contar` | `verCantidad()`       |
Es importante el orden en el que se realizan las tareas, ya que como mínimo `añadirFruta` es necesario para que el `ArrayList` tenga elementos para probar.

## Desarrollador trabaja en `feature-añadir` (Tarea 1). 

El desarrollador se encuentra inicialmente en la rama `master`. No debe realizar los `commits` en esa rama, ya que el Integrador así lo ha decidido.

La tarea 1 requiere realizar el trabajo en la rama denominada 'feature-añadir'. Esta rama no está creada todavía por lo que vamos a ejecutar el comando para inicializar y posicionarse en dicha rama.

```bash
git checkout -b feature-añadir
```

A partir de ahora los `commits` que realice el desarrollador no alteran la rama `master`, sino la rama `feature-añadir`

El programador completa el método `añadirFruta` asegurando que su funcionamiento es el que corresponde.
```java
public static void añadirFruta(ArrayList<String> frutas, Scanner sc) {
    System.out.print("Nombre de la fruta a añadir: ");
    String nombre = sc.nextLine();
    if (frutas.contains(nombre)) {
        System.out.println("Esa fruta ya existe.");
    } else {
        frutas.add(nombre);
        System.out.println("Fruta añadida.");
    }
}
```

Para ello, adapta el `switch`del `main`:

```java
case 2:
    añadirFruta(frutas, sc);
    break;
```

Una vez probado el buen funcionamiento de la tarea procedemos a realizar el `commit`

```bash
git add FrutasApp.java
git commit -m "Implementada función añadirFruta"
```

El desarrollador da por terminada la tarea 1, cosa que notifica el Integrador.

## Integrador trabaja en `feature-añadir` (Tarea 1). 

Una vez notificado por parte del Desarrollador la finalización de la Tarea 1 el desarrollador realizará los siguientes pasos:

Asegurarse que se encuentra en la rama `master`.

```bash
git checkout main
```

Mezclar el contenido de la rama `feature-añadir`:

```bash
git merge feature-añadir
```

Revisa si hay mensajes de conflicto. Si los hubiera tendríamos que revisar cuál es el problema editando el archivo `FrutasApp.java`. Una vez arreglado el conflicto procedería a llevar los cambios hasta el correspondiente `commit`.

Una vez verificado el funcionamiento del código, la rama ya no se necesita por lo que el Integrador procede a eliminarla:

```bash
git branch -d feature-añadir
```

Además, dado que se trata de un hito *importante* en el desarrollo genera un tag:

```bash
git tag v1.1-añadir-integrado
```

## Integrador planifica el reparto del resto de tareas

Hasta ahora Integrador y Desarrollador eran roles que realizaba una misma persona. Esto no es una manera eficiente de trabajar, ya que en este caso, las diferentes tareas pueden ser realizada por un equipo que trabaja en paralelo.
Para ello es necesario tener un repositorio compartido en `GitHub`. Supongamos que ha generado un repositorio colaborativo con la siguiente URL: 

`https://github.com/tu-usuario/frutas-colaborativo.git`

A continuación decide subir el contenido de todo el trabajo realizado hasta ahora. Esto sólo lo tendrá que hacer una vez:

```bash
# Añadir el remoto (solo la primera vez)
git remote add origin https://github.com/tu-usuario/frutas-colaborativo.git

# Subir el esqueleto y la etiqueta
git push -u origin main
git push origin v1.0-esqueleto
```
