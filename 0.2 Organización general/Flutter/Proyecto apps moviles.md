Dividir la programación en modulos, funciones y widgets.

Main dart de una app de una sola pantalla conectada con firebase
```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'package:cloud_firestore/cloud_firestore.dart';

void main() async {
  // Asegura que la inicialización de Firebase ocurra antes decorrer la app
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(); // Inicializa Firebase
  runApp(const MyApp()); // Lanza la aplicación
}

// Widget principal
class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      debugShowCheckedModeBanner: false, // Quita la etiqueta de debug
      home: ProductosScreen(), // Pantalla principal que muestra los productos
    );
  }
}

// Pantalla que lista los documentos de la colección 'productos'
class ProductosScreen extends StatefulWidget {
  const ProductosScreen({super.key});
  @override
  State<ProductosScreen> createState() => _ProductosScreenState();
}

class _ProductosScreenState extends State<ProductosScreen> {
  List<Map<String, dynamic>> productos = []; // Lista para guardar los productos
  @override
  void initState() {
    super.initState();
    obtenerProductos(); // Carga los productos al iniciar la pantalla
    print('Productos obtenidos: $productos');
  }

  // Función para obtener los documentos de la colección 'productos'
  Future<void> obtenerProductos() async {
    try {
      // Accede a la colección 'productos' y obtiene todos losdocumentos
      final snapshot = await FirebaseFirestore.instance
          .collection('productos')
          .get();
      // Transforma los documentos en una lista de mapas
      setState(() {
        productos = snapshot.docs
            .map(
              (doc) => {
                'id': doc.id, // Guarda el ID del documento
                ...doc.data(), // Agrega el contenido deldocumento
              },
            )
            .toList();
      });
    } catch (e) {
      print('Error al obtener productos: $e');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Lista de Productos')),
      body: productos.isEmpty
          ? const Center(child: CircularProgressIndicator()) // Cargando...
          : ListView.builder(
              itemCount: productos.length,
              itemBuilder: (context, index) {
                final producto = productos[index];
                return ListTile(
                  title: Text(producto['Nombre'] ?? 'Sin nombre'),
                  subtitle: Text('Precio: S/ ${producto['Precio'] ?? '0.00'}'),
                  trailing: Text('ID: ${producto['id']}'),
                );
              },
            ),
    );
  }
}
```