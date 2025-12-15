# Gestión de alumnos con HashSet + Conflicto


Vamos a provocar  un conflicto al trabajar dos ramas **la misma zona del código**. Resolver dicho conflicto.
Además en este ejercicio vamos a ver que cada desarrollador tiene la responsabilidad de comentar su trabajo.

---

## **1. Creación de repositorio y código inicial**

El integrador crea un repositorio vacío en `GitHub` llamado `ConflictoHashSet`

Procede a preparar el código fuente y las tareas de los desarrolladores:

```bash
git clone https://github.com/TU-USUARIO/ConflictoHashSet.git
cd ConflictoHashSet
```

Generamos un proyecto en IntelliJ y generamos el archivo: `AlumnosApp.java`. El programa a realizar es un CRUD sobre un conjunto de alumnos

```java
import java.util.HashSet;
import java.util.Scanner;

/**
 * Aplicación de gestión de alumnos usando HashSet.
 * Las funciones están definidas pero no implementadas.
 * Cada desarrollador debe implementar su función y documentarla.
 * @author Integrador1
 */
public class AlumnosApp {

    public static void main(String[] args) {
        HashSet alumnos = new HashSet();
        Scanner sc = new Scanner(System.in);

        int opcion = 0;

        while(opcion != 4) {
            System.out.println("1. Añadir alumno");
            System.out.println("2. Borrar alumno");
            System.out.println("3. Listar alumnos");
            System.out.println("4. Salir");
            System.out.print("Opción: ");
            opcion = Integer.parseInt(sc.nextLine());

            switch(opcion) {
                case 1:
                    funcionAnadir(alumnos, sc);
                    break;
                case 2:
                    funcionBorrar(alumnos, sc);
                    break;
                case 3:
                    funcionListar(alumnos);
                    break;
                case 4:
                    System.out.println("Adiós");
                    break;
                default:
                    System.out.println("Opción incorrecta");
            }
        }
    }

    /**
     * Función a implementar por el desarrollador de la rama feature-anadir.
     * Debe añadir un alumno al HashSet.
     * El desarrollador debe completar el Javadoc y la implementación.
     */
    public static void funcionAnadir(HashSet alumnos, Scanner sc) {
        System.out.println("Función no implementada.");
    }

    /**
     * Función a implementar por el desarrollador de la rama feature-borrar.
     * Debe borrar un alumno del HashSet.
     * El desarrollador debe completar el Javadoc y la implementación.
     */
    public static void funcionBorrar(HashSet alumnos, Scanner sc) {
        System.out.println("Función no implementada.");
    }

    /**
     * Función a implementar por el desarrollador de la rama feature-listar.
     * Debe mostrar todos los alumnos del HashSet.
     * El desarrollador debe completar el Javadoc y la implementación.
     */
    public static void funcionListar(HashSet alumnos) {
        System.out.println("Función no implementada.");
    }
}
```

```bash
git add AlumnosApp.java
git commit -m "Código base con funciones sin implementar"
git push origin main
```

---

## **2. Reparto de tareas en ramas feature‑XXX**

Cada alumno crea su rama desde `main`:

### Alumno A → `feature-anadir`

Implementa la función de añadir alumno.

### Alumno B → `feature-borrar`

Implementa la función de borrar alumno.

### Alumno C → `feature-listar`

Implementa la función de listar alumnos.

---

## **3. Cambios que deben hacer (y dónde estará el conflicto)**

### Rama 1: `feature-anadir`

Recupera el proyecto desde `GitHub`

```bash
git clone https://github.com/TU-USUARIO/fp-hashset-conflicto.git
cd fp-hashset-conflicto
git checkout -b feature-anadir
```

```

Implementa la función **case 1**:

```java
/**
 * Añade un alumno al conjunto si no existe previamente.
 * @param alumnos Conjunto HashSet donde se almacenan los alumnos.
 * @param sc Scanner para leer el nombre del alumno.
 * @author Ana
 */
public static void funcionAnadir(HashSet alumnos, Scanner sc) {
    System.out.print("Nombre del alumno a añadir: ");
    String nombre = sc.nextLine();
    alumnos.add(nombre);
    System.out.println("Alumno añadido.");
}
```


Commit:

```bash
git add AlumnosApp.java
git commit -m "Implementada función añadir alumno"
git push --set-upstream origin feature-añadir
```

---

## Rama 2: `feature-borrar` (esta provocará el conflicto)

```bash
git clone https://github.com/TU-USUARIO/fp-hashset-conflicto.git
cd fp-hashset-conflicto
git checkout -b feature-borrar
```

Modifica **case 1 también**, accidentalmente (forzamos conflicto):

```java
/**
 * Implementación temporal. Pendiente de revisión.
 * @param alumnos Conjunto HashSet.
 * @param sc Scanner para entrada de datos.
 * @author Luis
 */
public static void funcionAnadir(HashSet alumnos, Scanner sc) {
    System.out.println("Añadir alumno (pendiente)");
}

```

Y crea la función del **case 2** correctamente:

```java
/**
 * Elimina un alumno del conjunto si está presente.
 * @param alumnos Conjunto HashSet donde se almacenan los alumnos.
 * @param sc Scanner para leer el nombre del alumno a borrar.
 * @author Luis
 */
public static void funcionBorrar(HashSet alumnos, Scanner sc) {
    System.out.print("Nombre del alumno a borrar: ");
    String nombre = sc.nextLine();
    alumnos.remove(nombre);
    System.out.println("Alumno borrado.");
}

```

Commit:

```bash
git add AlumnosApp.java
git commit -m "Implementada funcionBorrar con Javadoc y cambio temporal en funcionAnadir"
git push --set-upstream origin feature-borrar
```

---

### Rama 3: `feature-listar`

```bash
git clone https://github.com/TU-USUARIO/fp-hashset-conflicto.git
cd fp-hashset-conflicto
git checkout -b feature-listar
```

Modifica **case 3**:

```java
/**
 * Muestra por pantalla todos los alumnos del conjunto.
 * @param alumnos Conjunto HashSet con los alumnos almacenados.
 * @author Marta
 */
public static void funcionListar(HashSet alumnos) {
    System.out.println("Listado de alumnos:");
    java.util.Iterator it = alumnos.iterator();
    while(it.hasNext()) {
        System.out.println(it.next());
    }
}

```

Commit:

```bash
git add AlumnosApp.java
git commit -m "Implementada función listar alumnos"
git push --set-upstream origin feature-listar
```

---

## **4. Integración y conflicto garantizado**

### 1. Mezclar `feature-anadir` en `main` (entra sin conflicto)

```bash
git fetch feature-anadir
git checkout main
git merge origin/feature-anadir
```

### 2. Mezclar `feature-listar` en `main` (entra sin conflicto)

```bash
git fetch feature-anadir
git checkout main
git merge origin/feature-listar
```

### 3. Mezclar `feature-borrar` en `main` (conflicto garantizado)

```bash
git fetch feature-anadir
git checkout main
git merge origin/feature-borrar
```

Git mostrará:

```
CONFLICT (content): Merge conflict in AlumnosApp.java
Automatic merge failed; fix conflicts and then commit the result.
```

---

## **5. Resolución del conflicto**

Dentro de la función que apunta el `case 1` aparecerá:

```java
<<<<<<< HEAD
/**
 * Añade un alumno al conjunto si no existe previamente.
 * @param alumnos Conjunto HashSet donde se almacenan los alumnos.
 * @param sc Scanner para leer el nombre del alumno.
 * @author Ana
 */
public static void funcionAnadir(HashSet alumnos, Scanner sc) {
    System.out.print("Nombre del alumno a añadir: ");
    String nombre = sc.nextLine();
    alumnos.add(nombre);
    System.out.println("Alumno añadido.");
}
=======
/**
 * Implementación temporal. Pendiente de revisión.
 * @param alumnos Conjunto HashSet.
 * @param sc Scanner para entrada de datos.
 * @author Luis
 */
public static void funcionAnadir(HashSet alumnos, Scanner sc) {
    System.out.println("Añadir alumno (pendiente)");
}
>>>>>>> feature-borrar

```

✅ Solución correcta:

```java
/**
 * Añade un alumno al conjunto si no existe previamente.
 * @param alumnos Conjunto HashSet donde se almacenan los alumnos.
 * @param sc Scanner para leer el nombre del alumno.
 * @author Ana
 */
public static void funcionAnadir(HashSet alumnos, Scanner sc) {
    System.out.print("Nombre del alumno a añadir: ");
    String nombre = sc.nextLine();
    alumnos.add(nombre);
    System.out.println("Alumno añadido.");
}

```

Guardar y:

```bash
git add AlumnosApp.java
git commit -m "Resuelto conflicto entre feature-anadir y feature-borrar"
git push origin main
```

Por último borra las ramas de desarrollo:

```bash
git checkout main
git branch -d feature-anadir
git branch -d feature-borrar
git branch -d feature-listar
git push origin --delete feature-anadir
git push origin --delete feature-borrar
git push origin --delete feature-listar
```

---
