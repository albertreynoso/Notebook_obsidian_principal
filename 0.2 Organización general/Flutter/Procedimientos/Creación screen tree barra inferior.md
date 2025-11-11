Aplicación con diferentes pantallas en navegación inferior
Archivos integrados
- main.dart
- home_screen.dart
- clients_screen.dart
- ubications_screen.dart
```dart

```
## main.dart
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
## home_screen.dart
```dart
import 'package:flutter/material.dart';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  @override
  Widget build(BuildContext context) {
    return const Scaffold(
      body: Center(
        child: Text('HomeScreen'),
      ),
    );
  }
}
```
## clients_screen.dart
```dart
import 'package:flutter/material.dart';


class ClientsScreen extends StatefulWidget {
  const ClientsScreen({super.key});

  @override
  State<ClientsScreen> createState() => _ClientsScreenState();
}

class _ClientsScreenState extends State<ClientsScreen> {
  @override
  Widget build(BuildContext context) {
    return const Scaffold(
      body: Center(
        child: Text('ClientsScreen'),
      ),
    );
  }
}
```
## ubications_screen.dart
```dart
import 'package:flutter/material.dart';

class UbicationsScreen extends StatefulWidget {
  const UbicationsScreen({super.key});

  @override
  State<UbicationsScreen> createState() => _UbicationsScreenState();
}

class _UbicationsScreenState extends State<UbicationsScreen> {
  @override
  Widget build(BuildContext context) {
    return const Scaffold(
      body: Center(
        child: Text('UbicationsScreen'),
      ),
    );
  }
}
```
