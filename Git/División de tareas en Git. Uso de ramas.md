Este tutorial está pensado para el trabajo individual alternando roles. Instruye en el rol A de integrador, y rol B de Programador.

Rol A: Crea un proyecto Java en  IntelliJ, inicializando el repositorio. Recuerda, que de momento vamos a utilizar siempre la consola. 

Edita el archivo `FrutasApp.java` con el siguiente contenido base:

```java
import java.util.ArrayList;
import java.util.Scanner;

public class FrutasApp {
    static ArrayList<String> frutas = new ArrayList<>();
    static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        int opcion;

        do {
            mostrarMenu();
            opcion = leerEntero();

            switch (opcion) {
                case 1:
                    verFrutas();
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
    }

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

    public static int leerEntero() {
        int valor = sc.nextInt();
        sc.nextLine(); // limpiar buffer
        return valor;
    }

    public static void verFrutas() {
        System.out.println("\nFrutas actuales:");
        if (frutas.isEmpty()) {
            System.out.println("(vacío)");
        } else {
            for (String f : frutas) {
                System.out.println("- " + f);
            }
        }
    }

    public static void añadirFruta() {
        // Pendiente
    }

    public static void borrarFruta() {
        // Pendiente
    }

    public static void buscarFruta() {
        // Pendiente
    }

    public static void verCantidad() {
        // Pendiente
    }
}
```

Hacemos el primer `commit`:

```bash
git add .
git commit -m "Versión inicial con ArrayList de frutas"
git tag v1.0-esqueleto
```

Ahora hay que repartir la tarea de realizar cada una de las funciones que quedan pendientes de completar. Es posible repartir cada una de estas funciones a un programador diferente. De momento al trabajar sólo con Git el trabajo es individual, sin embargo, potencialmente cada tarea podría ser entregada a un desarrollador diferente.
Ca:

| Rol           | Alumno   | Rama             | Función a implementar |
| ------------- | -------- | ---------------- | --------------------- |
| Desarrollador | El mismo | `feature-añadir` | `añadirFruta()`       |
| Desarrollador | El mismo | `feature-borrar` | `borrarFruta()`       |
| Desarrollador | El mismo | `feature-buscar` | `buscarFruta()`       |
| Desarrollador | El mismo | `feature-contar` | `verCantidad()`       |


## Desarrollador trabaja en `feature-añadir`

### 2.1. Crear rama

bash

Copy

```bash
git checkout -b feature-añadir
```

### 2.2. Implementar función
