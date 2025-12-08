Este tutorial está pensado para el trabajo en parejas. Instruye en el rol de Programador y el rol de Integrador.

Crea un proyecto Java en  IntelliJ, inicializando el repositorio. Recuerda, que de momento vamos a utilizar siempre la consola. 

Edita el archivo `FrutasApp.java` con el siguiente contenido:

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> frutas = new ArrayList<>();
        frutas.add("Manzana");
        frutas.add("Banana");

        System.out.println("Frutas iniciales:");
        for (String fruta : frutas) {
            System.out.println("- " + fruta);
        }
    }
}
```

Hacemos el primer `commit`:

```bash
git add .
git commit -m "Versión inicial con ArrayList de frutas"
```

