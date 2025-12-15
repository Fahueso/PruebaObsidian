# División de tareas en Git. Uso de ramas

Este tutorial está pensado para trabajar en dos fases:

* Fase 1: trabajo individual alternando roles. Instruye en el rol A de Integrador, y rol B de Programador.
* Fase 2: apertura al mundo colaborativo, permitiendo la entrada de múltiples programadores. En clase, invitaremos al menos a un compañero a desarrollar nuestro proyecto:

## Fase 1
### Generación del esqueleto y diseño de las tareas (Rol Integrador)

Crea un proyecto Java en  IntelliJ, inicializando el repositorio. En esta primera fase vamos a utilizar la consola para las operaciones de `Git`

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

### Integrador trabaja en `feature-añadir` (Tarea 1). 

El desarrollador se encuentra inicialmente en la rama `main`. No debe realizar los `commits` en esa rama, ya que el Integrador así lo ha decidido.

La tarea 1 requiere realizar el trabajo en la rama denominada 'feature-añadir'. Esta rama no está creada todavía por lo que vamos a ejecutar el comando para inicializar y posicionarse en dicha rama.

```bash
git checkout -b feature-añadir
```

A partir de ahora los `commits` que realice el desarrollador no alteran la rama `main`, sino la rama `feature-añadir`

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

El desarrollador da por terminada la tarea 1, cosa que notifica el Integrador. Nota: El desarrollador no crea ningún `tag`.

### Integrador trabaja en `feature-añadir` (Tarea 1). 

Una vez notificado por parte del Desarrollador la finalización de la Tarea 1 el integrador realizará los siguientes pasos:

Asegurarse que se encuentra en la rama `main`.

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


## Fase 2
### Integrador planifica el reparto del resto de tareas para colaboradores

Hasta ahora Integrador y Desarrollador eran roles que realizaba una misma persona. Esto no es una manera eficiente de trabajar, ya que en este caso, las diferentes tareas pueden ser realizada por un equipo que trabaja en paralelo.
Para ello es necesario tener un repositorio compartido en `GitHub`. Supongamos que ha generado un repositorio **público** colaborativo con la siguiente URL: 

`https://github.com/tu-usuario/frutas-colaborativo.git`

A continuación decide subir el contenido de todo el trabajo realizado hasta ahora. Esto sólo lo tendrá que hacer una vez:

```bash
# Añadir el remoto (solo la primera vez)
git remote add origin https://github.com/tu-usuario/frutas-colaborativo.git

# Subir el esqueleto y la etiqueta que se creo de esqueleto
git push -u origin main
git push origin v1.0-esqueleto
```

También vamos a indicar cómo añadir el remoto desde IntelliJ:

![[Pasted image 20251214201502.png]]

Esto permitirá conectarnos a GitHub, con nuestras credenciales y crear un nuevo repositorio.

El siguiente paso que puede hacer el Integrador es añadir al repositorio a los diferentes colaboradores del proyecto, escribiendo el nombre del correo del desarrollador o el nombre de usuario de `GitHub`. Para ello localiza el apartado `Settings > Collaborators> Add People`. Además se asegura que tenga rol de tipo `Write`, que les permite trabajar con sus ramas, sin administrar el repositorio.

Es posible proteger que los colaboradores no modifique la rama `main`, para ello podemos estudiar el apartado `Settings>Rules>Rulesets` donde podemos especificar que los `commits` a esta rama necesitarán aprobación.

Por último el Integrador comunica la URL del repositorio y publica las diferentes tareas a realizar. Organiza el trabajo para que los desarrolladores se repartan todas las tareas de manera eficiente.

### Desarrollador comienza la Tarea X

Supongamos que este desarrollador es nuevo en el proyecto, por lo que necesita traerse a su PC el código fuente del repositorio.

Para ello ejecuta en IntelliJ File>New Project from Version Control

![[Pasted image 20251214193238.png]]


a partir de entonces ya puede generar su rama de trabajo para la tarea actual, partiendo del estado actual de la rama `main:

![[Pasted image 20251214193624.png]]

![[Pasted image 20251214193746.png]]

Esto lo posicionará la rama activa a la requerida. 

![[Pasted image 20251214200510.png]]

La rama `feature-borrar` está posicionada como actual.

Realizará el desarrollo de la función asignada dentro de esta rama, y cuando termine subirá los cambios a su rama local y remota (Commit and Push). Nótese que automáticamente IntelliJ creará una rama del mismo nombre en Github dado que no existía inicialmente.

![[Pasted image 20251214194018.png]]

### Integrador desea procesar la tarea X

El integrador es conocedor de que algún desarrollador ha completado una tarea de desarrollo, y tiene localizada en `GitHub` la rama `feature-xxx`. Ahora realiza una serie de pasos para localizarla en IntelliJ y para mezclar todo ese trabajo a la rama `main`.

Actualmente el Integrador no tiene ninguna rama en su IntelliJ, excepto el `master`:

![[Pasted image 20251214194707.png]]

Pulsa el botón `Fetch` y recupera la rama remota.

![[Pasted image 20251214194739.png]]

Pulsa sobre `feature-listar` del remoto y hace checkout:

![[Pasted image 20251214194915.png]]

Probará el código fuente de la rama, y si este funciona, procederá al mezclado. Para ello, haremos checkout sobre `master` para posicionarnos en él, y una vez que lo tengamos arriba y haremos la mezcla:

![[Pasted image 20251214195058.png]]

Una vez mezclado podemos hacer `push` sobre la rama `master`:

![[Pasted image 20251214195539.png]]

### Integrador hace limpieza de la rama innecesaria

Si las ramas ya no son necesarias el Integrador debería borrarlas

![[Pasted image 20251214195621.png]]

![[Pasted image 20251214195657.png]]


### Integrador ya ha procesado todas las tareas

Cuando todas las tareas ya se hayan integrado, es recomendable establecer un `tag`, ya que se trata de una versión con funcionalidad completa. Mostramos como hacer un `tag` en IntelliJ.

![[Pasted image 20251214195908.png]]


### Anexo: código fuente final

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
                    añadirFruta(frutas, sc);
                    break;
                case 3:
                    borrarFruta(frutas, sc);
                    break;
                case 4:
                    buscarFruta(frutas, sc);
                    break;
                case 5:
                    verCantidad(frutas);
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

    /* ---------- Funciones implementadas ---------- */

    public static void añadirFruta(ArrayList<String> frutas, Scanner sc) {
        System.out.print("Introduce el nombre de la fruta: ");
        String fruta = sc.nextLine().trim();

        if (fruta.isEmpty()) {
            System.out.println("No se puede añadir una fruta vacía.");
            return;
        }

        frutas.add(fruta);
        System.out.println("Fruta añadida correctamente.");
    }

    public static void borrarFruta(ArrayList<String> frutas, Scanner sc) {
        System.out.print("Introduce el nombre de la fruta a borrar: ");
        String fruta = sc.nextLine().trim();

        if (frutas.remove(fruta)) {
            System.out.println("Fruta eliminada.");
        } else {
            System.out.println("No se encontró esa fruta.");
        }
    }

    public static void buscarFruta(ArrayList<String> frutas, Scanner sc) {
        System.out.print("Introduce el nombre de la fruta a buscar: ");
        String fruta = sc.nextLine().trim();

        if (frutas.contains(fruta)) {
            System.out.println("Sí, la fruta está en la lista.");
        } else {
            System.out.println("No, la fruta NO está en la lista.");
        }
    }

    public static void verCantidad(ArrayList<String> frutas) {
        System.out.println("Cantidad total de frutas: " + frutas.size());
    }
}
```