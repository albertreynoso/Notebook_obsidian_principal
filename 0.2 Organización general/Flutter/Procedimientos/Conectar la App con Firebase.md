# Recomendaciones iniciales
- Utilizar el celular para emular el proyecto
- Verificar permisos de la base de datos antes de extraer data
# Preparación de entorno
Paso 1: Instalar Flutter y Firebase CLI
- Tener instalado Flutter SDK y Android Studio o VS Code.
- Crear cuenta gratuita en Firebase Console.
# Crear un nuevo proyecto en Flutter
- Abrir vscode
- Pulsar ctrl + shift + p
- Escribir Flutter: New proyect
- Seleccionar Empty Application
- Guardar el proyecto con el nombre de la empresa
# Configurar el proyecto en Firebase
### Paso 1: Crear un nuevo proyecto en firebase
- Entra a Firebase console
- Haz clic en crear proyecto
	- Usar el nombre de la empresa
	- Sigue los pasos
	- No habilitar Google Analytics
### Paso 2: Registrar tu app Flutter en Firebase
- Elige agregar aplicacion android
- Ingresa el nombre del paquete (lo encuentras en android/app/build.gradle).
  ![[Pasted image 20251002211325.png]]
- Sigue los pasos especificados en Firebase
### Paso 3: Activar Realtime Database
- En firebase Console ➔ Database ➔ Realtime Database ➔ Crear Base de Datos.
- Elige modo de prueba (reglas abiertas por ahora).
# Configurar dependencias en FLUTTER
- Editar pubspec.yaml
  ![[Pasted image 20251002211634.png|300]]
- Seguir los pasos especificados en Firebase
# Inicializar Firebase en el proyecto

```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'package:firebase_database/firebase_database.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(const MainApp());
}

class MainApp extends StatelessWidget {
  const MainApp({super.key});
  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: Scaffold(body: Center(child: Text('Hello World!'))),
    );
  }
}
```

# Crear la primera interfaz con conexión a la base de datos
Editamos el main.dart:

```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import 'home_screen.dart';
import 'clients_screen.dart';
import 'ubications_screen.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(const MainApp());
}

class MainApp extends StatelessWidget {
  const MainApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "Bottom Nav Bar",
      theme: ThemeData(primarySwatch: Colors.cyan),
      home: const BottomNav(),
    );
  }
}

class BottomNav extends StatefulWidget {
  const BottomNav({super.key});

  @override
  State<BottomNav> createState() => _BottomNavState();
}

class _BottomNavState extends State<BottomNav> {
  int _select = 0;

  final List<Widget> _pantallas = const [
    HomeScreen(),
    ClientsScreen(),
    UbicationsScreen(),
  ];

  void _onItemSelected(int index) {
    setState(() {
      _select = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: _pantallas[_select],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _select,
        onTap: _onItemSelected,
        items: const [
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            label: "Inicio",
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.people),
            label: "Clientes",
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.map),
            label: "Ubicaciones",
          ),
        ],
      ),
    );
  }
}
```
