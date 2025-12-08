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


# Confirmar
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

Esta primera versión de `GestorDeudas` solo tiene el esqueleto del menú, y una serie de comentarios donde hay que realizar el trabajo pendiente. Conforme resolvemos cada una de estas tareas, eliminaremos el comentario y guardamos versión en GIT.

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
git status          
git add src/
git commit -m "Esqueleto Completo: menú y bloques TODO en main"
```

---

## 🧩 FASE 3 – Programación Opciones

### 3.1 Implementar cada opción en commits separados

#### Opción A – Método añadir cliente
```java
// Dentro de la clase, fuera de main
private static void anyadirCliente(ArrayList<String> clientes,
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
    añadirCliente(clientes, deudas, sc);
    break;
```

Commit:
```bash
git add src/
git commit -m "Añade opción D: listar deudas"
```

#### Opción C – Consultar saldo
```java
private static void consultarCliente() {
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
Commit:
```bash
git commit -am "Añade opción C: consultar saldo de un cliente"
```
> `-am` es atajo de `add` + `commit` cuando ya se ha hecho `add` antes.

#### Opción E – Eliminar
```java
private static void eliminarCliente() {
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
Commit:
```bash
git commit -am "Añade opción E: eliminar cliente"
```

#### Opción M – Modificar deuda
```java
private static void modificarDeuda() {
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
Commit:
```bash
git commit -am "Añade opción M: modificar deuda"
```

---

## 🧪 FASE 4 – Deshacer un cambio “accidental” (20’)

### 4.1 Simular error
Un alumno borra sin querer el método `listarDeudas()` y guarda.

### 4.2 Ver diferencias
```bash
git diff          # Muestra la línea borrada en rojo
```

### 4.3 Recuperar versión del repositorio
```bash
git restore src/GestorDeudas.java
```
> 💡 **Zona 1** (Working Directory) vuelve al estado del último commit.

### 4.4 Alternativa: deshacer último commit (si ya se había commiteado)
```bash
git reset --soft HEAD~1   # Mueve HEAD atrás, pero deja cambios en staging
```

---

## 🏁 FASE 5 – Ver historial y etiquetar (10’)

```bash
# Historial bonito
git log --oneline --graph --decorate

# Etiquetar versión entregable
git tag v1.0 -m "Versión funcional completa"
```

---

## ✅ Resumen de comandos usados
| Tarea | Comando |
|-------|---------|
| Iniciar repo | `git init` |
| Ver estado | `git status` |
| Preparar cambios | `git add <archivo>` o `git add .` |
| Guardar commit | `git commit -m "mensaje"` |
| Ver historial | `git log --oneline` |
| Deshacer cambios en working | `git restore <archivo>` |
| Deshacer último commit | `git reset --soft HEAD~1` |
| Etiquetar | `git tag v1.0 -m "mensaje"` |

---

¿Quieres que prepare un **script de solución** (`solucion.md`) con todo el código final por si alguien se pierde?