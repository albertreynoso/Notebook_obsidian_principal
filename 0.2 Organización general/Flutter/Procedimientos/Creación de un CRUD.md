Siempre empezar por la vista de lectura, que muestre los datos creados en la base de datos
# Codigo CRUD Screen Tech Store
```dart
import 'package:flutter/material.dart';
import 'package:cloud_firestore/cloud_firestore.dart';

class TechStoreScreen extends StatefulWidget {
  const TechStoreScreen({super.key});
  @override
  State<TechStoreScreen> createState() => _TechStoreScreenState();
}

class _TechStoreScreenState extends State<TechStoreScreen> {
  final TextEditingController _nombre = TextEditingController();
  final TextEditingController _precio = TextEditingController();
  final TextEditingController _marca = TextEditingController();
  final TextEditingController _stock = TextEditingController();
  String? _tipoSeleccionado;
  bool _estado = true;
  final List<String> _tipo = [
    'Accesorio',
    'Dispositivo',
    'Componente',
  ];
  String? _idSeleccionado;
  List<Map<String, dynamic>> productos = [];
  @override
  void initState() {
    super.initState();
    readProductos();
  }

  Future<void> createProductos() async {
    if (!_validarCampos()) return;
    final datos = {
      'nombre': _nombre.text,
      'precio': double.tryParse(_precio.text) ?? 0.0,
      'marca': _marca.text,
      'tipo': _tipoSeleccionado,
      'stock': int.tryParse(_stock.text) ?? 0,
      'estado': _estado,
    };
    try {
      await FirebaseFirestore.instance
          .collection('productos_tecnologicos')
          .add(datos);
      limpiarFormulario();
    } catch (e) {
      print('Error al crear producto: $e');
    }
  }

  Future<void> readProductos() async {
    try {
      final snapshot = await FirebaseFirestore.instance
          .collection('productos_tecnologicos')
          .get();
      setState(() {
        productos = snapshot.docs
            .map((doc) => {'id': doc.id, ...doc.data()})
            .toList();
      });
    } catch (e) {
      print('Error al leer productos: $e');
    }
  }

  Future<void> updateProductos(String id) async {
    if (!_validarCampos()) return;
    final datos = {
      'nombre': _nombre.text,
      'precio': double.tryParse(_precio.text) ?? 0.0,
      'marca': _marca.text,
      'categoria': _tipoSeleccionado,
      'stock': int.tryParse(_stock.text) ?? 0,
      'estado': _estado,
    };
    try {
      await FirebaseFirestore.instance
          .collection('productos_tecnologicos')
          .doc(id)
          .update(datos);
      limpiarFormulario();
    } catch (e) {
      print('Error al actualizar productos: $e');
    }
  }

  Future<void> deleteProductos(String id) async {
    try {
      await FirebaseFirestore.instance.collection('productos_tecnologicos').doc(id).delete();
      await readProductos();
      limpiarFormulario();
    } catch (e) {
      print('Error al eliminar productos: $e');
    }
  }

  void limpiarFormulario() {
    setState(() {
      _nombre.clear();
      _precio.clear();
      _marca.clear();
      _tipoSeleccionado = null;
      _stock.clear();
      _estado = true;
      _idSeleccionado = null;
    });
  }

  bool _validarCampos() {
    // Lista para acumular errores
    List<String> errores = [];

    if (_nombre.text.isEmpty ||
        _precio.text.isEmpty ||
        _marca.text.isEmpty ||
        _stock.text.isEmpty ||
        _tipoSeleccionado == null) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Por favor completa todos los campos')),
      );
      return false;
    }
    
    // Validar precio
    final precio = double.tryParse(_precio.text.replaceAll(',', '.'));
    if (precio == null) {
      errores.add('El precio debe ser un número válido');
    } else if (precio <= 0) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('El precio debe ser mayor a 0')),
      );
      return false;
    } 
  


    return true;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Tech Store'),
        backgroundColor: const Color.fromARGB(122, 152, 120, 102),
        centerTitle: true,
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _nombre,
              decoration: const InputDecoration(
                labelText: "Nombre del producto",
                icon: Icon(Icons.label),
              ),
            ),
            const SizedBox(height: 10),
            TextFormField(
              controller: _precio,
              keyboardType: TextInputType.numberWithOptions(decimal: true),
              decoration: const InputDecoration(
                labelText: "Precio",
                icon: Icon(Icons.attach_money),
              ),
            ),
            const SizedBox(height: 10),
            TextField(
              controller: _marca,
              decoration: const InputDecoration(
                labelText: "Marca",
                icon: Icon(Icons.phone_android),
              ),
            ),
            const SizedBox(height: 10),
            TextField(
              controller: _stock,
              decoration: const InputDecoration(
                labelText: "Stock",
                icon: Icon(Icons.storage),
              ),
            ),
            const SizedBox(height: 10),
            DropdownButtonFormField<String>(
              value: _tipoSeleccionado,
              items: _tipo.map((categoria) {
                return DropdownMenuItem(
                  value: categoria,
                  child: Text(categoria),
                );
              }).toList(),
              onChanged: (value) {
                setState(() {
                  _tipoSeleccionado = value;
                });
              },
              decoration: const InputDecoration(
                labelText: 'Tipo',
                icon: Icon(Icons.category),
              ),
            ),
            const SizedBox(height: 10),
            SwitchListTile(
              title: const Text('¿Estado?'),
              value: _estado,
              onChanged: (value) {
                setState(() {
                  _estado = value;
                });
              },
              secondary: Icon(
                _estado ? Icons.check_circle : Icons.cancel,
                color: _estado ? Colors.green : Colors.red,
              ),
            ),
            const SizedBox(height: 10),
            ElevatedButton.icon(
              onPressed: () {
                if (_idSeleccionado == null) {
                  createProductos();
                } else {
                  updateProductos(_idSeleccionado!);
                }
              },
              icon: Icon(_idSeleccionado == null ? Icons.add : Icons.save),
              label: Text(
                _idSeleccionado == null
                    ? 'Agregar Producto'
                    : 'Actualizar Producto',
              ),
              style: ElevatedButton.styleFrom(
                backgroundColor: _idSeleccionado == null
                    ? Colors.green
                    : Colors.blue,
              ),
            ),
            const SizedBox(height: 20),
            const Divider(thickness: 1),
            const SizedBox(height: 10),
            const Text(
              'Lista de Productos',
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 10),
            StreamBuilder(
              stream: FirebaseFirestore.instance
                  .collection('productos_tecnologicos')
                  .snapshots(),
              builder: (context, snapshot) {
                if (!snapshot.hasData) {
                  return const Center(child: CircularProgressIndicator());
                }
                final docs = snapshot.data!.docs;
                if (docs.isEmpty) {
                  return const Padding(
                    padding: EdgeInsets.all(16),
                    child: Text('No hay productos registrados.'),
                  );
                }
                return ListView.builder(
                  shrinkWrap: true,
                  physics: const NeverScrollableScrollPhysics(),
                  itemCount: docs.length,
                  itemBuilder: (context, index) {
                    final producto = docs[index];
                    return Card(
                      elevation: 2,
                      margin: const EdgeInsets.symmetric(vertical: 6),
                      child: ListTile(
                        leading: const Icon(Icons.shopping_basket),
                        title: Text(producto['nombre']),
                        subtitle: Column(
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: [
                            Text('Precio: S/. ${producto['precio']}'),
                            Text('Porción: ${producto['marca']}'),
                            Text('Tipo: ${producto['tipo']}'),
                            Text('Stock: ${producto['stock']}'),
                            Text(
                              'Estado: ${producto['estado'] ? 'activo' : 'inactivo'}',
                            ),
                          ],
                        ),
                        trailing: Row(
                          mainAxisSize: MainAxisSize.min,
                          children: [
                            IconButton(
                              icon: const Icon(Icons.edit, color: Colors.blue),
                              onPressed: () {
                                setState(() {
                                  _idSeleccionado = producto.id;
                                  _nombre.text = producto['nombre'];
                                  _precio.text = producto['precio'].toString();
                                  _marca.text = producto['marca'];
                                  _stock.text = producto['stock'].toString();
                                  _tipoSeleccionado = producto['tipo'];
                                  _estado = producto['estado'];
                                });
                              },
                            ),
                            IconButton(
                              icon: const Icon(Icons.delete, color: Colors.red),
                              onPressed: () => deleteProductos(producto.id),
                            ),
                          ],
                        ),
                      ),
                    );
                  },
                );
              },
            ),
          ],
        ),
      ),
    );
  }
}
```

# Explicación Completa del CRUD en Tech Store

## ¿Qué es un CRUD?

**CRUD** es un acrónimo que representa las 4 operaciones básicas de persistencia de datos:
- **C**reate (Crear)
- **R**ead (Leer)
- **U**pdate (Actualizar)
- **D**elete (Eliminar)

Tu aplicación implementa un CRUD completo para gestionar productos tecnológicos usando Firebase Firestore.

## Estructura del Código CRUD

### 1. **CREATE (Crear) - `createProductos()`**

```dart
Future<void> createProductos() async {
  if (!_validarCampos()) return;
  final datos = {
    'nombre': _nombre.text,
    'precio': double.tryParse(_precio.text) ?? 0.0,
    'marca': _marca.text,
    'tipo': _tipoSeleccionado,
    'stock': int.tryParse(_stock.text) ?? 0,
    'estado': _estado,
  };
  try {
    await FirebaseFirestore.instance
        .collection('productos_tecnologicos')
        .add(datos); // ← MÉTODO ADD PARA CREAR
    limpiarFormulario();
  } catch (e) {
    print('Error al crear producto: $e');
  }
}
```

**Elementos clave:**
- **FirebaseFirestore.instance.collection('productos_tecnologicos').add(datos)**
- Se ejecuta cuando `_idSeleccionado == null`
- El botón cambia a "Agregar Producto" (color verde)

### 2. **READ (Leer) - `readProductos()` y StreamBuilder**

**Método para lectura única:**
```dart
Future<void> readProductos() async {
  try {
    final snapshot = await FirebaseFirestore.instance
        .collection('productos_tecnologicos')
        .get(); // ← MÉTODO GET PARA LEER
    setState(() {
      productos = snapshot.docs
          .map((doc) => {'id': doc.id, ...doc.data()})
          .toList();
    });
  } catch (e) {
    print('Error al leer productos: $e');
  }
}
```

**StreamBuilder para lectura en tiempo real:**
```dart
StreamBuilder(
  stream: FirebaseFirestore.instance
      .collection('productos_tecnologicos')
      .snapshots(), // ← STREAM EN TIEMPO REAL
  builder: (context, snapshot) {
    // Construye la lista automáticamente cuando hay cambios
  },
)
```

### 3. **UPDATE (Actualizar) - `updateProductos()`**

```dart
Future<void> updateProductos(String id) async {
  if (!_validarCampos()) return;
  final datos = {
    'nombre': _nombre.text,
    'precio': double.tryParse(_precio.text) ?? 0.0,
    'marca': _marca.text,
    'categoria': _tipoSeleccionado, // ← ERROR: debería ser 'tipo'
    'stock': int.tryParse(_stock.text) ?? 0,
    'estado': _estado,
  };
  try {
    await FirebaseFirestore.instance
        .collection('productos_tecnologicos')
        .doc(id) // ← ESPECIFICAR DOCUMENTO POR ID
        .update(datos); // ← MÉTODO UPDATE
    limpiarFormulario();
  } catch (e) {
    print('Error al actualizar productos: $e');
  }
}
```

**Nota:** Hay un error - usa 'categoria' en lugar de 'tipo'

### 4. **DELETE (Eliminar) - `deleteProductos()`**

```dart
Future<void> deleteProductos(String id) async {
  try {
    await FirebaseFirestore.instance
        .collection('productos_tecnologicos')
        .doc(id) // ← ESPECIFICAR DOCUMENTO
        .delete(); // ← MÉTODO DELETE
    await readProductos();
    limpiarFormulario();
  } catch (e) {
    print('Error al eliminar productos: $e');
  }
}
```

## Flujo de la Aplicación

### **Interfaz de Usuario (UI)**

**Formulario de entrada:**
- 4 TextFields (Nombre, Precio, Marca, Stock)
- DropdownButton (Tipo de producto)
- SwitchListTile (Estado activo/inactivo)
- Botón dinámico (Agregar/Actualizar)

**Lista de productos:**
- Muestra todos los productos en Cards
- Botones Editar (✏️) y Eliminar (🗑️) en cada item

### **Estados y Controladores**

```dart
// Controladores para los campos de texto
final TextEditingController _nombre = TextEditingController();
final TextEditingController _precio = TextEditingController();
// ... otros controllers

// Estado para saber si estamos editando
String? _idSeleccionado; // null = crear, tiene valor = editar
```

### **Flujo de Edición**

1. **Usuario hace clic en "Editar"** → `onPressed()` del IconButton de edición
2. **Se llena el formulario** con los datos del producto seleccionado
3. **`_idSeleccionado` se establece** con el ID del documento
4. **El botón cambia** a "Actualizar Producto" (color azul)
5. **Al guardar** se ejecuta `updateProductos()` en lugar de `createProductos()`

## Firebase Firestore Structure

```
productos_tecnologicos/ (colección)
  │
  ├── documento1 (ID automático)
  │   ├── nombre: "Teclado Mecánico"
  │   ├── precio: 150.0
  │   ├── marca: "Logitech"
  │   ├── tipo: "Accesorio"
  │   ├── stock: 25
  │   └── estado: true
  │
  ├── documento2 (ID automático)
  │   ├── nombre: "Monitor 24\""
  │   ├── precio: 800.0
  │   └── ... otros campos
```

## Validaciones y Utilidades

### **Validación de Campos - `_validarCampos()`**
- Verifica que todos los campos obligatorios estén llenos
- Valida que el precio sea un número válido y mayor a 0

### **Limpieza del Formulario - `limpiarFormulario()`**
- Limpia todos los campos
- Restablece `_idSeleccionado` a null
- Vuelve el botón a modo "Agregar"

## Errores a Corregir

1. **En `updateProductos()`**: Cambiar `'categoria'` por `'tipo'` para consistencia
2. **En el ListTile**: Cambiar `'Porción:'` por `'Marca:'`
3. **Falta refresh después de crear**: Agregar `readProductos()` después de crear

Esta aplicación es un excelente ejemplo de un CRUD completo con Flutter y Firebase, mostrando buenas prácticas de desarrollo y una interfaz de usuario intuitiva.

# Explicación Completa de la Lógica UI en Tech Store

## **Arquitectura General de la UI**

### **Estructura Widget Principal**
```dart
Scaffold
├── AppBar
└── SingleChildScrollView
    └── Column
        ├── Formulario (Inputs)
        └── Lista de Productos (StreamBuilder)
```

## **1. Gestión de Estado y Reactividad**

### **Controladores de Texto**
```dart
final TextEditingController _nombre = TextEditingController();
final TextEditingController _precio = TextEditingController();
final TextEditingController _marca = TextEditingController();
final TextEditingController _stock = TextEditingController();
```
**Función:** Mantener el estado de los campos de texto y sincronizarlos con la UI.

### **Variables de Estado**
```dart
String? _tipoSeleccionado;    // Dropdown seleccionado
bool _estado = true;          // Switch estado
String? _idSeleccionado;      // Modo Edición vs Creación
```
**Lógica:** Cada cambio en estos valores dispara `setState()` para reconstruir la UI.

## **2. Diseño del Formulario**

### **Organización Vertical**
```dart
Column(
  children: [
    TextField(_nombre),       // Nombre
    SizedBox(height: 10),     // Espaciado
    TextField(_precio),       // Precio
    // ... más campos
  ],
)
```

### **Campos de Entrada Específicos**

**TextField Básico:**
```dart
TextField(
  controller: _nombre,
  decoration: const InputDecoration(
    labelText: "Nombre del producto",
    icon: Icon(Icons.label),  // Icono identificador
  ),
)
```

**TextField Numérico:**
```dart
TextFormField(
  controller: _precio,
  keyboardType: TextInputType.numberWithOptions(decimal: true),
  decoration: const InputDecoration(
    labelText: "Precio",
    icon: Icon(Icons.attach_money),  // Icono temático
  ),
)
```

### **DropdownButtonFormField - Selección de Tipo**
```dart
DropdownButtonFormField<String>(
  value: _tipoSeleccionado,    // Valor actual seleccionado
  items: _tipo.map((categoria) {
    return DropdownMenuItem(
      value: categoria,        // Valor interno
      child: Text(categoria),  // Texto visible
    );
  }).toList(),
  onChanged: (value) {
    setState(() {
      _tipoSeleccionado = value;  // Actualizar estado
    });
  },
)
```

### **SwitchListTile - Estado Booleano**
```dart
SwitchListTile(
  title: const Text('¿Estado?'),
  value: _estado,
  onChanged: (value) {
    setState(() {
      _estado = value;        // Cambiar estado
    });
  },
  secondary: Icon(            // Icono dinámico
    _estado ? Icons.check_circle : Icons.cancel,
    color: _estado ? Colors.green : Colors.red,  // Color contextual
  ),
)
```

## **3. Botón Dinámico - Lógica de Modo Dual**

### **Renderizado Condicional**
```dart
ElevatedButton.icon(
  onPressed: () {
    if (_idSeleccionado == null) {    // Lógica de modo
      createProductos();              // Modo Crear
    } else {
      updateProductos(_idSeleccionado!); // Modo Actualizar
    }
  },
  icon: Icon(_idSeleccionado == null ? Icons.add : Icons.save),
  label: Text(
    _idSeleccionado == null 
        ? 'Agregar Producto' 
        : 'Actualizar Producto',
  ),
  style: ElevatedButton.styleFrom(
    backgroundColor: _idSeleccionado == null 
        ? Colors.green    // Verde para crear
        : Colors.blue,    // Azul para actualizar
  ),
)
```

## **4. Lista de Productos - StreamBuilder Reactivo**

### **Stream en Tiempo Real**
```dart
StreamBuilder(
  stream: FirebaseFirestore.instance
      .collection('productos_tecnologicos')
      .snapshots(),  // ← Stream automático
  builder: (context, snapshot) {
    // UI se reconstruye automáticamente con cada cambio en Firestore
  },
)
```

### **Estados del StreamBuilder**
```dart
builder: (context, snapshot) {
  if (!snapshot.hasData) {
    return const Center(child: CircularProgressIndicator());  // Cargando
  }
  final docs = snapshot.data!.docs;
  if (docs.isEmpty) {
    return const Text('No hay productos registrados.');  // Vacío
  }
  return ListView.builder(  // Lista con datos
    // ...
  );
}
```

## **5. Item de Lista - Card Interactiva**

### **Estructura del Card**
```dart
Card(
  elevation: 2,                    // Sombra suave
  margin: const EdgeInsets.symmetric(vertical: 6),
  child: ListTile(
    leading: const Icon(Icons.shopping_basket),  // Icono constante
    title: Text(producto['nombre']),             // Título principal
    subtitle: Column(                            // Múltiples líneas
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Text('Precio: S/. ${producto['precio']}'),
        Text('Marca: ${producto['marca']}'),
        // ... más campos
      ],
    ),
    trailing: Row(  // Botones de acción
      mainAxisSize: MainAxisSize.min,
      children: [
        IconButton(  // Editar
          icon: const Icon(Icons.edit, color: Colors.blue),
          onPressed: () => _cargarFormularioEdicion(producto),
        ),
        IconButton(  // Eliminar
          icon: const Icon(Icons.delete, color: Colors.red),
          onPressed: () => deleteProductos(producto.id),
        ),
      ],
    ),
  ),
)
```

## **6. Lógica de Edición - Cargar Formulario**

### **Función de Carga para Edición**
```dart
onPressed: () {
  setState(() {
    _idSeleccionado = producto.id;                    // Activar modo edición
    _nombre.text = producto['nombre'];               // Llenar nombre
    _precio.text = producto['precio'].toString();    // Llenar precio
    _marca.text = producto['marca'];                 // Llenar marca
    _stock.text = producto['stock'].toString();      // Llenar stock
    _tipoSeleccionado = producto['tipo'];            // Seleccionar tipo
    _estado = producto['estado'];                    // Establecer estado
  });
}
```

## **7. Patrones de Diseño UI Utilizados**

### **Separación de Responsabilidades**
- **Formulario superior**: Entrada de datos
- **Lista inferior**: Visualización de datos
- **Divider**: Separación visual clara

### **Feedback Visual**
```dart
// Colores semánticos
Colors.green  → Acción positiva (Crear)
Colors.blue   → Acción neutral (Actualizar)  
Colors.red    → Acción peligrosa (Eliminar)

// Iconos significativos
Icons.add → Crear nuevo
Icons.save → Guardar cambios
Icons.edit → Modificar
Icons.delete → Eliminar
```

### **Diseño Responsivo**
```dart
SingleChildScrollView(  // Permite scroll en pantallas pequeñas
  padding: const EdgeInsets.all(16.0),  // Espaciado consistente
  child: Column(
    children: [
      // Campos apilados verticalmente
    ],
  ),
)
```

### **Optimizaciones de Rendimiento**
```dart
ListView.builder(
  shrinkWrap: true,  // Ocupa solo espacio necesario
  physics: const NeverScrollableScrollPhysics(),  // Scroll independiente
  itemCount: docs.length,
  itemBuilder: (context, index) {
    // Construye items bajo demanda
  },
)
```

## **8. Flujo Completo de Usuario**

1. **Usuario ingresa datos** → Campos se actualizan vía controllers
2. **Selecciona tipo** → Dropdown actualiza estado
3. **Cambia estado** → Switch cambia visualmente
4. **Presiona botón** → Lógica determina crear/actualizar
5. **En lista** → 
   - **Editar**: Carga formulario + cambia botón
   - **Eliminar**: Elimina + actualiza lista automáticamente
6. **StreamBuilder** → Refleja cambios en tiempo real

## **9. Principios UI/UX Implementados**

- **Consistencia**: Mismos colores e iconos para mismas acciones
- **Feedback inmediato**: Cambios visuales al instante
- **Prevención de errores**: Validación antes de operaciones
- **Eficiencia**: Formulario dual (crear/editar)
- **Accesibilidad**: Iconos + texto, contraste adecuado

Esta arquitectura UI permite una experiencia de usuario fluida e intuitiva, donde cada elemento visual está directamente conectado con la lógica de negocio subyacente.