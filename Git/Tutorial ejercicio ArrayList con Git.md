Vamos a **desarrollar el ejercicio en Java paso a paso** mientras **aprendemos Git por consola**.  
Así, vamos a lo largo del ejercicio las ayudas de GIT que nos va proponiendo IntelliJ, aunque más adelante sí las podremos utilizar.

## FASE 1 – Crear repositorio y primera versión

### 1.1 Crear proyecto Java en IntelliJ

- New Project → Java → Nombre: `GestorDeudas`.

Si IntelliJ detecta que tienes Git instalado en tu ordenador, te aparecerá el siguiente check, que no debes de pulsar, ya que como comentamos vamos a trabajar con la consola en este tutorial.

![[Pasted image 20251208121344.png]]

Se ha generado un fichero .gitignore con el siguiente contenido. 

```txt
### IntelliJ IDEA ###  
out/  
!**/src/main/**/out/  
!**/src/test/**/out/  
  
### Eclipse ###  
.apt_generated  
.classpath  
.factorypath  
.project  
.settings  
.springBeans  
.sts4-cache  
bin/  
!**/src/main/**/bin/  
!**/src/test/**/bin/  
  
### NetBeans ###  
/nbproject/private/  
/nbbuild/  
/dist/  
/nbdist/  
/.nb-gradle/  
  
### VS Code ###  
.vscode/  
  
### Mac OS ###  
.DS_Store
```

Esto nos viene muy bien, dado que de esta manera no guardaremos en el Git todos los archivos que IntelliJ genera para la gestión del proyecto, y para sus compilados.

**Como ya sabemos IntelliJ genera un fichero Main.java a efectos demostrativos. Como no lo necesitamos en este proyecto procedemos a borrarlo desde el IDE.**
### 1.2 Inicializar Git (por consola)
```bash
# Moverse a la carpeta raíz del proyecto
cd ruta/al/GestorDeudas

# Iniciar repo
git init
```

Con esto hemos generado el Entorno de Trabajo - Zona 1 (Working Directory) con el contenido actual de nuestro Proyecto.

### 1.3 Primer commit – estructura mínima
```bash
# Ver estado actual
git status
```

![[Pasted image 20251208122217.png]]

```bash 
git add .
git status
```

![[Pasted image 20251208122416.png]]

Ahora todos estos archivos se encuentran en la Zona 2, o Zona de Preparación (Staging Area)

```bash
git commit -m "Añade esqueleto del proyecto"
```

![[Pasted image 20251208122512.png]]

Ahora, todos esos archivos se encuentran en el Repositorio (Zona 3).

---

## FASE 2 – Añadir menú y métodos vacíos

### 2.1 Crear clase `GestorDeudas.java`

Creamos la clase GestorDeudas. De nuevo, si trabajamos con IntelliJ y la carpeta es un proyecto GIT, cada vez que creamos una clase nos saldrá una diálogo de este tipo:

![[Pasted image 20251208123844.png]]

De momento elegiremos la opción Cancel, por lo que más tarde añadiremos el fichero por consola.

Esta primera versión de `GestorDeudas` solo vamos a programar el esqueleto del menú, y una serie de comentarios que indican el trabajo pendiente. Conforme resolvemos cada una de estas tareas, eliminaremos el comentario y actualizaremos nuestra versión.

```java
import java.util.ArrayList;
import java.util.Scanner;

public class GestorDeudas {

    public static void main(String[] args) {
        ArrayList<String> clientes = new ArrayList<>();
        ArrayList<Double> deudas   = new ArrayList<>();
        Scanner sc = new Scanner(System.in);

        char opc;
        do {
            System.out.println("\n--- MENÚ ---");
            System.out.println("A) Añadir cliente");
            System.out.println("E) Eliminar cliente");
            System.out.println("D) Consultar listado");
            System.out.println("C) Consultar saldo cliente");
            System.out.println("M) Modificar deuda");
            System.out.println("S) Salir");
            System.out.print("Elige: ");
            opc = sc.nextLine().toUpperCase().charAt(0);

            switch (opc) {
                case 'A': {
                    /* TODO: añadir cliente */
                    break;
                }
                case 'E': {
                    /* TODO: eliminar cliente */
                    break;
                }
                case 'D': {
                    /* TODO: listar deudas */
                    break;
                }
                case 'C': {
                    /* TODO: consultar cliente */
                    break;
                }
                case 'M': {
                    /* TODO: modificar deuda */
                    break;
                }
                case 'S':
                    System.out.println("¡Hasta luego!");
                    break;
                default:
                    System.out.println("Opción no válida.");
            }
        } while (opc != 'S');

        // Limpieza
        clientes.clear();
        deudas.clear();
    }
}
       
```

### 2.2 Segundo commit


```bash
git status          # Aparecera src/ como archivo sin seguimiento
git add src/
git status         # Aparecerá src/GestorDeudas.java como archivo nuevo
git commit -m "Esqueleto Completo: menú y bloques TODO en main"
```

---

## 🧩 FASE 3 – Programación Opciones

### 3.1 Implementar cada opción en commits separados

#### Opción A – Método añadir cliente
```java
// Dentro de la clase, fuera de main
public static void anyadirCliente(ArrayList<String> clientes,
                                  ArrayList<Double> deudas,
                                  Scanner sc) {
    System.out.print("Nombre: ");
    String nombre = sc.nextLine();
    if (clientes.contains(nombre)) {
        System.out.println("Error: cliente ya existe.");
        return;
    }
    System.out.print("Deuda inicial: ");
    double deuda = Double.parseDouble(sc.nextLine());
    clientes.add(nombre);
    deudas.add(deuda);
    System.out.println("Cliente añadido.");
}
```

En `main`, dentro del `case 'A'`:

```java
case 'A':
    anyadirCliente(clientes, deudas, sc);
    break;
```

Commit:
```bash
git add src/
git commit -m "Implementa opción A: añadir cliente"
```

El procedimiento se va a repetir para cada una de las funciones de este problema


#### Opción D – Listar deudas
```java
public static void listarDeudas(ArrayList<String> clientes,
                                 ArrayList<Double> deudas) {
    if (clientes.isEmpty()) {
        System.out.println("No hay clientes.");
        return;
    }
    double total = 0;
    System.out.println("\n--- ESTADO DE DEUDAS ---");
    System.out.printf("%-15s %10s%n", "CLIENTE", "DEUDA");
    System.out.println("----------------------");
    for (int i = 0; i < clientes.size(); i++) {
        System.out.printf("%-15s %10.2f €%n", clientes.get(i), deudas.get(i));
        total += deudas.get(i);
    }
    System.out.println("----------------------");
    System.out.printf("TOTAL DEUDA: %10.2f €%n", total);
}
```

En `main`, dentro del `case 'D'`:

```java
case 'D':
    listarDeudas(clientes, deudas);
    break;
```

`Add` y `Commit` todo en uno:
```bash
git commit -am "Implementa opción D: listar deudas"
```

En este caso hemos como sabemos que solo vamos a modificar un fichero a lo largo de este programa podemos utilizar `-am` como parámetro del `commit` . De esta manera podemos ir más rápido.


#### Opción C – Consultar saldo de un cliente
```java
private static void consultarCliente(ArrayList<String> clientes,
                                     ArrayList<Double> deudas,
                                     Scanner sc) {
    System.out.print("Nombre: ");
    String nombre = sc.nextLine();
    int idx = clientes.indexOf(nombre);
    if (idx == -1) {
        System.out.println("Cliente no encontrado.");
    } else {
        System.out.printf("%s debe %.2f €%n", nombre, deudas.get(idx));
    }
}
```

En `main`, dentro del `case 'C'`:

```java
case 'C':
    consultarCliente(clientes, deudas, sc);
    break;
```

```bash
git commit -am "Implementa opción C: consultar saldo cliente"
```

#### Opción E – Eliminar cliente
```java
public static void eliminarCliente(ArrayList<String> clientes,
                                    ArrayList<Double> deudas,
                                    Scanner sc) {
    System.out.print("Nombre: ");
    String nombre = sc.nextLine();
    int idx = clientes.indexOf(nombre);
    if (idx == -1) {
        System.out.println("Cliente no encontrado.");
    } else {
        clientes.remove(idx);
        deudas.remove(idx);
        System.out.println("Cliente eliminado.");
    }
}
```

En `main`, dentro del `case 'E'`:

```java
case 'E':
    eliminarCliente(clientes, deudas, sc);
    break;
```

```bash
git commit -am "Implementa opción E: eliminar cliente"
```

#### Opción M – Modificar deuda
```java
public static void modificarDeuda(ArrayList<String> clientes,
                                   ArrayList<Double> deudas,
                                   Scanner sc) {
    System.out.print("Nombre: ");
    String nombre = sc.nextLine();
    int idx = clientes.indexOf(nombre);
    if (idx == -1) {
        System.out.println("Cliente no encontrado.");
        return;
    }
    System.out.print("Nueva deuda: ");
    double nueva = Double.parseDouble(sc.nextLine());
    deudas.set(idx, nueva);
    System.out.println("Deuda actualizada.");
}
```

En `main`, dentro del `case 'M'`:

```java
case 'M':
    modificarDeuda(clientes, deudas, sc);
    break;
```

```bash
git commit -am "Implementa opción M: modificar deuda"
```

#### Historial de commits

```bash
$ git log --oneline
5f6g7h8 Implementa opción M: modificar deuda
4e5f6g7 Implementa opción E: eliminar cliente
3d4e5f6 Implementa opción C: consultar saldo cliente
2c3d4e5 Implementa opción D: listar deudas
1b2c3d4 Implementa opción A: añadir cliente
0a1b2c3 Esqueleto completo: menú y bloques TODO en main
be1c2d4 Añade esqueleto del proyecto"
```
---

## FASE 4 – Deshacer un cambio “accidental”

### 4.1 Simular error
Un alumno borra sin querer el método `listarDeudas()` y guarda en IntelliJ

### 4.2 Ver diferencias
```bash
git diff          # Muestra las línesa borradas en rojo
```

### 4.3 Recuperar versión del repositorio
```bash
git restore src/GestorDeudas.java
```
