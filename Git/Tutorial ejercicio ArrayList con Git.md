Vamos a seguir paso a paso este tutorial sobre uno de los ejercicios que hemos resuelto en clase.

Perfecto.  
Vamos a **desarrollar el ejercicio en Java paso a paso** mientras **aprendemos Git por consola**.  
Cada “paso Git” irá acompañado de un **mini-diagrama mental** y el comando exacto que deben teclear los alumnos en la terminal (fuera de IntelliJ, aunque el código lo editen dentro).

## FASE 1 – Crear repositorio y primera versión

### 1.1 Crear proyecto Java en IntelliJ

- New Project → Java → Nombre: `GestorDeudas`.

Si IntelliJ detecta que tienes Git instalado en tu ordenador, te aparecerá el siguiente check, que no debes de pulsar, ya que vamos a trabajar con la consola para aprender mejor.

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

Con esto hemos generado el Entorno de Trabajo (Working Directory) con el contenido actual de nuestro Proyecto.

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

```bash


# Confirmar
git commit -m "Añade esqueleto del proyecto"
```

![[Pasted image 20251208122512.png]]

Ahora, todos esos ar

---

## 🧩 FASE 2 – Añadir menú y opción “A” (30’)

### 2.1 Crear clase `GestorDeudas.java`
```java
import java.util.ArrayList;
import java.util.Scanner;

public class GestorDeudas {
    private static ArrayList<String> clientes = new ArrayList<>();
    private static ArrayList<Double> deudas   = new ArrayList<>();
    private static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        char opc;
        do {
            mostrarMenu();
            opc = sc.nextLine().toUpperCase().charAt(0);
            switch (opc) {
                case 'A': añadirCliente(); break;
                case 'S': System.out.println("¡Hasta luego!"); break;
                default : System.out.println("Opción no válida.");
            }
        } while (opc != 'S');
    }

    private static void mostrarMenu() {
        System.out.println("\n--- MENÚ ---");
        System.out.println("A) Añadir cliente");
        System.out.println("S) Salir");
        System.out.print("Elige: ");
    }

    private static void añadirCliente() {
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
}
```

### 2.2 Segundo commit
```bash
git status          # src/.../GestorDeudas.java modificado
git add src/
git commit -m "Implementa menú y opción A (añadir cliente)"
```

---

## 🧩 FASE 3 – Opciones E, D, C, M (45’)

### 3.1 Implementar cada opción en commits separados

#### Opción D – Listado
```java
private static void listarDeudas() {
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
Añadir al switch: `case 'D': listarDeudas(); break;`

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