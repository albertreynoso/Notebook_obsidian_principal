Aquí tienes tu plan de estudio de 16 clases:

--------------------------------------------------------------------------------

**Plan de Estudio de 16 Clases: Dominando Flutter**

Este plan de estudio se basa en los temas más importantes de Flutter y Dart, estructurado para proporcionarte una comprensión integral y práctica de la tecnología. Cada clase incluirá información relevante, analogías para facilitar la comprensión y un ejemplo práctico que podrás programar.

--------------------------------------------------------------------------------

## Clase 1: Introducción a Flutter y Configuración del Entorno

• **Información Relevante:**

    ◦ **¿Qué es Flutter y por qué usarlo?** Flutter es un kit de desarrollo de software (SDK) de UI de código abierto creado por Google para construir aplicaciones multiplataforma (iOS, Android, web, escritorio e incluso Google Fuchsia) desde una única base de código. Ofrece desarrollo rápido (hot reload, hot restart, null safety), una interfaz de usuario rica en widgets y alto rendimiento al compilar a código nativo.

    ◦ **Requisitos Técnicos:** Necesitarás un sistema operativo de 64 bits (Windows 10+, macOS Yosemite 10.10+, Linux, ChromeOS), Git, PowerShell (en Windows), y se recomienda 8-16 GB de RAM, 50 GB de espacio en disco SSD y un procesador de 2 GHz. Para desarrollar para iOS, necesitarás una Mac.

    ◦ **Instalación del SDK de Flutter:** El proceso implica descargar el SDK de Flutter, configurar las variables de entorno (`PATH`) para la línea de comandos y luego instalar los SDK específicos de la plataforma (Android SDK, Xcode para iOS).

    ◦ **Entornos de Desarrollo Integrados (IDEs):** Se recomiendan Visual Studio Code (VS Code), Android Studio o IntelliJ IDEA, todos con las extensiones de Flutter/Dart instaladas.

    ◦ **flutter doctor****:** Una herramienta esencial para diagnosticar y solucionar problemas en tu entorno de desarrollo, asegurando que todo esté correctamente configurado.

    ◦ **Creación de tu Primera App:** Puedes crear una app desde la línea de comandos (`flutter create <nombre_app>`) o desde tu IDE.

• **Analogía:** Imagina que Flutter es una **caja de herramientas mágica** que te permite construir casas (aplicaciones) de diferentes estilos (iOS, Android, Web, Desktop) con un solo conjunto de planos (código). `flutter doctor` sería tu **inspector de herramientas** que verifica que todas tus herramientas estén en su lugar y funcionen correctamente antes de empezar a construir.

• **Ejemplo Práctico:**

    1. Instala el SDK de Flutter siguiendo las instrucciones oficiales.

    2. Configura tu IDE (VS Code o Android Studio) con las extensiones de Flutter.

    3. Abre una terminal y ejecuta `flutter doctor` para verificar tu configuración. Soluciona cualquier problema que se detecte.

    4. Crea un nuevo proyecto de Flutter desde la línea de comandos: `flutter create hello_world_app`.

    5. Navega a la carpeta del proyecto: `cd hello_world_app`.

    6. Ejecuta la aplicación predeterminada en un emulador o dispositivo conectado: `flutter run`.

--------------------------------------------------------------------------------

## Clase 2: Fundamentos de Dart I: Variables, Tipos de Datos y Control de Flujo

• **Información Relevante:**

    ◦ **Dart:** El lenguaje de programación utilizado por Flutter. Es un lenguaje de programación orientado a objetos, compilado estáticamente.

    ◦ **main()****:** El punto de entrada para cada programa Dart.

    ◦ **Variables:** Símbolos definidos por el usuario que hacen referencia a un valor.

    ◦ **Declaración de Variables (****var****,** **final****,** **const****):**

        ▪ `var`: Puede contener cualquier tipo de dato, y su valor puede cambiar después de la asignación.

        ▪ `final`: El valor se establece solo una vez en tiempo de ejecución y no puede cambiarse. Es inmutable.

        ▪ `const`: El valor debe ser una constante en tiempo de compilación y no puede cambiar. Es inmutable y se conoce antes de que el programa se ejecute.

    ◦ **Tipos de Datos Integrados:** Dart tiene tipos de datos incorporados como números (`int`, `double`), cadenas (`String`), booleanos (`bool`), listas (`List`), mapas (`Map`), runas y símbolos.

        ▪ `int`: Números enteros.

        ▪ `double`: Números decimales.

        ▪ `bool`: Valores verdaderos/falsos.

        ▪ `String`: Secuencia de caracteres. Pueden usarse comillas simples o dobles, y tres comillas para cadenas multilinea.

    ◦ **Interpolación de Cadenas:** Insertar valores de variables directamente en una cadena usando `${variable}` o `$variable`.

    ◦ **Control de Flujo:**

        ▪ `if`/`else`: Permite ejecutar bloques de código condicionalmente.

        ▪ `switch`: Realiza diferentes acciones según el valor de una variable, con las nuevas expresiones `switch` que devuelven valores.

        ▪ Bucles (`for`, `while`, `do-while`, `forEach`): Para iterar sobre colecciones o repetir acciones.

    ◦ **Enumeradores (****enum****):** Definen un grupo de valores constantes relacionados.

• **Analogía:** Piensa en las variables como **cajas de almacenamiento** en tu programa. `var` es una caja que puedes etiquetar con cualquier cosa y cambiar lo que hay dentro. `final` es una caja que solo se etiqueta una vez y su contenido no cambia después de poner algo. `const` es una caja pre-etiquetada y pre-llenada desde la fábrica, su contenido nunca cambia. El control de flujo es como las **señales de tráfico** en tu programa, dirigiendo cuándo y dónde se ejecuta el código.

• **Ejemplo Práctico:**

    1. Crea un nuevo archivo Dart (por ejemplo, `dart_fundamentals_1.dart`) en DartPad ([https://dartpad.dev/](https://www.google.com/url?sa=E&q=https%3A%2F%2Fdartpad.dev%2F)) o en tu IDE.

    2. Implementa variables con `var`, `final` y `const`, mostrando cómo `const` y `final` imponen inmutabilidad.

    3. Declara y usa diferentes tipos de datos (int, double, bool, String).

    4. Utiliza la interpolación de cadenas para combinar texto y variables.

    5. Escribe funciones simples que demuestren `if`/`else` y un bucle `for` o `forEach`.

    6. Define y utiliza un `enum`.

```
void main() {
  // 1. Declaración de variables
  var nombre = "Alice"; // Puede cambiar
  final edad = 30; // Se asigna una vez, no cambia
  const PI = 3.14159; // Constante de compilación, no cambia

  print("Hola, $nombre. Tienes $edad años.");
  print("El valor de PI es $PI.");

  // 2. Tipos de datos
  int contador = 10;
  double precio = 19.99;
  bool estaActivo = true;
  String mensaje = "Aprendiendo Dart";

  print("Contador: $contador, Precio: $precio, Activo: $estaActivo, Mensaje: $mensaje");

  // 3. Control de flujo - if/else
  if (edad >= 18) {
    print("$nombre es mayor de edad.");
  } else {
    print("$nombre es menor de edad.");
  }

  // 4. Control de flujo - bucle for
  List<String> frutas = ["Manzana", "Banana", "Cereza"];
  print("\nMis frutas favoritas:");
  for (var fruta in frutas) {
    print("- $fruta");
  }

  // 5. Enumerador
  var diaActual = DiaSemana.LUNES;
  print("\nHoy es ${diaActual.toString().split('.').last}");
}

enum DiaSemana { LUNES, MARTES, MIERCOLES, JUEVES, VIERNES, SABADO, DOMINGO }
```

--------------------------------------------------------------------------------

## Clase 3: Fundamentos de Dart II: Funciones, Clases y Programación Orientada a Objetos

• **Información Relevante:**

    ◦ **Funciones:** Bloques de código reutilizables que realizan una tarea específica. Pueden tener parámetros posicionales, nombrados u opcionales, y pueden retornar valores.

    ◦ **Funciones como Variables (Closures):** En Dart, las funciones son objetos de primera clase, lo que significa que pueden ser asignadas a variables, pasadas como argumentos y devueltas por otras funciones. Un _closure_ es una función que tiene acceso al scope de la función que la define, incluso después de que la función externa haya terminado de ejecutarse.

    ◦ **Programación Orientada a Objetos (POO):** Dart es un lenguaje POO.

    ◦ **Clases:** Son plantillas para crear objetos, encapsulando propiedades (datos) y comportamientos (métodos).

    ◦ **Constructores:** Métodos especiales para inicializar objetos de una clase. Dart ofrece un _shorthand_ para la creación de constructores que inicializan propiedades.

    ◦ **Herencia (****extends****):** Una clase puede heredar propiedades y métodos de otra (superclase), promoviendo la reutilización de código. Dart no soporta herencia múltiple.

    ◦ **Interfaces (****implements****):** En Dart, todas las clases son interfaces implícitas. Una clase puede implementar una o más interfaces, lo que significa que se compromete a proporcionar una implementación para todos los métodos y propiedades definidos en las interfaces.

    ◦ **Mixins (****with****):** Permiten reutilizar código de una clase en múltiples jerarquías de clases sin usar herencia. Son una forma de agregar funcionalidad a una clase.

• **Analogía:** Las funciones son como **recetas de cocina** que puedes seguir una y otra vez para preparar un plato específico. Las clases son como los **planos arquitectónicos** de un edificio; definen cómo será el edificio (objeto) y qué funciones tendrá. La herencia es como **heredar el negocio familiar**: obtienes todas las habilidades y la estructura del negocio de tus padres, pero puedes añadir las tuyas propias. Una interfaz es como un **contrato legal**: establece lo que debes hacer, pero no cómo hacerlo. Un mixin es como un **juego de herramientas extra** que puedes añadir a cualquier negocio para mejorar su funcionamiento, sin que cambie su naturaleza fundamental.

• **Ejemplo Práctico:**

    1. Crea un archivo Dart (`dart_fundamentals_2.dart`).

    2. Define funciones con diferentes tipos de parámetros (posicionales y nombrados) y una función que devuelva otra función (closure).

    3. Crea una clase base `Animal` con un constructor y un método.

    4. Crea una subclase `Perro` que `extends` de `Animal`, demostrando herencia.

    5. Define una clase `Volador` (implícitamente una interfaz) y haz que una clase `Pajaro` la `implements`.

    6. Crea un `mixin` `Nadador` y haz que una clase `Pato` lo `with`.

```
// Funciones
void saludar(String nombre, {String mensaje = "Hola"}) {
  print("$mensaje, $nombre!"); // Parámetro nombrado opcional
}

Function crearMultiplicador(int factor) {
  return (int numero) => numero * factor; // Closure
}

// Clases y POO
class Animal {
  String nombre;
  Animal(this.nombre); // Constructor shorthand
  void hacerSonido() {
    print("$nombre hace un sonido.");
  }
}

class Perro extends Animal {
  String raza;
  Perro(String nombre, this.raza) : super(nombre); // Herencia y super
  @override
  void hacerSonido() {
    print("$nombre (${raza}) ladra.");
  }
}

// Interfaz implícita (todas las clases son interfaces)
class Volador {
  void volar() {
    print("Volando alto!");
  }
}

class Pajaro implements Volador { // Implementa la interfaz
  String nombre;
  Pajaro(this.nombre);

  @override
  void volar() {
    print("$nombre está volando con sus alas.");
  }
}

// Mixin
mixin Nadador {
  void nadar() {
    print("Nadando en el agua.");
  }
}

class Pato extends Animal with Nadador { // Usa un mixin
  Pato(String nombre) : super(nombre);

  @override
  void hacerSonido() {
    print("$nombre hace cuac.");
  }
}

void main() {
  saludar("Carlos");
  saludar("Ana", mensaje: "¡Saludos");

  var duplicar = crearMultiplicador(2);
  print("Duplicar 5: ${duplicar(5)}");

  var miPerro = Perro("Fido", "Golden Retriever");
  miPerro.hacerSonido();

  var miPajaro = Pajaro("Gorrión");
  miPajaro.volar();

  var miPato = Pato("Donald");
  miPato.hacerSonido();
  miPato.nadar();
}
```

--------------------------------------------------------------------------------

## Clase 4: Fundamentos de Dart III: Colecciones, Null Safety y Operadores Avanzados

• **Información Relevante:**

    ◦ **Colecciones:** Estructuras para agrupar y manipular datos.

        ▪ **List****:** Colección ordenada de objetos. Similar a un array.

        ▪ **Map****:** Colección de pares clave-valor. Similar a un diccionario o hashmap.

        ▪ **Set****:** Colección de elementos únicos y desordenados.

    ◦ **Operadores de Colección:** `...` (spread operator) para expandir elementos de una colección en otra. `if` y `for` en colecciones.

    ◦ **Funciones de Orden Superior (Higher-Order Functions):** Funciones que toman otras funciones como argumentos o devuelven una función. Son clave para manipular datos de manera reutilizable y modular, un pilar de la programación funcional. Ejemplos: `map`, `where` (filter), `forEach`, `sort`, `reduce`.

    ◦ **Operador Cascada (****..****):** Permite realizar múltiples operaciones en el mismo objeto sin tener que repetir el nombre del objeto. Mejora la legibilidad y concisión del código.

    ◦ **Null Safety (Nulabilidad Segura):** Introducida en Dart para prevenir errores de referencia nula en tiempo de ejecución.

        ▪ `?`: Indica que una variable puede ser nula (nullable type).

        ▪ `!`: Operador de aserción (nunca nulo), indica que estás seguro de que un valor no es nulo, incluso si el compilador piensa que sí.

        ▪ `late`: Declara una variable no nula que se inicializará más tarde, antes de ser usada.

        ▪ `required`: Indica que un parámetro nombrado es obligatorio.

• **Analogía:** Las colecciones son como **diferentes tipos de organizadores** para tus cosas. Una `List` es como una lista de compras, el orden importa y puedes tener duplicados. Un `Map` es como un diccionario, cada palabra (clave) tiene una definición única (valor). Un `Set` es como tu grupo de amigos, a cada uno lo conoces por su nombre único y no importa el orden. El operador cascada es como un **cepillo multiusos** que te permite aplicar varias acciones a la misma cosa de forma seguida y eficiente. Null safety es como poner **cinturones de seguridad** a tus variables; evita accidentes inesperados (errores de tiempo de ejecución) cuando un valor es nulo.

• **Ejemplo Práctico:**

    1. Crea un archivo Dart (`dart_fundamentals_3.dart`).

    2. Define una `List`, un `Map` y un `Set`, y realiza operaciones básicas (añadir, remover, acceder, iterar).

    3. Usa el operador spread (`...`) para combinar listas o añadir elementos condicionalmente (`if` en colecciones).

    4. Implementa funciones de orden superior como `map`, `where` y `forEach` en una lista de datos.

    5. Demuestra el operador cascada en un objeto.

    6. Declara variables con y sin null safety, y usa `?`, `!` y `late` para manejar valores nulos.

```
void main() {
  // 1. Listas, Mapas y Sets
  List<int> numeros = [44-46, 117, 118];
  print("Lista original: $numeros");
  numeros.add(6);
  print("Lista después de añadir: $numeros");

  Map<String, String> capitales = {
    "España": "Madrid",
    "Francia": "París"
  };
  print("Map original: $capitales");
  capitales["Alemania"] = "Berlín";
  print("Map después de añadir: $capitales");

  Set<String> colores = {"Rojo", "Verde", "Azul"};
  print("Set original: $colores");
  colores.add("Rojo"); // No se añade porque ya existe
  print("Set después de añadir duplicado: $colores");

  // 2. Operadores de colección
  List<int> masNumeros = [51, 75, 84];
  List<int> todosLosNumeros = [...numeros, ...masNumeros]; // Spread operator
  print("Todos los números con spread: $todosLosNumeros");

  bool incluirCero = true;
  List<int> numerosDinamicos = [
    10,
    11,
    if (incluirCero) 0, // if en colecciones
    12
  ];
  print("Números dinámicos: $numerosDinamicos");

  // 3. Funciones de orden superior
  var cuadrados = numeros.map((n) => n * n).toList(); // map
  print("Cuadrados de los números: $cuadrados");

  var pares = numeros.where((n) => n % 2 == 0).toList(); // where
  print("Números pares: $pares");

  print("Iterando con forEach:");
  numeros.forEach((n) => print(n));

  // 4. Operador cascada
  StringBuffer sb = StringBuffer();
  sb..write("Hola ")
    ..write("Mundo ")
    ..write("Dart");
  print("\nBuffer con cascada: ${sb.toString()}");

  // 5. Null Safety
  String? textoNullable; // Puede ser nulo
  print("Texto nullable: $textoNullable");

  textoNullable = "¡No es nulo!";
  print("Texto nullable (después de asignar): $textoNullable");

  String textoNoNulo = textoNullable!; // ¡Asumo que no es nulo!
  print("Texto no nulo: $textoNoNulo");

  late String inicializadoMasTarde;
  inicializadoMasTarde = "Valor tardío";
  print("Inicializado más tarde: $inicializadoMasTarde");
}
```

--------------------------------------------------------------------------------

## Clase 5: Introducción a Widgets: Los Bloques de Construcción de UI

• **Información Relevante:**

    ◦ **Widgets:** En Flutter, **todo es un widget**. Desde un botón, una imagen o una tabla, hasta la aplicación misma, todo se construye con widgets. Son las unidades fundamentales de la interfaz de usuario.

    ◦ **Composición:** El poder de Flutter no reside en widgets individuales, sino en cómo se componen entre sí para crear interfaces complejas. Los widgets suelen realizar una tarea pequeña y específica, y se anidan para construir diseños elaborados.

    ◦ **Árbol de Widgets (Widget Tree):** Todos los widgets en una pantalla, cuando se combinan, forman una estructura de árbol jerárquica. Flutter utiliza este árbol para dibujar la UI de manera eficiente.

    ◦ **Declarative UI:** En Flutter, la UI se construye de forma declarativa, es decir, describes cómo debería verse tu UI para un estado dado, y Flutter se encarga de renderizarla. No hay lenguajes de marcado como XML o HTML; la UI se define directamente en Dart.

    ◦ **StatelessWidget** **vs** **StatefulWidget****:**

        ▪ **StatelessWidget****:** Widgets que no tienen estado interno que cambie durante su vida útil. Son inmutables. Son ideales para partes de la UI que no necesitan cambiar dinámicamente, como un `Text` o un `Icon`.

        ▪ **StatefulWidget****:** Widgets que sí tienen un estado mutable que puede cambiar con el tiempo. Flutter los reconstruye cuando su estado cambia para reflejar los nuevos datos. Se utilizan para elementos interactivos como casillas de verificación o campos de texto.

    ◦ **Widgets Básicos de UI:**

        ▪ **Text****:** Para mostrar texto en la pantalla, con opciones de estilo (`TextStyle`).

        ▪ **Icon****:** Para mostrar iconos.

        ▪ **Image****:** Para mostrar imágenes (desde assets, red, memoria).

        ▪ **Container****:** Un widget multipropósito que permite añadir padding, márgenes, colores de fondo, bordes y otras decoraciones.

        ▪ **Center****:** Centra su widget hijo tanto horizontal como verticalmente.

        ▪ **SizedBox****:** Crea un cuadro de un tamaño fijo. Útil para espaciar widgets o restringir tamaños.

        ▪ **Scaffold****:** Proporciona una estructura básica para una pantalla de Material Design (con AppBar, body, FloatingActionButton, Drawer, etc.).

• **Analogía:** Piensa en los widgets como **piezas de LEGO**. Un `Text` es una pieza de LEGO con texto, un `Image` es una pieza con una imagen. Puedes combinar estas piezas pequeñas para construir estructuras más grandes (composición). Un `StatelessWidget` es una pieza de LEGO que, una vez colocada, no cambia. Un `StatefulWidget` es una pieza de LEGO que puede cambiar de color o forma con el tiempo (por ejemplo, un contador). `Scaffold` es como el **esqueleto de un robot**, proporcionando la estructura básica (cabeza, cuerpo, brazos) donde puedes colocar todas las demás piezas de LEGO.

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `mis_widgets_basicos`.

    2. Modifica el archivo `main.dart`.

    3. Crea un `StatelessWidget` simple que use un `Scaffold`.

    4. Dentro del `Scaffold` (en la propiedad `body`):

        ▪ Usa un `Center` widget.

        ▪ Como hijo del `Center`, utiliza un `Column` (que veremos en la siguiente clase) para apilar varios widgets.

        ▪ Añade un `Text` con un estilo personalizado.

        ▪ Añade un `Icon`.

        ▪ Añade un `Image.network` que muestre una imagen desde una URL.

        ▪ Añade un `Container` con color de fondo, padding y un borde.

        ▪ Usa un `SizedBox` para crear un espacio entre dos elementos.

        ▪ Añade un `FloatingActionButton` al `Scaffold`.

```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Mis Widgets Básicos',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const BasicWidgetsScreen(),
    );
  }
}

class BasicWidgetsScreen extends StatelessWidget {
  const BasicWidgetsScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Explorando Widgets Básicos'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            // 1. Text Widget con estilo
            const Text(
              '¡Hola Flutter!',
              style: TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
                color: Colors.deepPurple,
              ),
            ),
            // 2. SizedBox para espacio
            const SizedBox(height: 20),
            // 3. Icon Widget
            const Icon(
              Icons.star,
              color: Colors.amber,
              size: 50,
            ),
            // 4. SizedBox para espacio
            const SizedBox(height: 20),
            // 5. Image.network
            Image.network(
              'https://via.placeholder.com/150', // Una URL de imagen de ejemplo
              width: 150,
              height: 150,
              fit: BoxFit.cover,
            ),
            // 6. SizedBox para espacio
            const SizedBox(height: 20),
            // 7. Container con decoración
            Container(
              padding: const EdgeInsets.all(20),
              margin: const EdgeInsets.all(10),
              decoration: BoxDecoration(
                color: Colors.lightGreen,
                borderRadius: BorderRadius.circular(15),
                border: Border.all(
                  color: Colors.green.shade800,
                  width: 3,
                ),
                boxShadow: const [
                  BoxShadow(
                    color: Colors.black26,
                    blurRadius: 10,
                    offset: Offset(5, 5),
                  ),
                ],
              ),
              child: const Text(
                '¡Un Container con estilo!',
                style: TextStyle(color: Colors.white, fontSize: 18),
              ),
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Acción del botón flotante
          ScaffoldMessenger.of(context).showSnackBar(
            const SnackBar(content: Text('Botón flotante presionado!')),
          );
        },
        child: const Icon(Icons.add),
      ),
    );
  }
}
```

--------------------------------------------------------------------------------

## Clase 6: Dominando el Layout I: Rows y Columns para Disposición Secuencial

• **Información Relevante:**

    ◦ **Estrategia de Layout de Flutter:** Flutter tiene un motor de layout flexible y responsivo que aprende de soluciones de layout previas en web, escritorio e iOS/Android.

    ◦ **Layouts Secuenciales:** Para organizar widgets uno tras otro, los `Row` y `Column` son fundamentales.

    ◦ **Column****:** Dispone sus widgets hijos en una matriz vertical. Es el widget ideal para apilar elementos uno encima del otro.

    ◦ **Row****:** Dispone sus widgets hijos en una matriz horizontal. Es perfecto para colocar elementos uno al lado del otro.

    ◦ **mainAxisAlignment****:** Controla cómo los hijos se alinean a lo largo del eje principal (`Column`: vertical; `Row`: horizontal). Valores comunes: `start`, `end`, `center`, `spaceBetween`, `spaceAround`, `spaceEvenly`.

    ◦ **crossAxisAlignment****:** Controla cómo los hijos se alinean a lo largo del eje transversal (`Column`: horizontal; `Row`: vertical). Valores comunes: `start`, `end`, `center`, `stretch`, `baseline`.

    ◦ **MainAxisSize****:** Define cuánto espacio debe ocupar el `Row` o `Column` en el eje principal. `max` (por defecto) ocupa todo el espacio disponible; `min` ocupa solo el espacio necesario para sus hijos.

• **Analogía:** Piensa en `Row` y `Column` como los **carriles de una carretera**. Un `Column` es una carretera vertical donde los coches (widgets) se alinean uno detrás de otro. Un `Row` es una carretera horizontal. `mainAxisAlignment` es cómo los coches se distribuyen a lo largo de su carril (¿están al principio, al final, espaciados uniformemente?). `crossAxisAlignment` es cómo se alinean los coches dentro del ancho del carril (¿están pegados a la izquierda, a la derecha o centrados?).

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `layout_secuencial`.

    2. Diseña una pantalla de perfil simple utilizando `Column` y `Row` anidados. Por ejemplo, una imagen de perfil, un nombre y una serie de botones o información de contacto en filas.

    3. Experimenta con diferentes valores para `mainAxisAlignment` y `crossAxisAlignment` en `Row` y `Column` para ver cómo afectan la disposición de los hijos.

    4. Usa `MainAxisSize.min` en una `Column` para que ocupe solo el espacio necesario.

```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Layout Secuencial',
      theme: ThemeData(
        primarySwatch: Colors.teal,
      ),
      home: const ProfileScreen(),
    );
  }
}

class ProfileScreen extends StatelessWidget {
  const ProfileScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Mi Perfil'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start, // Alinea el contenido al inicio de la columna
          crossAxisAlignment: CrossAxisAlignment.center, // Centra los hijos horizontalmente
          children: <Widget>[
            // Espacio superior para una mejor estética
            const SizedBox(height: 30),

            // Imagen de perfil
            const CircleAvatar(
              radius: 60,
              backgroundImage: NetworkImage('https://via.placeholder.com/150/0000FF/FFFFFF?text=User'), // Imagen de usuario de ejemplo
            ),

            // Espacio entre imagen y nombre
            const SizedBox(height: 20),

            // Nombre del usuario
            const Text(
              'Jane Doe',
              style: TextStyle(
                fontSize: 28,
                fontWeight: FontWeight.bold,
              ),
            ),

            // Pequeña descripción
            const Text(
              'Desarrolladora Flutter Entusiasta',
              style: TextStyle(
                fontSize: 18,
                color: Colors.grey,
              ),
            ),

            // Espacio antes de los botones/información
            const SizedBox(height: 40),

            // Fila de botones de acción
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly, // Distribuye el espacio uniformemente entre los botones
              children: <Widget>[
                ElevatedButton.icon(
                  onPressed: () {
                    ScaffoldMessenger.of(context).showSnackBar(
                        const SnackBar(content: Text('Mensaje enviado')));
                  },
                  icon: const Icon(Icons.message),
                  label: const Text('Mensaje'),
                ),
                ElevatedButton.icon(
                  onPressed: () {
                    ScaffoldMessenger.of(context).showSnackBar(
                        const SnackBar(content: Text('Llamada realizada')));
                  },
                  icon: const Icon(Icons.call),
                  label: const Text('Llamar'),
                ),
              ],
            ),

            // Espacio antes de la información de contacto
            const SizedBox(height: 30),

            // Información de contacto usando Rows anidadas en una Column
            Column(
              crossAxisAlignment: CrossAxisAlignment.start, // Alinea el texto a la izquierda
              children: <Widget>[
                Padding(
                  padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 5),
                  child: Row(
                    children: const <Widget>[
                      Icon(Icons.email, color: Colors.teal),
                      SizedBox(width: 10),
                      Text('jane.doe@example.com', style: TextStyle(fontSize: 16)),
                    ],
                  ),
                ),
                Padding(
                  padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 5),
                  child: Row(
                    children: const <Widget>[
                      Icon(Icons.phone, color: Colors.teal),
                      SizedBox(width: 10),
                      Text('+1 (555) 123-4567', style: TextStyle(fontSize: 16)),
                    ],
                  ),
                ),
                Padding(
                  padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 5),
                  child: Row(
                    children: const <Widget>[
                      Icon(Icons.location_on, color: Colors.teal),
                      SizedBox(width: 10),
                      Text('Ciudad Flutter, Mundo Digital', style: TextStyle(fontSize: 16)),
                    ],
                  ),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

--------------------------------------------------------------------------------

## Clase 7: Dominando el Layout II: Widgets Flexibles y Adaptables

• **Información Relevante:**

    ◦ **Espaciado Proporcional (****Flexible** **y** **Expanded****):** Cuando trabajas con `Row` y `Column`, necesitas controlar cómo los hijos utilizan el espacio disponible.

        ▪ **Flexible****:** Permite que su hijo se ajuste a las limitaciones del padre, pero no requiere que el hijo llene todo el espacio disponible. Puede tener un parámetro `flex` para indicar la proporción de espacio que ocupará, y un `fit` (`tight` o `loose`) para controlar si el hijo debe llenar el espacio (`tight`) o puede ser más pequeño (`loose`).

        ▪ **Expanded****:** Es un `Flexible` con `fit: FlexFit.tight` por defecto. Forzará a su hijo a llenar todo el espacio disponible a lo largo del eje principal de un `Row` o `Column`.

    ◦ **Spacer****:** Un widget que crea espacio flexible a lo largo del eje principal de un `Row` o `Column`. Es como un `Expanded` sin hijo.

    ◦ **FittedBox****:** Escala y posiciona a su hijo dentro de sí mismo. Útil para asegurar que el contenido encaje en el espacio disponible, por ejemplo, un texto largo dentro de un contenedor pequeño.

    ◦ **ConstrainedBox****:** Impone restricciones adicionales a su hijo. Por ejemplo, puedes establecer una `minHeight` o `minWidth`.

    ◦ **LayoutBuilder****:** Un widget que te permite construir diferentes interfaces de usuario basándose en las restricciones de tamaño de su padre (por ejemplo, el tamaño de la pantalla). Esto es crucial para crear interfaces responsivas que se adaptan a diferentes dispositivos o rotaciones.

    ◦ **MediaQuery****:** Proporciona información sobre el tamaño y la orientación de la pantalla, la densidad de píxeles, etc. Útil para adaptar layouts de forma más global.

    ◦ **Wrap****:** Coloca los widgets hijos uno al lado del otro y los "envuelve" a la siguiente línea si no hay suficiente espacio. Útil para etiquetas o chips que pueden necesitar disponerse en varias líneas.

• **Analogía:** Imagina que `Flexible` y `Expanded` son como **asientos de avión reclinables**. `Flexible` te permite reclinar el asiento un poco (ajustar el tamaño) pero no necesariamente hasta el final. `Expanded` es como reclinarlo al máximo, ocupando todo el espacio disponible y empujando a los de atrás. `FittedBox` es como un **zoom inteligente**: si la imagen es demasiado grande para el marco, la reduce para que quepa perfectamente. `LayoutBuilder` es como un **arquitecto adaptativo**: diseña la casa de manera diferente si el terreno es grande o pequeño, o si es para una familia numerosa o una pareja.

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `layouts_adaptables`.

    2. Implementa un `Row` con dos o tres widgets `Expanded` para dividir el espacio horizontal de manera proporcional. Juega con el parámetro `flex`.

    3. Dentro de uno de los `Expanded`, usa un `FittedBox` con un `Text` largo para demostrar cómo se ajusta el texto.

    4. Crea un `ConstrainedBox` con un `Container` como hijo para imponer límites de tamaño.

    5. Utiliza `LayoutBuilder` para mostrar un diseño diferente (por ejemplo, una `Column` para pantallas estrechas y una `Row` para pantallas anchas) basándose en el ancho disponible.

    6. Usa un `Wrap` widget para una lista de "tags" que se ajusten automáticamente a la siguiente línea.

```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Layouts Adaptables',
      theme: ThemeData(
        primarySwatch: Colors.indigo,
      ),
      home: const AdaptiveLayoutScreen(),
    );
  }
}

class AdaptiveLayoutScreen extends StatelessWidget {
  const AdaptiveLayoutScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Widgets Flexibles y Adaptables'),
      ),
      body: SingleChildScrollView( // Permite el scroll si el contenido se desborda
        child: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: <Widget>[
              const Text(
                '1. Expanded y Flexible para distribución de espacio:',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
              ),
              const SizedBox(height: 10),
              // Ejemplo de Expanded
              Row(
                children: <Widget>[
                  Expanded(
                    flex: 2, // Ocupa 2/3 del espacio disponible
                    child: Container(
                      color: Colors.red,
                      height: 50,
                      child: const Center(child: Text('Expanded (Flex 2)', style: TextStyle(color: Colors.white))),
                    ),
                  ),
                  Expanded(
                    flex: 1, // Ocupa 1/3 del espacio disponible
                    child: Container(
                      color: Colors.blue,
                      height: 50,
                      child: const Center(child: Text('Expanded (Flex 1)', style: TextStyle(color: Colors.white))),
                    ),
                  ),
                ],
              ),
              const SizedBox(height: 20),
              // Ejemplo de Flexible
              Row(
                children: <Widget>[
                  Flexible(
                    flex: 1,
                    fit: FlexFit.loose, // El hijo puede ser más pequeño que el espacio
                    child: Container(
                      color: Colors.orange,
                      height: 50,
                      child: const Center(child: Text('Flexible Loose (Flex 1)', style: TextStyle(color: Colors.white))),
                    ),
                  ),
                  Flexible(
                    flex: 2,
                    fit: FlexFit.tight, // El hijo debe llenar el espacio asignado
                    child: Container(
                      color: Colors.purple,
                      height: 50,
                      child: const Center(child: Text('Flexible Tight (Flex 2)', style: TextStyle(color: Colors.white))),
                    ),
                  ),
                ],
              ),

              const SizedBox(height: 30),
              const Text(
                '2. FittedBox para ajuste de contenido:',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
              ),
              const SizedBox(height: 10),
              Container(
                width: 150,
                height: 50,
                color: Colors.grey[221],
                child: FittedBox(
                  fit: BoxFit.scaleDown, // Escala el texto para que quepa
                  child: Text(
                    'Un texto muy largo que debe ajustarse',
                    style: TextStyle(fontSize: 100), // Tamaño de fuente grande para demostrar el ajuste
                  ),
                ),
              ),

              const SizedBox(height: 30),
              const Text(
                '3. ConstrainedBox para imponer límites:',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
              ),
              const SizedBox(height: 10),
              ConstrainedBox(
                constraints: const BoxConstraints(
                  minHeight: 80, // Altura mínima
                  maxHeight: 120, // Altura máxima
                  minWidth: 150,
                  maxWidth: 250,
                ),
                child: Container(
                  color: Colors.cyan,
                  child: const Center(child: Text('Contenido con restricciones', style: TextStyle(color: Colors.white))),
                ),
              ),

              const SizedBox(height: 30),
              const Text(
                '4. LayoutBuilder para diseño responsivo:',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
              ),
              const SizedBox(height: 10),
              // LayoutBuilder que cambia la disposición según el ancho
              LayoutBuilder(
                builder: (BuildContext context, BoxConstraints constraints) {
                  if (constraints.maxWidth < 600) {
                    // Pantalla estrecha (móvil)
                    return Column(
                      children: _buildResponsiveWidgets('Columna'),
                    );
                  } else {
                    // Pantalla ancha (tablet/desktop)
                    return Row(
                      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                      children: _buildResponsiveWidgets('Fila'),
                    );
                  }
                },
              ),

              const SizedBox(height: 30),
              const Text(
                '5. Wrap para contenido que se ajusta a la siguiente línea:',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
              ),
              const SizedBox(height: 10),
              Wrap(
                spacing: 8.0, // Espacio horizontal entre los chips
                runSpacing: 8.0, // Espacio vertical entre las líneas de chips
                children: List<Widget>.generate(
                  10,
                  (index) => Chip(
                    avatar: CircleAvatar(backgroundColor: Colors.blue.shade900, child: Text('${index + 1}')),
                    label: Text('Etiqueta ${index + 1}'),
                  ),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }

  List<Widget> _buildResponsiveWidgets(String orientation) {
    return [
      Container(
        color: Colors.green,
        width: orientation == 'Columna' ? double.infinity : 100,
        height: 50,
        margin: const EdgeInsets.all(5),
        child: Center(child: Text('$orientation Widget 1', style: const TextStyle(color: Colors.white))),
      ),
      Container(
        color: Colors.yellow.shade800,
        width: orientation == 'Columna' ? double.infinity : 100,
        height: 50,
        margin: const EdgeInsets.all(5),
        child: Center(child: Text('$orientation Widget 2', style: const TextStyle(color: Colors.white))),
      ),
    ];
  }
}
```

--------------------------------------------------------------------------------

## Clase 8: Interacción del Usuario: Botones y Campos de Texto

• **Información Relevante:**

    ◦ **Interactividad:** La experiencia de usuario (UX) se centra en cómo los usuarios interactúan con la interfaz. Esto incluye botones, campos de texto, scrolls y diálogos.

    ◦ **Manejo de Eventos:** Los widgets interactivos tienen callbacks (funciones) que se ejecutan cuando ocurre un evento del usuario. Por ejemplo, la propiedad `onPressed` en un botón.

    ◦ **Tipos de Botones:** Flutter proporciona una "familia" de botones con diferentes estilos y propósitos:

        ▪ **ElevatedButton****:** Botón con un efecto de elevación (sombra), para acciones principales.

        ▪ **TextButton****:** Botón de texto plano, para acciones menos prominentes.

        ▪ **OutlinedButton****:** Botón con un borde, para acciones secundarias.

        ▪ **FloatingActionButton** **(FAB):** Botón flotante generalmente circular, para la acción primaria de una pantalla.

        ▪ Otros: `IconButton`, `DropdownButton`, `SegmentedButton`.

    ◦ **Campos de Texto (****TextField****):** Permiten al usuario introducir texto. Son fundamentales para formularios.

    ◦ **TextEditingController****:** Un objeto que se utiliza para controlar y manipular el texto en un `TextField`. Permite leer el valor actual, establecer texto, escuchar cambios, etc..

    ◦ **InputDecoration****:** Permite personalizar la apariencia de un `TextField` con etiquetas, texto de ayuda, iconos, prefijos/sufijos, y manejo de errores.

    ◦ **FormField** **y** **TextFormField****:** Widgets que extienden `TextField` y añaden funcionalidad de validación y guardado para formularios.

• **Analogía:** Los botones son como los **interruptores y timbres** de una casa. `ElevatedButton` es el interruptor de la luz principal. `TextButton` es un interruptor más discreto para una lámpara. `FloatingActionButton` es el timbre de la puerta principal, siempre visible y para una acción importante. `TextField` es como una **pizarra interactiva** donde los usuarios pueden escribir información, y `TextEditingController` es el **marcador inteligente** que te permite ver, cambiar y borrar lo que está escrito en la pizarra.

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `interaccion_usuario`.

    2. En la pantalla principal, añade varios tipos de botones (`ElevatedButton`, `TextButton`, `OutlinedButton`, `FloatingActionButton`) con diferentes `onPressed` callbacks que muestren `SnackBar`s.

    3. Implementa un `TextField` para que el usuario introduzca su nombre.

    4. Asocia un `TextEditingController` al `TextField` para capturar el valor del texto.

    5. Añade un segundo `TextFormField` dentro de un `Form` widget, usando `InputDecoration` para añadir una etiqueta (`labelText`), texto de ayuda (`helperText`) y un icono, y con validación básica (por ejemplo, campo no vacío).

    6. Añade un botón para "Enviar" el formulario y mostrar los valores introducidos.

```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Interacción de Usuario',
      theme: ThemeData(
        primarySwatch: Colors.blueGrey,
      ),
      home: const InteractionScreen(),
    );
  }
}

class InteractionScreen extends StatefulWidget {
  const InteractionScreen({super.key});

  @override
  State<InteractionScreen> createState() => _InteractionScreenState();
}

class _InteractionScreenState extends State<InteractionScreen> {
  final TextEditingController _nameController = TextEditingController();
  final TextEditingController _emailController = TextEditingController();
  final _formKey = GlobalKey<FormState>(); // Clave global para el formulario

  @override
  void dispose() {
    _nameController.dispose();
    _emailController.dispose();
    super.dispose();
  }

  void _showSnackbar(String message) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(content: Text(message)),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Botones y Campos de Texto'),
      ),
      body: SingleChildScrollView( // Permite el scroll si el contenido se desborda
        padding: const EdgeInsets.all(16.0),
        child: Form(
          key: _formKey, // Asigna la clave al formulario
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              const Text(
                '1. Ejemplos de Botones:',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
              ),
              const SizedBox(height: 15),

              ElevatedButton(
                onPressed: () => _showSnackbar('ElevatedButton presionado'),
                child: const Text('Botón Elevado'),
              ),
              const SizedBox(height: 10),

              TextButton(
                onPressed: () => _showSnackbar('TextButton presionado'),
                child: const Text('Botón de Texto'),
              ),
              const SizedBox(height: 10),

              OutlinedButton(
                onPressed: () => _showSnackbar('OutlinedButton presionado'),
                child: const Text('Botón Contorneado'),
              ),
              const SizedBox(height: 20),

              const Text(
                '2. Campos de Texto:',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
              ),
              const SizedBox(height: 15),

              // TextField simple con TextEditingController
              TextField(
                controller: _nameController,
                decoration: const InputDecoration(
                  labelText: 'Nombre',
                  hintText: 'Introduce tu nombre',
                  prefixIcon: Icon(Icons.person),
                  border: OutlineInputBorder(),
                ),
                onChanged: (text) {
                  // Se ejecuta cada vez que el texto cambia
                  print('Nombre actual: $text');
                },
              ),
              const SizedBox(height: 20),

              // TextFormField con validación
              TextFormField(
                controller: _emailController,
                decoration: const InputDecoration(
                  labelText: 'Correo Electrónico',
                  hintText: 'ejemplo@dominio.com',
                  suffixIcon: Icon(Icons.email),
                  border: OutlineInputBorder(),
                  helperText: 'Introduce un correo válido',
                ),
                keyboardType: TextInputType.emailAddress,
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Por favor, introduce tu correo';
                  }
                  if (!value.contains('@')) {
                    return 'Introduce un correo válido';
                  }
                  return null;
                },
              ),
              const SizedBox(height: 30),

              ElevatedButton.icon(
                onPressed: () {
                  // Si el formulario es válido, muestra los datos
                  if (_formKey.currentState!.validate()) {
                    _showSnackbar(
                        'Datos enviados: Nombre: ${_nameController.text}, Email: ${_emailController.text}');
                  }
                },
                icon: const Icon(Icons.send),
                label: const Text('Enviar Formulario'),
                style: ElevatedButton.styleFrom(
                  padding: const EdgeInsets.symmetric(vertical: 12),
                  textStyle: const TextStyle(fontSize: 18),
                ),
              ),
            ],
          ),
        ),
      ),
      floatingActionButton: FloatingActionButton.extended(
        onPressed: () => _showSnackbar('FAB extendido presionado'),
        label: const Text('Acción Principal'),
        icon: const Icon(Icons.star),
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerFloat,
    );
  }
}
```

--------------------------------------------------------------------------------

## Clase 9: Listas y Scrolling: Manejo Eficiente de Datos en Pantalla

• **Información Relevante:**

    ◦ **ListView****:** Un widget fundamental para mostrar listas desplazables de elementos.

        ▪ **ListView.builder****:** El constructor más eficiente para listas largas o infinitas, ya que solo construye los elementos que son visibles en la pantalla (virtualización de UI). Requiere `itemCount` y `itemBuilder`.

        ▪ `itemExtent`: Si todos los elementos de la lista tienen una altura fija, especificar esta propiedad mejora el rendimiento.

        ▪ `ScrollController`: Permite programáticamente controlar el desplazamiento de la lista (por ejemplo, ir a una posición específica).

    ◦ **ListTile****:** Un widget de Material Design que se usa comúnmente como hijo de un `ListView`. Contiene típicamente una a tres líneas de texto y puede incluir un icono inicial (`leading`) y un widget final (`trailing`).

    ◦ **GridView****:** Un widget para mostrar una cuadrícula desplazable de elementos. Útil para galerías de imágenes o productos.

        ▪ `GridView.builder`: Al igual que `ListView.builder`, es eficiente para cuadrículas grandes.

        ▪ `SliverGridDelegateWithFixedCrossAxisCount` / `SliverGridDelegateWithMaxCrossAxisExtent`: Controlan cómo se organizan los elementos en la cuadrícula (número fijo de columnas o ancho máximo por elemento).

    ◦ **SingleChildScrollView****:** Permite que un solo widget hijo se desplace. Útil cuando tienes un contenido que podría exceder el tamaño de la pantalla (como un formulario largo o una descripción extensa) y no es una lista de elementos dinámicos.

    ◦ **CustomScrollView** **y Slivers:** Widgets avanzados para crear efectos de desplazamiento personalizados, como AppBars que se colapsan o expansiones complejas. Los `SliverAppBar` y `SliverList` son ejemplos de slivers.

• **Analogía:** `ListView` es como una **escalera mecánica infinita** en un centro comercial, mostrando productos (elementos) a medida que la gente sube o baja. `ListView.builder` es una versión inteligente de esa escalera mecánica que solo fabrica el producto cuando está a punto de ser visible, ahorrando recursos. `GridView` es como un **tablero de anuncios con fotos**, donde puedes ver varias imágenes a la vez y desplazarte para ver más. `SingleChildScrollView` es como un **pergamino que puedes enrollar o desenrollar** para ver todo el contenido, útil para documentos largos.

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `listas_y_scroll`.

    2. Implementa una `ListView.builder` que muestre 50 elementos de texto (por ejemplo, "Item 1", "Item 2", etc.). Cada elemento debe ser un `ListTile` con un icono y texto.

    3. Añade un `ScrollController` a la `ListView` y un botón flotante que, al presionarse, desplace la lista a una posición específica o al final.

    4. Crea una segunda pantalla o una sección en la misma pantalla que use `GridView.builder` para mostrar una cuadrícula de imágenes o tarjetas. Utiliza `SliverGridDelegateWithFixedCrossAxisCount` para definir un número fijo de columnas.

    5. Añade un `SingleChildScrollView` que contenga un texto largo (Lorem Ipsum) para demostrar su funcionalidad.

```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Listas y Scroll',
      theme: ThemeData(
        primarySwatch: Colors.green,
      ),
      home: const ListAndScrollScreen(),
    );
  }
}

class ListAndScrollScreen extends StatefulWidget {
  const ListAndScrollScreen({super.key});

  @override
  State<ListAndScrollScreen> createState() => _ListAndScrollScreenState();
}

class _ListAndScrollScreenState extends State<ListAndScrollScreen> {
  final ScrollController _scrollController = ScrollController();
  final List<String> items = List<String>.generate(50, (i) => 'Elemento ${i + 1}');

  @override
  void dispose() {
    _scrollController.dispose();
    super.dispose();
  }

  void _scrollToEnd() {
    _scrollController.animateTo(
      _scrollController.position.maxScrollExtent,
      duration: const Duration(seconds: 1),
      curve: Curves.easeOut,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Manejo Eficiente de Datos en Pantalla'),
      ),
      body: Column(
        children: [
          // Sección de ListView
          Expanded(
            child: ListView.builder(
              controller: _scrollController,
              itemCount: items.length,
              itemBuilder: (context, index) {
                return ListTile(
                  leading: const Icon(Icons.arrow_right),
                  title: Text(items[index]),
                  subtitle: Text('Detalle del ${items[index]}'),
                  onTap: () {
                    ScaffoldMessenger.of(context).showSnackBar(
                      SnackBar(content: Text('Presionado ${items[index]}')),
                    );
                  },
                );
              },
            ),
          ),
          const Divider(),
          // Sección de GridView
          const Padding(
            padding: EdgeInsets.all(8.0),
            child: Text(
              'Ejemplo de GridView:',
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
          ),
          Expanded(
            child: GridView.builder(
              gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
                crossAxisCount: 3, // 3 columnas
                crossAxisSpacing: 8.0, // Espacio horizontal entre celdas
                mainAxisSpacing: 8.0, // Espacio vertical entre celdas
              ),
              itemCount: 15, // Número de elementos en la cuadrícula
              itemBuilder: (context, index) {
                return Card(
                  color: Colors.green.shade100,
                  child: Center(
                    child: Text(
                      'Grid Item ${index + 1}',
                      style: const TextStyle(fontSize: 16),
                    ),
                  ),
                );
              },
            ),
          ),
          const Divider(),
          // Sección de SingleChildScrollView
          const Padding(
            padding: EdgeInsets.all(8.0),
            child: Text(
              'Ejemplo de SingleChildScrollView (Texto Largo):',
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
          ),
          Expanded(
            child: SingleChildScrollView(
              padding: const EdgeInsets.all(16.0),
              child: Text(
                'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. ' * 5, // Repetir texto para hacerlo largo
                textAlign: TextAlign.justify,
                style: const TextStyle(fontSize: 16),
              ),
            ),
          ),
        ],
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _scrollToEnd,
        child: const Icon(Icons.arrow_downward),
      ),
    );
  }
}
```

--------------------------------------------------------------------------------

## Clase 10: Navegación entre Pantallas y Diálogos

• **Información Relevante:**

    ◦ **Navegación:** Permite a los usuarios moverse entre diferentes pantallas (o rutas/páginas) de la aplicación.

    ◦ **Navigator****:** Un widget que gestiona un "stack" (pila) de rutas. Cada pantalla es una `Route`.

        ▪ **push()****:** Añade una nueva ruta a la pila, mostrando una nueva pantalla. La pantalla anterior permanece en la pila.

        ▪ **pop()****:** Elimina la ruta superior de la pila, volviendo a la pantalla anterior.

        ▪ **pushReplacement()****:** Reemplaza la ruta actual por una nueva, eliminando la anterior de la pila. Útil para pantallas de login.

        ▪ **Rutas Nombradas (****pushNamed()****):** Permite navegar a rutas predefinidas en el `MaterialApp` utilizando un nombre de cadena.

        ▪ **Pasar datos:** Puedes pasar datos entre pantallas a través de los argumentos de `push` o utilizando un gestor de estado (ver Clase 11).

    ◦ **AppBar** **con botón "atrás":** El `Scaffold` automáticamente añade un botón de "atrás" en el `AppBar` si hay rutas previas en la pila del `Navigator`.

    ◦ **Diálogos (****AlertDialog****,** **SimpleDialog****):** Ventanas emergentes que requieren interacción del usuario.

        ▪ **showDialog()****:** Muestra un diálogo.

        ▪ **AlertDialog****:** Un diálogo de Material Design con título, contenido y botones de acción.

        ▪ `SimpleDialog`: Un diálogo más simple que puede tener una lista de opciones.

    ◦ **Hojas Inferiores (****BottomSheet****):** Paneles que se deslizan desde la parte inferior de la pantalla, útiles para mostrar un menú de opciones o contenido adicional.

• **Analogía:** La navegación es como **caminar por las habitaciones de una casa**. Cada habitación es una pantalla. `push()` es como abrir una puerta y entrar a una nueva habitación (la habitación anterior sigue ahí). `pop()` es como dar media vuelta y salir por la puerta por la que entraste. `pushReplacement()` es como teletransportarse a una nueva habitación, haciendo que la anterior desaparezca. Los diálogos son como **notas adhesivas emergentes** que aparecen para darte información o pedirte una decisión rápida. Una `BottomSheet` es como una **bandeja que se desliza de debajo de la mesa** con opciones adicionales.

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `navegacion_dialogos`.

    2. Define dos pantallas: `HomeScreen` y `DetailScreen`.

    3. En `HomeScreen`, añade un `ElevatedButton` que, al presionarse, use `Navigator.push()` para ir a `DetailScreen`, pasando un dato simple (por ejemplo, un `String` o un `int`).

    4. En `DetailScreen`, muestra el dato recibido y añade un `ElevatedButton` que use `Navigator.pop()` para volver a `HomeScreen`.

    5. En `HomeScreen`, añade otro botón que use `showDialog()` para mostrar un `AlertDialog` con un título, un mensaje y dos botones de acción (por ejemplo, "Aceptar" y "Cancelar").

    6. Añade un botón que muestre un `BottomSheet` (`showModalBottomSheet`) con varias opciones.

```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Navegación y Diálogos',
      theme: ThemeData(
        primarySwatch: Colors.deepOrange,
      ),
      home: const HomeScreen(),
      // Define rutas nombradas (opcional, pero buena práctica)
      routes: {
        '/detail': (context) => const DetailScreen(data: ''), // Se esperaría un argumento aquí, pero se maneja en push()
      },
    );
  }
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Pantalla Principal'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            // 1. Navegar a DetailScreen con datos
            ElevatedButton(
              onPressed: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => const DetailScreen(data: '¡Hola desde Home!'),
                  ),
                );
              },
              child: const Text('Ir a Pantalla de Detalle'),
            ),
            const SizedBox(height: 20),

            // 2. Mostrar AlertDialog
            ElevatedButton(
              onPressed: () {
                showDialog(
                  context: context,
                  builder: (BuildContext context) {
                    return AlertDialog(
                      title: const Text('Alerta Importante'),
                      content: const Text('Esta es una demostración de AlertDialog.'),
                      actions: <Widget>[
                        TextButton(
                          onPressed: () {
                            Navigator.of(context).pop(); // Cierra el diálogo
                            ScaffoldMessenger.of(context).showSnackBar(
                                const SnackBar(content: Text('Acción Cancelada')));
                          },
                          child: const Text('Cancelar'),
                        ),
                        TextButton(
                          onPressed: () {
                            Navigator.of(context).pop(); // Cierra el diálogo
                            ScaffoldMessenger.of(context).showSnackBar(
                                const SnackBar(content: Text('Acción Aceptada')));
                          },
                          child: const Text('Aceptar'),
                        ),
                      ],
                    );
                  },
                );
              },
              child: const Text('Mostrar Alerta'),
            ),
            const SizedBox(height: 20),

            // 3. Mostrar BottomSheet
            ElevatedButton(
              onPressed: () {
                showModalBottomSheet(
                  context: context,
                  builder: (BuildContext context) {
                    return SizedBox(
                      height: 200,
                      child: Column(
                        children: <Widget>[
                          ListTile(
                            leading: const Icon(Icons.share),
                            title: const Text('Compartir'),
                            onTap: () {
                              Navigator.pop(context);
                              ScaffoldMessenger.of(context).showSnackBar(
                                  const SnackBar(content: Text('Compartir presionado')));
                            },
                          ),
                          ListTile(
                            leading: const Icon(Icons.edit),
                            title: const Text('Editar'),
                            onTap: () {
                              Navigator.pop(context);
                              ScaffoldMessenger.of(context).showSnackBar(
                                  const SnackBar(content: Text('Editar presionado')));
                            },
                          ),
                          ListTile(
                            leading: const Icon(Icons.delete),
                            title: const Text('Eliminar'),
                            onTap: () {
                              Navigator.pop(context);
                              ScaffoldMessenger.of(context).showSnackBar(
                                  const SnackBar(content: Text('Eliminar presionado')));
                            },
                          ),
                        ],
                      ),
                    );
                  },
                );
              },
              child: const Text('Mostrar Opciones (BottomSheet)'),
            ),
          ],
        ),
      ),
    );
  }
}

class DetailScreen extends StatelessWidget {
  final String data;
  const DetailScreen({super.key, required this.data});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Pantalla de Detalle'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'Datos recibidos: $data',
              style: const TextStyle(fontSize: 24),
            ),
            const SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context); // Vuelve a la pantalla anterior
              },
              child: const Text('Volver a Home'),
            ),
          ],
        ),
      ),
    );
  }
}
```

--------------------------------------------------------------------------------

## Clase 11: Gestión de Estado (Básico): StatelessWidget, StatefulWidget y Patrones Simples

• **Información Relevante:**

    ◦ **Estado (State):** Datos que pueden cambiar durante la vida de un widget. El estado determina cómo se ve la UI en un momento dado.

    ◦ **Tipos de Estado:**

        ▪ **Estado efímero (Ephemeral State):** Estado que se mantiene localmente dentro de un solo widget (`StatefulWidget`). No necesita compartirse con otros widgets.

        ▪ **Estado de la aplicación (App State):** Estado que se comparte a través de múltiples widgets, en diferentes pantallas o que persiste entre sesiones.

    ◦ **StatelessWidget****:** Como vimos en la Clase 5, no tiene estado mutable. Sus propiedades son inmutables.

    ◦ **StatefulWidget****:** Un widget que puede tener estado mutable. Cuando el estado cambia, Flutter reconstruye el widget. Se compone de dos clases: el `StatefulWidget` en sí (inmutable) y la clase `State` (mutable).

        ▪ **setState()****:** El método clave dentro de la clase `State` para notificar a Flutter que el estado ha cambiado y que el widget necesita reconstruirse. Cualquier cambio de estado debe hacerse dentro de `setState`.

    ◦ **Separación Modelo-Vista (Model-View Separation):** Mantener la capa de datos (modelo) separada de la capa de UI (vista). Esto hace que el código sea más simple, legible y fácil de mantener y escalar.

    ◦ **InheritedWidget** **/** **InheritedNotifier****:** Widgets que permiten pasar datos de manera eficiente a los widgets descendientes en el árbol de widgets, sin tener que pasarlos explícitamente a través de constructores intermedios. `InheritedNotifier` es una subclase de `InheritedWidget` que escucha un `Listenable` y notifica a los oyentes cuando cambia.

    ◦ **ValueNotifier** **/** **ValueListenableBuilder****:** Una solución ligera para manejar el estado. `ValueNotifier` es una clase `Listenable` que contiene un único valor. `ValueListenableBuilder` es un widget que reconstruye su interfaz solo cuando el `ValueNotifier` al que escucha cambia, evitando reconstrucciones innecesarias de árboles de widgets grandes.

• **Analogía:** Imagina tu aplicación como un **teatro de marionetas**. Los `StatelessWidget` son marionetas que siempre se ven igual. Los `StatefulWidget` son marionetas que pueden cambiar de ropa o expresión (su estado). `setState()` es como el director del teatro que grita "¡Cambio de escena!" para que la marioneta cambie. `InheritedWidget` es como un **tablón de anuncios universal** en el backstage; cualquier marioneta puede mirar el tablón para obtener información que necesite. `ValueNotifier` es como un **micrófono inalámbrico** que una marioneta puede usar para anunciar un cambio, y `ValueListenableBuilder` es como un **grupo de oyentes selectivos** que solo actúan cuando escuchan algo en ese micrófono específico, ignorando el resto del ruido.

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `gestion_estado_basico`.

    2. Implementa un contador simple usando `StatefulWidget` y `setState()`. Muestra cómo el `setState` reconstruye todo el `build` method.

    3. Refactoriza el contador para usar `ValueNotifier` y `ValueListenableBuilder`. Observa cómo solo el widget `Text` que muestra el contador se reconstruye, no toda la pantalla, lo que mejora el rendimiento.

    4. Crea un `InheritedWidget` o `InheritedNotifier` simple (siguiendo el ejemplo de `PlanProvider` de las fuentes) para compartir un valor (por ejemplo, el tema actual de la app) con sus descendientes.

```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

// ============== Ejemplo con StatefulWidget y setState() ==============
class CounterAppWithSetState extends StatefulWidget {
  const CounterAppWithSetState({super.key});

  @override
  State<CounterAppWithSetState> createState() => _CounterAppWithSetStateState();
}

class _CounterAppWithSetStateState extends State<CounterAppWithSetState> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
      print('setState() - Contador: $_counter'); // Observa que todo el build se ejecuta
    });
  }

  @override
  Widget build(BuildContext context) {
    print('setState() - Reconstruyendo CounterAppWithSetState');
    return Scaffold(
      appBar: AppBar(title: const Text('Contador con setState()')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text('Has pulsado el botón muchas veces:'),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headlineMedium,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Incrementar',
        child: const Icon(Icons.add),
      ),
    );
  }
}

// ============== Ejemplo con ValueNotifier y ValueListenableBuilder ==============
class CounterAppWithValueNotifier extends StatefulWidget {
  const CounterAppWithValueNotifier({super.key});

  @override
  State<CounterAppWithValueNotifier> createState() => _CounterAppWithValueNotifierState();
}

class _CounterAppWithValueNotifierState extends State<CounterAppWithValueNotifier> {
  final ValueNotifier<int> _counter = ValueNotifier<int>(0);

  @override
  void dispose() {
    _counter.dispose(); // Es importante liberar el ValueNotifier
    super.dispose();
  }

  void _incrementCounter() {
    _counter.value++; // Cambia el valor directamente, ValueNotifier notificará
    print('ValueNotifier - Contador: ${_counter.value}');
  }

  @override
  Widget build(BuildContext context) {
    print('ValueNotifier - Reconstruyendo CounterAppWithValueNotifier (solo una vez inicial)');
    return Scaffold(
      appBar: AppBar(title: const Text('Contador con ValueNotifier')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text('Has pulsado el botón muchas veces:'),
            // ValueListenableBuilder solo reconstruye su hijo cuando _counter.value cambia
            ValueListenableBuilder<int>(
              valueListenable: _counter,
              builder: (context, value, child) {
                print('ValueListenableBuilder - Reconstruyendo Text widget: $value');
                return Text(
                  '$value',
                  style: Theme.of(context).textTheme.headlineMedium,
                );
              },
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Incrementar',
        child: const Icon(Icons.add),
      ),
    );
  }
}

// ============== Aplicación principal ==============
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Gestión de Estado',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: DefaultTabController(
        length: 2,
        child: Scaffold(
          appBar: AppBar(
            title: const Text('Ejemplos de Gestión de Estado'),
            bottom: const TabBar(
              tabs: [
                Tab(text: 'setState()'),
                Tab(text: 'ValueNotifier'),
              ],
            ),
          ),
          body: const TabBarView(
            children: [
              CounterAppWithSetState(),
              CounterAppWithValueNotifier(),
            ],
          ),
        ),
      ),
    );
  }
}
```

--------------------------------------------------------------------------------

## Clase 12: Gestión de Estado (Avanzado): Programación Asíncrona y Streams

• **Información Relevante:**

    ◦ **Programación Asíncrona:** Crucial para operaciones que tardan tiempo (red, E/S de archivos, cálculos complejos) sin bloquear la interfaz de usuario.

    ◦ **Future****:** Representa un valor o error que estará disponible en algún momento en el futuro.

    ◦ **async** **y** **await****:** Simplifican el código asíncrono, permitiéndote escribirlo como si fuera síncrono. `async` marca una función como asíncrona; `await` pausa la ejecución hasta que un `Future` se completa.

    ◦ **FutureBuilder****:** Un widget de Flutter que construye la UI basándose en el estado de un `Future` (esperando, completado con datos, completado con error). Flutter gestiona la reconstrucción de la UI cuando el `Future` se resuelve.

    ◦ **Stream****:** Representa una secuencia de valores o errores que pueden llegar en el tiempo. Útil para datos que cambian continuamente (chats, actualizaciones de base de datos en tiempo real, eventos del usuario).

    ◦ **StreamBuilder****:** Similar a `FutureBuilder`, pero construye la UI basándose en los eventos de un `Stream`. Se reconstruye cada vez que el `Stream` emite un nuevo valor.

    ◦ **Patrón BLoC (Business Logic Component):** Un patrón de gestión de estado popular que utiliza `Streams` para separar la lógica de negocio de la UI. Los eventos de la UI se envían a un BLoC, que procesa la lógica y emite nuevos estados como `Streams` que la UI escucha.

• **Analogía:** `Future` es como pedir una pizza: haces el pedido, y en algún momento en el futuro (cuando esté lista), te la entregan. `async`/`await` es como esperar pacientemente por la pizza, sin hacer nada más hasta que llega. `Stream` es como una **radio en vivo**: la enciendes, y recibes un flujo continuo de música o noticias a lo largo del tiempo. `FutureBuilder` y `StreamBuilder` son como **paneles de control inteligentes** en tu UI; se conectan a tu pizza (Future) o a tu radio (Stream) y actualizan automáticamente la pantalla cuando llega la pizza o cuando la radio emite algo nuevo. BLoC es como el **cerebro de un robot**; toma decisiones (eventos de la UI), las procesa (lógica de negocio) y luego le dice a los brazos y piernas (la UI) qué hacer.

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `async_streams_bloc`.

    2. Implementa una función asíncrona que simule una llamada a la red usando `Future.delayed`. Utiliza `async` y `await`.

    3. Usa `FutureBuilder` para mostrar un `CircularProgressIndicator` mientras la función asíncrona está en progreso, y luego muestra los datos resultantes.

    4. Crea un `Stream` simple que emita números cada segundo.

    5. Usa `StreamBuilder` para mostrar los valores emitidos por el `Stream` en tiempo real.

    6. (Opcional, si el tiempo lo permite y para un desafío mayor) Implementa un contador básico con el patrón BLoC, donde un `StreamController` maneje los eventos de incremento y un `StreamBuilder` muestre el estado del contador.

```
import 'dart:async';
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Async, Streams y BLoC',
      theme: ThemeData(
        primarySwatch: Colors.deepPurple,
      ),
      home: DefaultTabController(
        length: 3,
        child: Scaffold(
          appBar: AppBar(
            title: const Text('Async, Streams y BLoC'),
            bottom: const TabBar(
              tabs: [
                Tab(text: 'FutureBuilder'),
                Tab(text: 'StreamBuilder'),
                Tab(text: 'BLoC (básico)'),
              ],
            ),
          ),
          body: const TabBarView(
            children: [
              FutureBuilderScreen(),
              StreamBuilderScreen(),
              BlocCounterScreen(), // Implementación básica de BLoC
            ],
          ),
        ),
      ),
    );
  }
}

// ============== 1. FutureBuilder Example ==============
Future<String> _fetchData() async {
  await Future.delayed(const Duration(seconds: 3));
  return 'Datos cargados exitosamente!';
}

class FutureBuilderScreen extends StatelessWidget {
  const FutureBuilderScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: FutureBuilder<String>(
        future: _fetchData(),
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return const CircularProgressIndicator();
          } else if (snapshot.hasError) {
            return Text('Error: ${snapshot.error}');
          } else if (snapshot.hasData) {
            return Text(
              snapshot.data!,
              style: const TextStyle(fontSize: 24, color: Colors.deepPurple),
            );
          } else {
            return const Text('No hay datos');
          }
        },
      ),
    );
  }
}

// ============== 2. StreamBuilder Example ==============
Stream<int> _numberStream() async* {
  for (int i = 1; i <= 10; i++) {
    await Future.delayed(const Duration(seconds: 1));
    yield i; // Emite un valor
  }
}

class StreamBuilderScreen extends StatelessWidget {
  const StreamBuilderScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: StreamBuilder<int>(
        stream: _numberStream(),
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return const Text(
              'Esperando números...',
              style: TextStyle(fontSize: 24, color: Colors.deepPurple),
            );
          } else if (snapshot.hasError) {
            return Text('Error: ${snapshot.error}');
          } else if (snapshot.hasData) {
            return Text(
              'Número actual: ${snapshot.data}',
              style: const TextStyle(fontSize: 36, fontWeight: FontWeight.bold, color: Colors.deepPurple),
            );
          } else {
            return const Text('Stream terminado');
          }
        },
      ),
    );
  }
}

// ============== 3. Basic BLoC Example (Contador) ==============
class CounterBloc {
  final _controller = StreamController<int>(); // Stream para el estado del contador
  final _eventController = StreamController<CounterEvent>(); // Stream para los eventos

  int _counter = 0;

  CounterBloc() {
    _eventController.stream.listen((event) {
      if (event == CounterEvent.increment) {
        _counter++;
      } else if (event == CounterEvent.decrement) {
        _counter--;
      }
      _controller.sink.add(_counter); // Añade el nuevo estado al stream
    });
  }

  Stream<int> get counterStream => _controller.stream;
  Sink<CounterEvent> get eventSink => _eventController.sink;

  void dispose() {
    _controller.close();
    _eventController.close();
  }
}

enum CounterEvent { increment, decrement }

class BlocCounterScreen extends StatefulWidget {
  const BlocCounterScreen({super.key});

  @override
  State<BlocCounterScreen> createState() => _BlocCounterScreenState();
}

class _BlocCounterScreenState extends State<BlocCounterScreen> {
  final _bloc = CounterBloc();

  @override
  void dispose() {
    _bloc.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text('Contador BLoC:'),
            StreamBuilder<int>(
              stream: _bloc.counterStream,
              initialData: 0,
              builder: (context, snapshot) {
                return Text(
                  '${snapshot.data}',
                  style: Theme.of(context).textTheme.headlineLarge,
                );
              },
            ),
          ],
        ),
      ),
      floatingActionButton: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          FloatingActionButton(
            heroTag: 'incrementBtn', // Unique tag for multiple FABs
            onPressed: () => _bloc.eventSink.add(CounterEvent.increment),
            child: const Icon(Icons.add),
          ),
          const SizedBox(height: 10),
          FloatingActionButton(
            heroTag: 'decrementBtn', // Unique tag
            onPressed: () => _bloc.eventSink.add(CounterEvent.decrement),
            child: const Icon(Icons.remove),
          ),
        ],
      ),
    );
  }
}
```

--------------------------------------------------------------------------------

## Clase 13: Comunicación con Servicios Web y Persistencia de Datos

• **Información Relevante:**

    ◦ **Comunicación HTTP:** La mayoría de las aplicaciones necesitan interactuar con servicios web (APIs REST) para obtener o enviar datos.

        ▪ **http** **package:** Una biblioteca popular para realizar solicitudes HTTP (GET, POST, PUT, DELETE, PATCH).

        ▪ **JSON (JavaScript Object Notation):** El formato más común para intercambiar datos con servicios web. Dart tiene librerías para codificar (`jsonEncode`) y decodificar (`jsonDecode`) JSON.

        ▪ **Serialización/Deserialización:** Convertir objetos Dart a JSON (serialización) y JSON a objetos Dart (deserialización).

    ◦ **Persistencia de Datos Local:** Guardar datos en el dispositivo del usuario para que estén disponibles sin conexión o entre sesiones.

        ▪ **shared_preferences** **package:** Para almacenar pequeñas cantidades de datos clave-valor (como configuraciones de usuario, el tema seleccionado, tokens). Es simple y eficiente para preferencias.

        ▪ **Bases de Datos Locales (ej. SQLite con** **moor****/****drift****,** **sqflite****):** Para almacenar grandes volúmenes de datos estructurados. Son más robustas y garantizan la persistencia.

        ▪ **Activos (****assets****):** Incluir archivos (imágenes, JSON) directamente en el paquete de la aplicación. Se accede a ellos usando `rootBundle`.

• **Analogía:** La comunicación con servicios web es como **pedir comida a domicilio** por teléfono. Haces una solicitud (HTTP GET/POST), y el restaurante (API) te devuelve la comida (JSON). La persistencia de datos local es como tener una **nevera o una despensa** en casa; guardas la comida para cuando la necesites, sin tener que pedirla siempre. `shared_preferences` es como el compartimento de especias, para pequeñas cosas; una base de datos local es como la nevera grande, para todo.

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `web_persistencia`.

    2. Añade el paquete `http` y `shared_preferences` a tu `pubspec.yaml`.

    3. Crea un modelo de datos simple (por ejemplo, `Post` con `userId`, `id`, `title`, `body`).

    4. Implementa una función asíncrona para realizar una solicitud GET a una API pública (por ejemplo, JSONPlaceholder `https://jsonplaceholder.typicode.com/posts/1`) y deserializar la respuesta JSON a tu modelo `Post`. Usa `FutureBuilder` para mostrar los datos.

    5. Añade dos `ElevatedButton`s: uno para "Guardar Configuración" y otro para "Cargar Configuración" usando `shared_preferences` para almacenar un `bool` (por ejemplo, `isDarkMode`) o un `String`.

```
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'package:shared_preferences/shared_preferences.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Web y Persistencia',
      theme: ThemeData(
        primarySwatch: Colors.indigo,
      ),
      home: const WebAndPersistenceScreen(),
    );
  }
}

// Modelo de datos para un Post
class Post {
  final int userId;
  final int id;
  final String title;
  final String body;

  Post({required this.userId, required this.id, required this.title, required this.body});

  factory Post.fromJson(Map<String, dynamic> json) {
    return Post(
      userId: json['userId'] as int,
      id: json['id'] as int,
      title: json['title'] as String,
      body: json['body'] as String,
    );
  }
}

class WebAndPersistenceScreen extends StatefulWidget {
  const WebAndPersistenceScreen({super.key});

  @override
  State<WebAndPersistenceScreen> createState() => _WebAndPersistenceScreenState();
}

class _WebAndPersistenceScreenState extends State<WebAndPersistenceScreen> {
  // Estado para HTTP
  late Future<Post> _postFuture;

  // Estado para Shared Preferences
  bool _isDarkMode = false;
  String? _savedMessage;

  @override
  void initState() {
    super.initState();
    _postFuture = _fetchPost(); // Inicia la carga del post
    _loadPreferences(); // Carga las preferencias al inicio
  }

  // ============== Funciones para HTTP ==============
  Future<Post> _fetchPost() async {
    final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

    if (response.statusCode == 200) {
      return Post.fromJson(jsonDecode(response.body) as Map<String, dynamic>);
    } else {
      throw Exception('Fallo al cargar el post');
    }
  }

  // ============== Funciones para Shared Preferences ==============
  Future<void> _loadPreferences() async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      _isDarkMode = prefs.getBool('isDarkMode') ?? false;
      _savedMessage = prefs.getString('message');
    });
  }

  Future<void> _savePreferences() async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setBool('isDarkMode', _isDarkMode);
    await prefs.setString('message', '¡Mensaje guardado en preferencias!');
    _loadPreferences(); // Volver a cargar para actualizar la UI
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('Preferencias guardadas!')),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Servicios Web y Persistencia'),
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            const Text(
              '1. Consumo de API REST (JSONPlaceholder):',
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 15),
            FutureBuilder<Post>(
              future: _postFuture,
              builder: (context, snapshot) {
                if (snapshot.connectionState == ConnectionState.waiting) {
                  return const Center(child: CircularProgressIndicator());
                } else if (snapshot.hasError) {
                  return Center(child: Text('Error: ${snapshot.error}'));
                } else if (snapshot.hasData) {
                  return Card(
                    child: Padding(
                      padding: const EdgeInsets.all(12.0),
                      child: Column(
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Text(
                            snapshot.data!.title,
                            style: const TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
                          ),
                          const SizedBox(height: 8),
                          Text(snapshot.data!.body),
                          const SizedBox(height: 8),
                          Text('User ID: ${snapshot.data!.userId}'),
                        ],
                      ),
                    ),
                  );
                } else {
                  return const Center(child: Text('No se encontraron datos.'));
                }
              },
            ),
            const SizedBox(height: 30),
            const Text(
              '2. Persistencia con SharedPreferences:',
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 15),
            SwitchListTile(
              title: const Text('Modo Oscuro'),
              value: _isDarkMode,
              onChanged: (bool value) {
                setState(() {
                  _isDarkMode = value;
                });
              },
            ),
            if (_savedMessage != null)
              Padding(
                padding: const EdgeInsets.symmetric(horizontal: 16.0, vertical: 8.0),
                child: Text('Mensaje guardado: $_savedMessage'),
              ),
            const SizedBox(height: 15),
            ElevatedButton(
              onPressed: _savePreferences,
              child: const Text('Guardar Preferencias'),
            ),
          ],
        ),
      ),
    );
  }
}
```

--------------------------------------------------------------------------------

## Clase 14: Temas, Estilos y Animaciones

• **Información Relevante:**

    ◦ **Consistencia Visual (****Theme** **y** **TextStyle****):** La consistencia es clave en el diseño. Flutter permite aplicar un estilo visual consistente en toda la aplicación.

    ◦ **ThemeData****:** Define los colores, las tipografías y otras propiedades visuales de tu aplicación. Se aplica en el `MaterialApp`.

    ◦ **ColorScheme****:** Un conjunto de colores derivados de un color semilla (`fromSeed`) que forman una paleta armoniosa para tu aplicación.

    ◦ **TextTheme****:** Un conjunto de estilos de texto para diferentes elementos (títulos, cuerpos, subtítulos) que se pueden acceder desde `Theme.of(context).textTheme`.

    ◦ **Fuentes Personalizadas:** Puedes importar fuentes desde Google Fonts o tus propios archivos de fuentes para personalizar la tipografía de tu app. Se declaran en `pubspec.yaml`.

    ◦ **Animaciones Básicas:** Mejoran la experiencia de usuario y hacen las apps más atractivas.

        ▪ **AnimationController****:** Gestiona el progreso de una animación (inicio, parada, avance, retroceso).

        ▪ **Tween****:** Define un rango de valores (principio a fin) entre los que una animación interpolará. Se combina con un `AnimationController`.

        ▪ **Curvas (****Curves****):** Definen la velocidad de la animación a lo largo de su duración (por ejemplo, `easeIn`, `linear`, `bounceOut`).

        ▪ **AnimatedBuilder****:** Un widget que reconstruye su hijo de manera eficiente cada vez que una `Animation` cambia, evitando reconstruir toda la UI.

        ▪ **Hero** **Animations:** Animaciones que transforman visualmente un widget de una pantalla a otra, creando una transición fluida (por ejemplo, una imagen que se "vuela" de una lista a una vista de detalle).

• **Analogía:** Los temas y estilos son como la **decoración interior de una casa**. `ThemeData` es el estilo general (moderno, rústico, minimalista). `ColorScheme` es la paleta de colores que utilizas en todas las habitaciones para mantener la armonía. `TextTheme` es el tipo de letra y el tamaño que usas para los títulos, subtítulos y textos normales. Las animaciones son como el **movimiento y la vida** que le das a los objetos en esa casa. Un `AnimationController` es el interruptor que enciende y apaga una luz. `Tween` es como definir el brillo inicial y final de esa luz. `Curves` es cómo la luz se enciende o apaga (suavemente, rápidamente, con un rebote). `Hero` Animation es como una **magia de teletransporte visual**; un objeto desaparece de un lugar y aparece en otro, pero con un rastro visual suave y agradable.

• **Ejemplo Práctico:**

    1. Crea un nuevo proyecto Flutter llamado `temas_y_animaciones`.

    2. Define un `ThemeData` en tu `MaterialApp` utilizando `ColorScheme.fromSeed` para un color semilla y personaliza algunos `TextTheme`s.

    3. Carga una fuente personalizada desde Google Fonts (`google_fonts` package) o un asset local y aplícala a un `Text` widget.

    4. Crea un `StatefulWidget` que implemente una animación simple: un `Container` que cambie de tamaño y color. Utiliza `AnimationController` y `Tween` con una `Curve`.

    5. (Opcional) Implementa una `Hero` Animation simple entre dos pantallas. Por ejemplo, una `CircleAvatar` en una lista que se expande a una imagen más grande en una pantalla de detalle.

```
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart'; // Asegúrate de añadir google_fonts a pubspec.yaml

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Temas y Animaciones',
      theme: ThemeData(
        // 1. Definir ThemeData con ColorScheme y TextTheme
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.purple),
        textTheme: GoogleFonts.latoTextTheme( // Usar una fuente de Google Fonts para el tema general
          Theme.of(context).textTheme.copyWith(
            displayLarge: GoogleFonts.pacifico(fontSize: 50, color: Colors.purple.shade700),
            headlineMedium: GoogleFonts.oswald(fontSize: 30, fontWeight: FontWeight.bold),
          ),
        ),
        appBarTheme: AppBarTheme(
          backgroundColor: Colors.purple.shade800,
          foregroundColor: Colors.white,
          titleTextStyle: GoogleFonts.patuaOne(fontSize: 28, color: Colors.white),
        ),
      ),
      home: const ThemeAndAnimationScreen(),
    );
  }
}

class ThemeAndAnimationScreen extends StatefulWidget {
  const ThemeAndAnimationScreen({super.key});

  @override
  State<ThemeAndAnimationScreen> createState() => _ThemeAndAnimationScreenState();
}

class _ThemeAndAnimationScreenState extends State<ThemeAndAnimationScreen>
    with SingleTickerProviderStateMixin { // Necesario para AnimationController
  late AnimationController _controller;
  late Animation<double> _sizeAnimation;
  late Animation<Color?> _colorAnimation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      vsync: this,
      duration: const Duration(seconds: 2),
    );

    // Animación de tamaño (de 50 a 200) con curva de rebote
    _sizeAnimation = Tween<double>(begin: 50, end: 200).animate(
      CurvedAnimation(parent: _controller, curve: Curves.bounceOut),
    );

    // Animación de color (de púrpura a ámbar)
    _colorAnimation = ColorTween(begin: Colors.purple, end: Colors.amber).animate(_controller);

    _controller.addListener(() {
      setState(() {}); // Forzar reconstrucción para ver los cambios de animación
    });

    _controller.repeat(reverse: true); // Repetir la animación de ida y vuelta
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Temas y Animaciones'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            // Texto con estilo del tema global y fuente personalizada
            Text(
              '¡Mi App Estilizada!',
              style: Theme.of(context).textTheme.displayLarge,
            ),
            const SizedBox(height: 20),
            Text(
              'Un subtítulo interesante',
              style: Theme.of(context).textTheme.headlineMedium,
            ),
            const SizedBox(height: 40),

            // Contenedor animado
            AnimatedBuilder(
              animation: _controller,
              builder: (context, child) {
                return Container(
                  width: _sizeAnimation.value,
                  height: _sizeAnimation.value,
                  decoration: BoxDecoration(
                    color: _colorAnimation.value,
                    borderRadius: BorderRadius.circular(_sizeAnimation.value / 2),
                  ),
                  child: const Center(
                    child: Text(
                      '¡Animado!',
                      style: TextStyle(color: Colors.white, fontSize: 20),
                    ),
                  ),
                );
              },
            ),
            const SizedBox(height: 40),

            // Ejemplo de Hero Animation (Placeholder, requiere otra pantalla)
            const Text(
              'Hero Animation (requiere navegación):',
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 10),
            Hero(
              tag: 'avatarTag',
              child: GestureDetector(
                onTap: () {
                  Navigator.push(
                    context,
                    MaterialPageRoute(builder: (context) => const DetailHeroScreen()),
                  );
                },
                child: CircleAvatar(
                  radius: 40,
                  backgroundColor: Colors.blue.shade300,
                  child: const Icon(Icons.flight_takeoff, size: 50, color: Colors.white),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}

class DetailHeroScreen extends StatelessWidget {
  const DetailHeroScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Detalle del Héroe'),
      ),
      body: Center(
        child: Hero(
          tag: 'avatarTag',
          child: Container(
            width: 300,
            height: 300,
            decoration: BoxDecoration(
              color: Colors.blue.shade500,
              borderRadius: BorderRadius.circular(150),
            ),
            child: const Icon(Icons.flight_takeoff, size: 200, color: Colors.white),
          ),
        ),
      ),
    );
  }
}
```

--------------------------------------------------------------------------------

## Clase 15: Integración con Firebase y Machine Learning

• **Información Relevante:**

    ◦ **Firebase:** Una plataforma backend como servicio (BaaS) desarrollada por Google que simplifica el desarrollo de aplicaciones al proporcionar servicios backend sin que tengas que escribir código de servidor.

    ◦ **Configuración de Firebase:** Implica crear un proyecto en la consola de Firebase, registrar tu aplicación y añadir los paquetes de Flutter necesarios (`firebase_core`, y luego servicios específicos).

    ◦ **Autenticación (****Firebase Authentication****):** Proporciona servicios de autenticación de usuario (correo/contraseña, Google Sign-in, Facebook, etc.).

        ▪ `Google Sign-in`: Permite a los usuarios iniciar sesión con sus cuentas de Google.

    ◦ **Cloud Firestore:** Una base de datos NoSQL flexible y escalable para almacenar y sincronizar datos en tiempo real.

        ▪ Leer y escribir datos: API sencilla para operaciones CRUD (Create, Read, Update, Delete).

    ◦ **Firebase Analytics:** Herramienta de análisis de comportamiento del usuario para obtener información sobre cómo los usuarios interactúan con tu aplicación.

    ◦ **Firebase ML Kit (Machine Learning):** Ofrece API listas para usar de Machine Learning para tareas comunes.

        ▪ **Reconocimiento de Texto:** Extraer texto de imágenes.

        ▪ **Lectura de Códigos de Barras:** Escanear códigos de barras y QR.

        ▪ **Etiquetado de Imágenes:** Identificar objetos, conceptos y acciones en imágenes.

        ▪ **Identificación de Idioma:** Determinar el idioma de un texto.