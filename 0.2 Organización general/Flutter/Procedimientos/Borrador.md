
## Empleados Screen
```dart
import 'package:flutter/material.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import 'empleados_detalle_screen.dart';
//import 'empleadosform_screen.dart';
//import 'empleadoseditar_screen.dart';

/// Pantalla principal para la gestión de empleados de clínica dental
///
/// Permite visualizar, crear, editar y eliminar empleados
/// Integra con Firebase Firestore para el almacenamiento de datos
class EmpleadosScreen extends StatefulWidget {
  const EmpleadosScreen({super.key});

  @override
  State<EmpleadosScreen> createState() => _EmpleadosScreenState();
}

/// Estado de la pantalla de empleados
class _EmpleadosScreenState extends State<EmpleadosScreen> {
  // ========== VARIABLES DE ESTADO ==========

  /// Lista de empleados obtenidos de Firestore
  List<Map<String, dynamic>> _empleados = [];

  /// Indica si los datos están siendo cargados
  bool _isLoading = true;

  /// Filtro de tipo de empleado actual
  String _filtroTipo = 'todos';

  /// Referencia a la colección de empleados en Firestore
  static const String _collectionName = 'personal';

  /// Mapa de nombres descriptivos para los tipos de empleado
  static const Map<String, String> _tipoEmpleadoLabels = {
    'odontologo': 'Odontólogo',
    'asistente_dental': 'Asistente Dental',
    'recepcionista': 'Recepcionista',
    'higienista': 'Higienista Dental',
    'administrador': 'Administrador',
  };

  /// Opciones de filtro por tipo de empleado
  static const List<Map<String, String>> _filtrosTipo = [
    {'value': 'todos', 'label': 'Todos'},
    {'value': 'odontologo', 'label': 'Odontólogos'},
    {'value': 'asistente_dental', 'label': 'Asistentes'},
    {'value': 'recepcionista', 'label': 'Recepcionistas'},
    {'value': 'higienista', 'label': 'Higienistas'},
    {'value': 'administrador', 'label': 'Administradores'},
  ];

  // ========== CICLO DE VIDA DEL WIDGET ==========

  @override
  void initState() {
    super.initState();
    _cargarEmpleados();
  }

  // ========== MÉTODOS DE DATOS ==========

  /// Carga la lista de empleados desde Firestore
  Future<void> _cargarEmpleados() async {
    try {
      setState(() => _isLoading = true);

      final snapshot = await FirebaseFirestore.instance
          .collection(_collectionName)
          .orderBy('fecha_contratacion', descending: true)
          .get();

      final List<Map<String, dynamic>> empleadosList = snapshot.docs
          .map(
            (DocumentSnapshot doc) => {
              'id': doc.id,
              ...doc.data() as Map<String, dynamic>,
            },
          )
          .toList();

      if (mounted) {
        setState(() {
          _empleados = empleadosList;
          _isLoading = false;
        });
      }
    } catch (e) {
      if (mounted) {
        setState(() => _isLoading = false);
        _mostrarMensajeError('Error al cargar empleados: $e');
      }
    }
  }

  /// Elimina un empleado de Firestore
  Future<void> _eliminarEmpleado(String empleadoId) async {
    try {
      await FirebaseFirestore.instance
          .collection(_collectionName)
          .doc(empleadoId)
          .delete();

      _mostrarMensajeExito('Empleado eliminado correctamente');
      _cargarEmpleados();
    } catch (e) {
      _mostrarMensajeError('Error al eliminar empleado: $e');
    }
  }

  /// Filtra la lista de empleados según el tipo seleccionado
  List<Map<String, dynamic>> _filtrarEmpleados() {
    if (_filtroTipo == 'todos') {
      return _empleados;
    }

    return _empleados
        .where((empleado) => empleado['tipo_empleado_id'] == _filtroTipo)
        .toList();
  }

  /// Calcula la edad a partir de la fecha de nacimiento
  int _calcularEdad(DateTime fechaNacimiento) {
    final ahora = DateTime.now();
    int edad = ahora.year - fechaNacimiento.year;
    if (ahora.month < fechaNacimiento.month ||
        (ahora.month == fechaNacimiento.month &&
            ahora.day < fechaNacimiento.day)) {
      edad--;
    }
    return edad;
  }

  // ========== MÉTODOS DE UI ==========

  @override
  Widget build(BuildContext context) {
    final empleadosFiltrados = _filtrarEmpleados();

    return Scaffold(
      extendBodyBehindAppBar: false, // Asegúrate de que esté en false
      backgroundColor: const Color(0xFFF7F7F7),
      appBar: _construirAppBar(),
      body: _buildBody(empleadosFiltrados),
      floatingActionButton: _buildFloatingActionButton(),
    );
  }

  /// Construye la barra de aplicación
  PreferredSizeWidget _construirAppBar() {
    return PreferredSize(
      preferredSize: const Size.fromHeight(56),
      child: Container(
        decoration: const BoxDecoration(
          color: Colors.white, // Color sólido
          // Puedes agregar un border o boxShadow si quieres una línea o sombra
          boxShadow: [
            BoxShadow(
              color: Color(0x11000000),
              blurRadius: 4,
              offset: Offset(0, 2),
            ),
          ],
        ),
        child: SafeArea(
          bottom: false,
          child: Row(
            children: [
              // Tu logo o icono
              Padding(
                padding: const EdgeInsets.symmetric(horizontal: 16),
                child: Image.asset('assets/img/dentlink_logo.png', height: 40),
              ),
              const Text(
                'DentLink',
                style: TextStyle(
                  color: Colors.black,
                  fontSize: 20,
                  fontWeight: FontWeight.w600,
                  letterSpacing: 0.5,
                ),
              ),
              // ...otros widgets si necesitas
            ],
          ),
        ),
      ),
    );
  }

  /// Construye el cuerpo principal de la pantalla
  Widget _buildBody(List<Map<String, dynamic>> empleadosFiltrados) {
    return Column(
      children: [
        // Filtros
        _construirFiltros(),

        // Lista de empleados
        Expanded(child: _buildListaEmpleados(empleadosFiltrados)),
      ],
    );
  }

  /// Construye los filtros por tipo de empleado
  Widget _construirFiltros() {
    return Container(
      padding: const EdgeInsets.all(16),
      decoration: BoxDecoration(
        color: const Color(0xFFF7F7F7),
        border: Border(bottom: BorderSide(color: const Color(0xFFF7F7F7))),
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          const Text(
            'Filtrar por tipo de empleado',
            style: TextStyle(
              fontSize: 12,
              color: Colors.grey,
              fontWeight: FontWeight.w500,
            ),
          ),
          const SizedBox(height: 8),
          DropdownButtonFormField<String>(
            value: _filtroTipo,
            decoration: const InputDecoration(
              isDense: true,
              contentPadding: EdgeInsets.symmetric(
                horizontal: 12,
                vertical: 12,
              ),
              border: OutlineInputBorder(),
              filled: true,
              fillColor: Colors.white,
            ),
            items: _filtrosTipo.map((filtro) {
              return DropdownMenuItem(
                value: filtro['value'],
                child: Text(filtro['label']!),
              );
            }).toList(),
            onChanged: (String? nuevoValor) {
              if (nuevoValor != null) {
                setState(() {
                  _filtroTipo = nuevoValor;
                });
              }
            },
          ),
        ],
      ),
    );
  }

  /// Construye la lista de empleados
  Widget _buildListaEmpleados(List<Map<String, dynamic>> empleadosFiltrados) {
    if (_isLoading) {
      return _buildLoadingWidget();
    }

    if (empleadosFiltrados.isEmpty) {
      return _buildEmptyStateWidget();
    }

    return RefreshIndicator(
      onRefresh: _cargarEmpleados,
      child: ListView.builder(
        padding: const EdgeInsets.symmetric(vertical: 8),
        itemCount: empleadosFiltrados.length,
        itemBuilder: (context, index) {
          final empleado = empleadosFiltrados[index];
          return _construirEmpleadoCard(empleado);
        },
      ),
    );
  }

  /// Widget de carga
  Widget _buildLoadingWidget() {
    return const Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          CircularProgressIndicator(),
          SizedBox(height: 16),
          Text(
            'Cargando empleados...',
            style: TextStyle(fontSize: 16, color: Colors.grey),
          ),
        ],
      ),
    );
  }

  /// Widget para estado vacío
  Widget _buildEmptyStateWidget() {
    return Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Icon(
            Icons.medical_services_outlined,
            size: 64,
            color: Colors.grey[400],
          ),
          const SizedBox(height: 16),
          Text(
            'No hay empleados registrados',
            style: TextStyle(
              fontSize: 18,
              color: Colors.grey[600],
              fontWeight: FontWeight.w500,
            ),
          ),
          const SizedBox(height: 8),
          Text(
            'Presiona el botón + para agregar el primer empleado',
            style: TextStyle(fontSize: 14, color: Colors.grey[500]),
            textAlign: TextAlign.center,
          ),
        ],
      ),
    );
  }

  /// Construye el botón flotante para agregar empleado
  Widget _buildFloatingActionButton() {
    return FloatingActionButton(
      onPressed: () {}, //_navegarACrearEmpleado,
      tooltip: 'Agregar empleado',
      child: const Icon(Icons.person_add),
    );
  }

  Widget _construirEmpleadoCard(Map<String, dynamic> empleado) {
    final String tipoEmpleado = empleado['tipo_empleado_id'] ?? 'Sin tipo';
    final bool isActive = empleado['activo'] ?? true;

    return Card(
      color: Colors.white,
      margin: const EdgeInsets.symmetric(horizontal: 12, vertical: 4),
      elevation: 2,
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8)),
      child: Padding(
        padding: const EdgeInsets.all(16),
        child: Row(
          children: [
            // Avatar/Icono del empleado
            _buildAvatarEmpleado(empleado, tipoEmpleado),

            const SizedBox(width: 12),

            // Información del empleado - MODIFICADO
            Expanded(
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  // Nombre completo (primer nombre + primer apellido)
                  Text(
                    _obtenerNombreCompletoCorto(empleado),
                    style: TextStyle(
                      fontSize: 16,
                      fontWeight: FontWeight.w600,
                      color: Colors.black,
                    ),
                  ),

                  const SizedBox(height: 4),

                  // Tipo de empleado
                  Row(
                    children: [
                      Icon(
                        Icons.person_outline,
                        size: 16,
                        color: Colors.grey[700],
                      ),
                      Text(
                        _capitalizeFirst(tipoEmpleado),
                        style: TextStyle(
                          fontSize: 14,
                          fontWeight: FontWeight.w400,
                          color: Colors.grey[700],
                        ),
                      ),
                    ],
                  ),

                  const SizedBox(height: 4),

                  // Estado activo/inactivo
                  Row(
                    children: [
                      Container(
                        width: 8,
                        height: 8,
                        decoration: BoxDecoration(
                          color: isActive ? Colors.green : Colors.red,
                          shape: BoxShape.circle,
                        ),
                      ),
                      const SizedBox(width: 6),
                      Text(
                        isActive ? 'Activo' : 'Inactivo',
                        style: TextStyle(
                          fontSize: 12,
                          fontWeight: FontWeight.w400,
                          color: isActive ? Colors.green : Colors.red,
                        ),
                      ),
                    ],
                  ),
                ],
              ),
            ),

            const SizedBox(width: 12),

            // Acciones
            _buildAccionesColumn(empleado),
          ],
        ),
      ),
    );
  }

  /// Construye el avatar/icono del empleado
  Widget _buildAvatarEmpleado(
    Map<String, dynamic> empleado,
    String tipoEmpleado,
  ) {
    return Container(
      width: 50,
      height: 50,
      decoration: BoxDecoration(
        color: _getColorPorTipo(tipoEmpleado),
        shape: BoxShape.circle,
      ),
      child: Icon(
        _getIconoPorTipo(tipoEmpleado),
        color: Colors.white,
        size: 24,
      ),
    );
  }

  /// Construye la información del empleado
  Widget _buildEmpleadoInfo(
    Map<String, dynamic> empleado,
    String tipoEmpleado,
    String fechaContratacion,
    String fechaNacimiento,
    int edad,
  ) {
    final String nombreCompleto =
        '${empleado['nombres'] ?? ''} ${empleado['apellido_paterno'] ?? ''} ${empleado['apellido_materno'] ?? ''}'
            .trim();

    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        // Nombre completo
        Text(
          nombreCompleto.isEmpty ? 'Sin nombre' : nombreCompleto,
          style: const TextStyle(
            fontSize: 16,
            fontWeight: FontWeight.bold,
            color: Colors.black87,
          ),
          maxLines: 2,
          overflow: TextOverflow.ellipsis,
        ),

        const SizedBox(height: 6),

        // DNI y Edad
        Row(
          children: [
            Text(
              'DNI: ${empleado['dni_empleado'] ?? 'No especificado'}',
              style: TextStyle(
                fontSize: 14,
                color: Colors.grey[700],
                fontWeight: FontWeight.w500,
              ),
            ),
            const SizedBox(width: 12),
            Text(
              'Edad: $edad años',
              style: TextStyle(fontSize: 14, color: Colors.grey[700]),
            ),
          ],
        ),

        const SizedBox(height: 4),

        // Tipo de empleado
        Row(
          children: [
            Icon(
              _getIconoPorTipo(tipoEmpleado),
              size: 14,
              color: Colors.grey[600],
            ),
            const SizedBox(width: 4),
            Text(
              _tipoEmpleadoLabels[tipoEmpleado] ?? tipoEmpleado,
              style: TextStyle(
                fontSize: 13,
                color: Colors.grey[600],
                fontWeight: FontWeight.w500,
              ),
            ),
          ],
        ),

        const SizedBox(height: 4),

        // Género
        Text(
          'Género: ${_formatearGenero(empleado['genero'])}',
          style: const TextStyle(fontSize: 12, color: Colors.grey),
        ),

        const SizedBox(height: 4),

        // Información de contacto
        Row(
          children: [
            const Icon(Icons.phone, size: 12, color: Colors.grey),
            const SizedBox(width: 4),
            Expanded(
              child: Text(
                empleado['numero_telefonico'] ?? 'Sin teléfono',
                style: const TextStyle(fontSize: 12, color: Colors.grey),
                maxLines: 1,
                overflow: TextOverflow.ellipsis,
              ),
            ),
          ],
        ),

        // Fecha de contratación
        Row(
          children: [
            const Icon(Icons.calendar_today, size: 12, color: Colors.grey),
            const SizedBox(width: 4),
            Text(
              'Contratación: $fechaContratacion',
              style: const TextStyle(fontSize: 12, color: Colors.grey),
            ),
          ],
        ),

        // Salario
        if (empleado['salario'] != null) ...[
          const SizedBox(height: 4),
          Text(
            'Salario: S/. ${empleado['salario'].toStringAsFixed(2)}',
            style: const TextStyle(
              fontSize: 12,
              color: Colors.green,
              fontWeight: FontWeight.w600,
            ),
          ),
        ],
      ],
    );
  }

  /// Construye la columna de acciones (editar y eliminar)
  Widget _buildAccionesColumn(Map<String, dynamic> empleado) {
    return Column(
      mainAxisSize: MainAxisSize.min,

      children: [
        _construirBotonDetalle(empleado),
        //_buildBotonEditar(empleado),
        //const SizedBox(height: 8),
        //_buildBotonEliminar(empleado),
      ],
    );
  }

  Widget _construirBotonDetalle(Map<String, dynamic> empleado) {
    return IconButton(
      onPressed: () {
        print('🚀 Intentando navegar...');

        try {
          Navigator.push(
            context,
            MaterialPageRoute(
              builder: (context) => EmpleadosDetalle(empleado: empleado),
            ),
          );
          print('✅ Navegación exitosa');
        } catch (e) {
          print('❌ ERROR: $e');
          // Fallback seguro
          Navigator.push(
            context,
            MaterialPageRoute(
              builder: (context) => Scaffold(
                appBar: AppBar(title: const Text('Error - Usando fallback')),
                body: const Center(
                  child: Text('Hubo un error, pero esto es seguro'),
                ),
              ),
            ),
          );
        }
      },
      icon: const Icon(Icons.chevron_right, color: Colors.grey, size: 26),
    );
  }

  /// Construye el botón de editar
  Widget _buildBotonEditar(Map<String, dynamic> empleado) {
    return IconButton(
      onPressed: () => {}, //_navegarAEditarEmpleado(empleado),
      icon: Icon(Icons.edit_outlined, color: Colors.blue[600], size: 20),
      padding: const EdgeInsets.all(8),
      constraints: const BoxConstraints(minWidth: 40, minHeight: 40),
      tooltip: 'Editar empleado',
      style: IconButton.styleFrom(
        backgroundColor: Colors.blue[50],
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8)),
      ),
    );
  }

  /// Construye el botón de eliminar
  Widget _buildBotonEliminar(Map<String, dynamic> empleado) {
    return IconButton(
      onPressed: () => _confirmarEliminacion(empleado),
      icon: const Icon(Icons.delete_outline, color: Colors.red, size: 20),
      padding: const EdgeInsets.all(8),
      constraints: const BoxConstraints(minWidth: 40, minHeight: 40),
      tooltip: 'Eliminar empleado',
      style: IconButton.styleFrom(
        backgroundColor: Colors.red[50],
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8)),
      ),
    );
  }

  // ========== MÉTODOS DE UTILIDAD ==========

  /// Obtiene el color correspondiente al tipo de empleado
  Color _getColorPorTipo(String tipo) {
    switch (tipo) {
      case 'odontologo':
        return Colors.blue;
      case 'asistente_dental':
        return Colors.green;
      case 'recepcionista':
        return Colors.orange;
      case 'higienista':
        return Colors.purple;
      case 'administrador':
        return Colors.red;
      default:
        return Colors.grey;
    }
  }

  /// Obtiene el icono correspondiente al tipo de empleado
  IconData _getIconoPorTipo(String tipo) {
    switch (tipo) {
      case 'odontologo':
        return Icons.medical_services;
      case 'asistente_dental':
        return Icons.assistant;
      case 'recepcionista':
        return Icons.desk;
      case 'higienista':
        return Icons.clean_hands;
      case 'administrador':
        return Icons.admin_panel_settings;
      default:
        return Icons.person;
    }
  }

  String _capitalizeFirst(String text) {
    if (text.isEmpty) return text;
    return text[0].toUpperCase() + text.substring(1).toLowerCase();
  }

  // Método auxiliar para obtener nombre corto (primer nombre + primer apellido)
  String _obtenerNombreCompletoCorto(Map<String, dynamic> empleado) {
    final String nombreCompleto =
        empleado['nombre_completo'] ??
        '${empleado['nombres']} ${empleado['apellido_paterno']}' ??
        'Nombre no disponible';

    // Dividir el nombre completo en partes
    final partesNombre = nombreCompleto.split(' ');

    // Tomar primer nombre y primer apellido
    if (partesNombre.length >= 2) {
      return '${partesNombre[0]} ${partesNombre[1]}';
    } else {
      return partesNombre[0]; // Si solo tiene un nombre
    }
  }

  /// Formatea una fecha Timestamp para mostrar al usuario
  String _formatearFecha(dynamic fecha) {
    try {
      if (fecha == null) return 'No disponible';

      DateTime fechaDateTime;
      if (fecha is Timestamp) {
        fechaDateTime = fecha.toDate();
      } else if (fecha is String) {
        fechaDateTime = DateTime.parse(fecha);
      } else {
        return 'Formato inválido';
      }

      return '${fechaDateTime.day.toString().padLeft(2, '0')}/${fechaDateTime.month.toString().padLeft(2, '0')}/${fechaDateTime.year}';
    } catch (e) {
      return 'Fecha no disponible';
    }
  }

  /// Formatea el género para mostrar
  String _formatearGenero(String? genero) {
    switch (genero?.toLowerCase()) {
      case 'masculino':
        return 'Masculino';
      case 'femenino':
        return 'Femenino';
      case 'otro':
        return 'Otro';
      default:
        return 'No especificado';
    }
  }

  // ========== MÉTODOS DE NAVEGACIÓN ==========
  /*
  /// Navega a la pantalla de creación de empleado
  Future<void> _navegarACrearEmpleado() async {
    final result = await Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => const EmpleadosFormScreen()),
    );
    
    if (result == true) {
      _cargarEmpleados();
    }
  } 

  /// Navega a la pantalla de edición de empleado
  Future<void> _navegarAEditarEmpleado(Map<String, dynamic> empleado) async {
    final result = await Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => EmpleadoEditarScreen(empleadoToEdit: empleado),
      ),
    );
    
    if (result == true) {
      _cargarEmpleados();
    }
  } */

  // ========== MÉTODOS DE DIÁLOGOS Y MENSAJES ==========

  /// Confirma la eliminación de un empleado
  Future<void> _confirmarEliminacion(Map<String, dynamic> empleado) async {
    final String nombreCompleto =
        '${empleado['nombres'] ?? ''} ${empleado['apellido_paterno'] ?? ''}'
            .trim();

    final bool? confirmar = await showDialog<bool>(
      context: context,
      barrierDismissible: false,
      builder: (BuildContext context) {
        return AlertDialog(
          shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.circular(12),
          ),
          title: Row(
            children: [
              Icon(
                Icons.warning_amber_rounded,
                color: Colors.orange[600],
                size: 28,
              ),
              const SizedBox(width: 12),
              const Text(
                'Confirmar Eliminación',
                style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
              ),
            ],
          ),
          content: Padding(
            padding: const EdgeInsets.symmetric(vertical: 8),
            child: RichText(
              text: TextSpan(
                style: TextStyle(
                  fontSize: 16,
                  color: Colors.grey[800],
                  height: 1.4,
                ),
                children: [
                  const TextSpan(
                    text: '¿Estás seguro de que deseas eliminar al empleado ',
                  ),
                  TextSpan(
                    text: '"$nombreCompleto"',
                    style: const TextStyle(
                      fontWeight: FontWeight.bold,
                      color: Colors.black87,
                    ),
                  ),
                  const TextSpan(
                    text: '?\n\nEsta acción no se puede deshacer.',
                  ),
                ],
              ),
            ),
          ),
          actions: [
            TextButton(
              onPressed: () => Navigator.of(context).pop(false),
              child: Text(
                'Cancelar',
                style: TextStyle(
                  color: Colors.grey[600],
                  fontWeight: FontWeight.w600,
                ),
              ),
            ),
            const SizedBox(width: 8),
            ElevatedButton(
              onPressed: () => Navigator.of(context).pop(true),
              style: ElevatedButton.styleFrom(
                backgroundColor: Colors.red,
                foregroundColor: Colors.white,
                shape: RoundedRectangleBorder(
                  borderRadius: BorderRadius.circular(8),
                ),
              ),
              child: const Text(
                'Eliminar',
                style: TextStyle(fontWeight: FontWeight.w600),
              ),
            ),
          ],
        );
      },
    );

    if (confirmar == true) {
      _eliminarEmpleado(empleado['id']);
    }
  }

  /// Muestra un mensaje de error
  void _mostrarMensajeError(String mensaje) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(
        content: Text(mensaje),
        backgroundColor: Colors.red,
        duration: const Duration(seconds: 4),
        behavior: SnackBarBehavior.floating,
        action: SnackBarAction(
          label: 'Reintentar',
          textColor: Colors.white,
          onPressed: _cargarEmpleados,
        ),
      ),
    );
  }

  /// Muestra un mensaje de éxito
  void _mostrarMensajeExito(String mensaje) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(
        content: Text(mensaje),
        backgroundColor: Colors.green,
        duration: const Duration(seconds: 2),
        behavior: SnackBarBehavior.floating,
      ),
    );
  }
}

// Widget temporal para testing - AGREGA ESTO AL FINAL DEL ARCHIVO
class EmpleadosDetalle extends StatelessWidget {
  final Map<String, dynamic> empleado;

  const EmpleadosDetalle({super.key, required this.empleado});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Detalle Empleado'),
        backgroundColor: Colors.blue,
      ),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              'Nombre: ${empleado['nombres']} ${empleado['apellido_paterno']}',
              style: const TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 10),
            Text('DNI: ${empleado['dni_empleado']}'),
            const SizedBox(height: 10),
            Text('Teléfono: ${empleado['numero_telefonico']}'),
            const SizedBox(height: 20),
            ElevatedButton(
              onPressed: () => Navigator.pop(context),
              child: const Text('Volver'),
            ),
          ],
        ),
      ),
    );
  }
}

```

## main.dart
```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import 'package:proto_appdental_v02/calendario_screen.dart'; // Solo una vez
import 'clientsscreen.dart';
import 'homescreen.dart';
import 'empleados_screen.dart';
import 'pagos_screen.dart';
// Removida la importación duplicada de calendario_screen.dart

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
      theme: ThemeData(
        useMaterial3: true,
        colorScheme: ColorScheme.fromSeed(
          seedColor: Colors.white,
          brightness: Brightness.light,
        ),

        // Personalización de texto
        textTheme: TextTheme(
          titleLarge: const TextStyle(
            fontSize: 16,
            fontWeight: FontWeight.w600,
            color: Colors.black,
          ),
          bodyMedium: TextStyle(
            fontSize: 14,
            fontWeight: FontWeight.w400,
            color: Colors.grey[700],
          ),
          labelSmall: TextStyle(
            fontSize: 12,
            fontWeight: FontWeight.w400,
            color: Colors.grey[600],
          ),
        ),
      ),

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
    CalendarioScreen(),
    EmpleadosScreen(),
    PagosScreen(),
  ];

  void _onItemSelected(int index) {
    setState(() {
      _select = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: IndexedStack(index: _select, children: _pantallas),
      bottomNavigationBar: _buildCustomBottomNav(),
      floatingActionButton: _buildFloatingActionButton(),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked,
    );
  }

  /// Bottom Navigation Bar personalizado
  Widget _buildCustomBottomNav() {
    return Container(
      height: 70, // Altura fija para mejor control
      decoration: BoxDecoration(
        color: Colors.white,
        boxShadow: [
          BoxShadow(
            color: Colors.black.withOpacity(0.1),
            blurRadius: 8,
            offset: const Offset(0, -2),
          ),
        ],
      ),
      child: SafeArea(
        // ✅ AGREGAR ESTO
        child: Row(
          children: [
            // Primeros 2 items (Principal y Clientes)
            _buildNavItem(icon: Icons.home, label: "Principal", index: 0),
            _buildNavItem(icon: Icons.people, label: "Clientes", index: 1),

            // Espacio para el FAB central (importante)
            const SizedBox(width: 40),

            // Últimos 2 items (Empleados y Pagos)
            _buildNavItem(icon: Icons.person, label: "Empleados", index: 3),
            _buildNavItem(icon: Icons.payments, label: "Pagos", index: 4),
          ],
        ),
      ),
    );
  }

  /// Item individual de navegación
  Widget _buildNavItem({
    required IconData icon,
    required String label,
    required int index,
  }) {
    final bool isSelected = _select == index;

    return Expanded(
      child: Material(
        color: Colors.transparent,
        child: InkWell(
          onTap: () => _onItemSelected(index),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Icon(
                icon,
                color: isSelected ? Colors.blue : Colors.grey,
                size: 24,
              ),
              const SizedBox(height: 4),
              Text(
                label,
                style: TextStyle(
                  fontSize: 12,
                  color: isSelected ? Colors.blue : Colors.grey,
                  fontWeight: isSelected ? FontWeight.w600 : FontWeight.w400,
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }

  /// Botón flotante central (Calendario)
  Widget _buildFloatingActionButton() {
    return FloatingActionButton(
      onPressed: () => _onItemSelected(2),
      backgroundColor: Colors.blue,
      foregroundColor: Colors.white,
      elevation: 4,
      child: const Icon(Icons.calendar_today, size: 24),
    );
  }
}
```

## Empleados Editar Screen

```Dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:cloud_firestore/cloud_firestore.dart';

/// Pantalla para editar empleados existentes
///
/// Proporciona un formulario completo para modificar los datos de un empleado
/// existente, incluyendo funcionalidades de actualización, eliminación y
/// restauración de cambios.
///
/// Características:
/// - Carga automática de datos existentes
/// - Validación integral de campos
/// - Confirmaciones para acciones críticas
/// - Historial de cambios con timestamps
/// - Mensajes de confirmación y error
/// - Interfaz intuitiva con acciones rápidas
class EmpleadoEditarScreen extends StatefulWidget {
  /// Datos del empleado a editar
  final Map<String, dynamic> empleadoToEdit;

  /// Constructor de la pantalla de edición
  ///
  /// [empleadoToEdit] Mapa con los datos del empleado existente a editar
  const EmpleadoEditarScreen({super.key, required this.empleadoToEdit});

  @override
  State<EmpleadoEditarScreen> createState() => _EmpleadoEditarScreenState();
}

/// Estado de la pantalla de edición de empleados
///
/// Maneja todo el ciclo de vida del formulario de edición, incluyendo
/// la carga de datos, validaciones, y operaciones de base de datos.
class _EmpleadoEditarScreenState extends State<EmpleadoEditarScreen> {
  // ========== CONSTANTES ==========

  /// Nombre de la colección en Firebase Firestore
  static const String _nombreColeccion = 'empleados';

  /// Áreas disponibles para los empleados
  static const List<String> _areasDisponibles = [
    'cocina',
    'atencion',
    'delivery',
    'administracion',
  ];

  /// Mapa de nombres descriptivos para las áreas
  static const Map<String, String> _areaLabels = {
    'cocina': 'Cocina',
    'atencion': 'Atención al Cliente',
    'delivery': 'Delivery',
    'administracion': 'Administración',
  };

  /// Estados disponibles para los empleados
  static const List<String> _estadosDisponibles = ['activo', 'inactivo'];

  // ========== CONTROLADORES Y CLAVES ==========

  /// Clave global para validar el formulario
  final GlobalKey<FormState> _claveFormulario = GlobalKey<FormState>();

  /// Controlador para el campo de nombre completo
  final TextEditingController _controladorNombreCompleto =
      TextEditingController();

  /// Controlador para el campo de DNI
  final TextEditingController _controladorDNI = TextEditingController();

  /// Controlador para el campo de cargo
  final TextEditingController _controladorCargo = TextEditingController();

  /// Controlador para el campo de fecha de ingreso
  final TextEditingController _controladorFechaIngreso =
      TextEditingController();

  // ========== VARIABLES DE ESTADO ==========

  /// Área seleccionada actualmente
  String _areaSeleccionada = 'cocina';

  /// Estado seleccionado actualmente
  String _estadoSeleccionado = 'activo';

  /// Fecha de ingreso seleccionada
  DateTime? _fechaIngreso;

  // ========== MÉTODOS DEL CICLO DE VIDA ==========

  @override
  void initState() {
    super.initState();
    _cargarDatosEmpleado();
  }

  @override
  void dispose() {
    // Liberar recursos de los controladores
    _controladorNombreCompleto.dispose();
    _controladorDNI.dispose();
    _controladorCargo.dispose();
    _controladorFechaIngreso.dispose();
    super.dispose();
  }

  // ========== MÉTODOS DE INICIALIZACIÓN ==========

  /// Carga los datos del empleado existente en los controladores del formulario
  ///
  /// Inicializa todos los campos del formulario con los valores actuales
  /// del empleado que se está editando.
  void _cargarDatosEmpleado() {
    final Map<String, dynamic> datosActuales = widget.empleadoToEdit;

    // Cargar datos en los controladores de texto
    _controladorNombreCompleto.text =
        datosActuales['nombreCompleto']?.toString() ?? '';
    _controladorDNI.text = datosActuales['dni']?.toString() ?? '';
    _controladorCargo.text = datosActuales['cargo']?.toString() ?? '';

    // Configurar estado inicial
    _areaSeleccionada = datosActuales['area']?.toString() ?? 'cocina';
    _estadoSeleccionado = datosActuales['estado']?.toString() ?? 'activo';

    // Configurar fecha de ingreso
    if (datosActuales['fechaIngreso'] != null) {
      try {
        _fechaIngreso = DateTime.parse(datosActuales['fechaIngreso']);
        _controladorFechaIngreso.text = _formatearFechaParaInput(
          _fechaIngreso!,
        );
      } catch (e) {
        _fechaIngreso = DateTime.now();
        _controladorFechaIngreso.text = _formatearFechaParaInput(
          _fechaIngreso!,
        );
      }
    } else {
      _fechaIngreso = DateTime.now();
      _controladorFechaIngreso.text = _formatearFechaParaInput(_fechaIngreso!);
    }

    // Verificar que el área cargada sea válida
    if (!_areasDisponibles.contains(_areaSeleccionada)) {
      _areaSeleccionada = _areasDisponibles.first;
    }

    // Verificar que el estado cargado sea válido
    if (!_estadosDisponibles.contains(_estadoSeleccionado)) {
      _estadoSeleccionado = _estadosDisponibles.first;
    }
  }

  // ========== MÉTODOS DE VALIDACIÓN ==========

  /// Valida que un campo requerido no esté vacío
  ///
  /// [value] Valor del campo a validar
  /// [nombreCampo] Nombre del campo para el mensaje de error
  /// Returns: Mensaje de error o null si es válido
  String? _validarCampoRequerido(String? value, String nombreCampo) {
    if (value == null || value.trim().isEmpty) {
      return 'Por favor ingrese $nombreCampo';
    }
    return null;
  }

  /// Valida que el DNI tenga 8 dígitos
  ///
  /// [value] Valor del DNI a validar
  /// Returns: Mensaje de error o null si es válido
  String? _validarDNI(String? value) {
    final String? baseValidation = _validarCampoRequerido(value, 'el DNI');
    if (baseValidation != null) return baseValidation;

    final String trimmedValue = value!.trim();
    if (!RegExp(r'^\d{8}$').hasMatch(trimmedValue)) {
      return 'El DNI debe tener 8 dígitos';
    }

    return null;
  }

  /// Valida que el nombre completo tenga una longitud apropiada
  ///
  /// [value] Nombre completo a validar
  /// Returns: Mensaje de error o null si es válido
  String? _validarNombreCompleto(String? value) {
    final String? validacionBase = _validarCampoRequerido(
      value,
      'el nombre completo',
    );
    if (validacionBase != null) return validacionBase;

    final String valorLimpio = value!.trim();
    if (valorLimpio.length < 5) {
      return 'El nombre debe tener al menos 5 caracteres';
    }

    if (valorLimpio.length > 100) {
      return 'El nombre no puede exceder 100 caracteres';
    }

    return null;
  }

  /// Valida que el cargo tenga una longitud apropiada
  ///
  /// [value] Cargo a validar
  /// Returns: Mensaje de error o null si es válido
  String? _validarCargo(String? value) {
    final String? validacionBase = _validarCampoRequerido(value, 'el cargo');
    if (validacionBase != null) return validacionBase;

    final String valorLimpio = value!.trim();
    if (valorLimpio.length < 3) {
      return 'El cargo debe tener al menos 3 caracteres';
    }

    if (valorLimpio.length > 50) {
      return 'El cargo no puede exceder 50 caracteres';
    }

    return null;
  }

  /// Valida que la fecha de ingreso sea válida
  ///
  /// [value] Fecha de ingreso a validar
  /// Returns: Mensaje de error o null si es válido
  String? _validarFechaIngreso(String? value) {
    final String? validacionBase = _validarCampoRequerido(
      value,
      'la fecha de ingreso',
    );
    if (validacionBase != null) return validacionBase;

    if (_fechaIngreso == null) {
      return 'Seleccione una fecha de ingreso válida';
    }

    // Validar que la fecha no sea futura
    if (_fechaIngreso!.isAfter(DateTime.now())) {
      return 'La fecha de ingreso no puede ser futura';
    }

    // Validar que la fecha no sea muy antigua (más de 50 años)
    if (_fechaIngreso!.isBefore(
      DateTime.now().subtract(const Duration(days: 18250)),
    )) {
      // 50 años
      return 'La fecha de ingreso no puede ser hace más de 50 años';
    }

    return null;
  }

  // ========== MÉTODOS DE PROCESAMIENTO DE FORMULARIO ==========

  /// Procesa el envío del formulario de edición
  ///
  /// Valida todos los campos y si son correctos, prepara los datos
  /// actualizados para mostrar el diálogo de confirmación.
  void _procesarEnvioFormulario() {
    if (_claveFormulario.currentState!.validate()) {
      final Map<String, dynamic> datosActualizados =
          _construirDatosActualizados();
      _mostrarDialogoConfirmacion(datosActualizados);
    }
  }

  /// Construye el mapa de datos actualizados del empleado
  ///
  /// Returns: Mapa con todos los datos actualizados del empleado
  Map<String, dynamic> _construirDatosActualizados() {
    return {
      // Datos editables
      'nombreCompleto': _controladorNombreCompleto.text.trim(),
      'dni': _controladorDNI.text.trim(),
      'area': _areaSeleccionada,
      'cargo': _controladorCargo.text.trim(),
      'fechaIngreso': _fechaIngreso!.toIso8601String(),
      'estado': _estadoSeleccionado,

      // Metadatos de actualización
      'fechaActualizacion': DateTime.now().toIso8601String(),
      'ultimaModificacion': {
        'fecha': DateTime.now().toIso8601String(),
        'accion': 'edicion',
      },

      // Mantener datos originales
      'id': widget.empleadoToEdit['id'],
      'fechaCreacion':
          widget.empleadoToEdit['fechaCreacion'] ??
          DateTime.now().toIso8601String(),
    };
  }

  // ========== MÉTODOS DE DIÁLOGOS Y CONFIRMACIONES ==========

  /// Muestra el diálogo de confirmación para actualizar el empleado
  ///
  /// [datosEmpleado] Datos actualizados del empleado a confirmar
  void _mostrarDialogoConfirmacion(Map<String, dynamic> datosEmpleado) {
    showDialog(
      context: context,
      builder: (BuildContext context) => AlertDialog(
        title: const Row(
          children: [
            Icon(Icons.edit, color: Colors.blue),
            SizedBox(width: 8),
            Text(
              'Confirmar Actualización',
              style: TextStyle(
                fontSize: 14,
                fontWeight: FontWeight.bold,
              ),
            ),
          ],
        ),
        content: Column(
          mainAxisSize: MainAxisSize.min,
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const Text(
              '¿Está seguro de actualizar este empleado?',
              style: TextStyle(fontSize: 16),
            ),
            const SizedBox(height: 16),
            const Text(
              'Datos actualizados:',
              style: TextStyle(fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 8),
            _construirResumenEmpleado(datosEmpleado),
          ],
        ),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: const Text('Cancelar'),
          ),
          ElevatedButton(
            onPressed: () {
              Navigator.pop(context);
              _actualizarEmpleado(datosEmpleado);
            },
            style: ElevatedButton.styleFrom(backgroundColor: Colors.blue),
            child: const Text(
              'Actualizar',
              style: TextStyle(color: Colors.white),
            ),
          ),
        ],
      ),
    );
  }

  /// Construye el widget de resumen del empleado para confirmación
  ///
  /// [datosEmpleado] Datos del empleado a mostrar
  /// Returns: Widget con el resumen del empleado
  Widget _construirResumenEmpleado(Map<String, dynamic> datosEmpleado) {
    return Container(
      padding: const EdgeInsets.all(12),
      decoration: BoxDecoration(
        color: Colors.grey[50],
        borderRadius: BorderRadius.circular(8),
        border: Border.all(color: Colors.grey[300]!),
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        mainAxisSize: MainAxisSize.min,
        children: [
          _construirFilaDato(
            'Nombre:',
            datosEmpleado['nombreCompleto']?.toString() ?? 'N/A',
          ),
          _construirFilaDato('DNI:', datosEmpleado['dni']?.toString() ?? 'N/A'),
          _construirFilaDato(
            'Área:',
            _areaLabels[datosEmpleado['area']] ??
                datosEmpleado['area']?.toString() ??
                'N/A',
          ),
          _construirFilaDato(
            'Cargo:',
            datosEmpleado['cargo']?.toString() ?? 'N/A',
          ),
          _construirFilaDato(
            'Fecha Ingreso:',
            _formatearFecha(datosEmpleado['fechaIngreso']),
          ),
          Row(
            children: [
              const Text(
                'Estado: ',
                style: TextStyle(fontWeight: FontWeight.w500),
              ),
              Text(
                datosEmpleado['estado'] == 'activo' ? 'Activo' : 'Inactivo',
                style: TextStyle(
                  color: datosEmpleado['estado'] == 'activo'
                      ? Colors.green
                      : Colors.red,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ],
          ),
        ],
      ),
    );
  }

  /// Construye una fila de dato con etiqueta y valor
  ///
  /// [etiqueta] Etiqueta del dato
  /// [valor] Valor del dato
  /// Returns: Widget Row con la información
  Widget _construirFilaDato(String etiqueta, String valor) {
    return Padding(
      padding: const EdgeInsets.only(bottom: 4),
      child: Row(
        children: [
          Text(etiqueta, style: const TextStyle(fontWeight: FontWeight.w500)),
          const SizedBox(width: 4),
          Expanded(child: Text(valor)),
        ],
      ),
    );
  }

  // ========== OPERACIONES DE BASE DE DATOS ==========

  /// Actualiza el empleado en la base de datos de Firebase
  ///
  /// [datosEmpleado] Datos actualizados del empleado
  /// Returns: Future que completa cuando la operación termine
  Future<void> _actualizarEmpleado(Map<String, dynamic> datosEmpleado) async {
    try {
      // Validar que tenemos un ID válido
      final String? idEmpleado = widget.empleadoToEdit['id']?.toString();
      if (idEmpleado == null || idEmpleado.isEmpty) {
        throw Exception('ID del empleado no válido');
      }

      // Actualizar en Firebase Firestore
      await FirebaseFirestore.instance
          .collection(_nombreColeccion)
          .doc(idEmpleado)
          .update(datosEmpleado);

      // Mostrar mensaje de éxito
      _mostrarMensajeExito(
        'Empleado "${datosEmpleado['nombreCompleto']}" actualizado correctamente',
      );

      // Regresar con indicador de éxito
      if (mounted) {
        Navigator.pop(context, true);
      }
    } catch (error) {
      // Manejar errores específicos
      String mensajeError = _procesarError(error);
      _mostrarMensajeError('Error al actualizar el empleado: $mensajeError');

      // Log del error para debugging
      print('Error al actualizar empleado: $error');
    }
  }

  // ========== MÉTODOS DE UTILIDAD ==========

  /// Procesa los errores de Firebase para mostrar mensajes user-friendly
  ///
  /// [error] Error capturado de Firebase
  /// Returns: Mensaje de error apropiado para el usuario
  String _procesarError(dynamic error) {
    if (error.toString().contains('network')) {
      return 'Verifique su conexión a internet';
    } else if (error.toString().contains('permission')) {
      return 'No tiene permisos para realizar esta operación';
    } else if (error.toString().contains('not-found')) {
      return 'El empleado no fue encontrado';
    } else if (error.toString().contains('quota')) {
      return 'Se ha excedido la cuota de la base de datos';
    } else {
      return 'Error interno del servidor';
    }
  }

  /// Formatea una fecha ISO string para mostrar al usuario
  ///
  /// [fechaString] Fecha en formato ISO string
  /// Returns: Fecha formateada como DD/MM/YYYY
  String _formatearFecha(String fechaString) {
    try {
      final DateTime fecha = DateTime.parse(fechaString);
      return '${fecha.day.toString().padLeft(2, '0')}/${fecha.month.toString().padLeft(2, '0')}/${fecha.year}';
    } catch (e) {
      return 'Fecha no disponible';
    }
  }

  /// Formatea una fecha para el campo de input
  ///
  /// [fecha] Fecha a formatear
  /// Returns: Fecha formateada como YYYY-MM-DD
  String _formatearFechaParaInput(DateTime fecha) {
    return '${fecha.year}-${fecha.month.toString().padLeft(2, '0')}-${fecha.day.toString().padLeft(2, '0')}';
  }

  /// Muestra el selector de fecha
  Future<void> _mostrarSelectorFecha() async {
    final DateTime? fechaSeleccionada = await showDatePicker(
      context: context,
      initialDate: _fechaIngreso ?? DateTime.now(),
      firstDate: DateTime(1950),
      lastDate: DateTime.now(),
      initialEntryMode: DatePickerEntryMode.calendar,
      helpText: 'SELECCIONAR FECHA DE INGRESO',
      cancelText: 'CANCELAR',
      confirmText: 'SELECCIONAR',
      errorFormatText: 'Formato de fecha inválido',
      errorInvalidText: 'Fecha fuera de rango válido',
      fieldLabelText: 'Fecha de ingreso',
      fieldHintText: 'DD/MM/AAAA',
    );

    if (fechaSeleccionada != null && fechaSeleccionada != _fechaIngreso) {
      setState(() {
        _fechaIngreso = fechaSeleccionada;
        _controladorFechaIngreso.text = _formatearFechaParaInput(
          fechaSeleccionada,
        );
      });
    }
  }

  // ========== MÉTODOS DE INTERFAZ DE USUARIO ==========

  /// Muestra un mensaje de error al usuario
  ///
  /// [mensaje] Mensaje de error a mostrar
  void _mostrarMensajeError(String mensaje) {
    if (mounted) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(
          content: Text(mensaje),
          backgroundColor: Colors.red,
          duration: const Duration(seconds: 4),
          action: SnackBarAction(
            label: 'OK',
            textColor: Colors.white,
            onPressed: () {
              ScaffoldMessenger.of(context).hideCurrentSnackBar();
            },
          ),
        ),
      );
    }
  }

  /// Muestra un mensaje de éxito al usuario
  ///
  /// [mensaje] Mensaje de éxito a mostrar
  void _mostrarMensajeExito(String mensaje) {
    if (mounted) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(
          content: Row(
            children: [
              const Icon(Icons.check_circle, color: Colors.white, size: 20),
              const SizedBox(width: 8),
              Expanded(child: Text(mensaje)),
            ],
          ),
          backgroundColor: Colors.green,
          duration: const Duration(seconds: 3),
        ),
      );
    }
  }

  /// Muestra información detallada sobre las áreas disponibles
  void _mostrarInfoAreas() {
    showDialog(
      context: context,
      builder: (BuildContext context) => AlertDialog(
        title: const Row(
          children: [
            Icon(Icons.business_center, color: Colors.purple),
            SizedBox(width: 8),
            Text('Áreas de Trabajo'),
          ],
        ),
        content: const Column(
          mainAxisSize: MainAxisSize.min,
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              'Áreas disponibles:',
              style: TextStyle(fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 12),
            Text('👨‍🍳 Cocina: Personal de cocina y preparación'),
            Text('💁 Atención: Atención al cliente y meseros'),
            Text('🚗 Delivery: Repartidores y delivery'),
            Text('📊 Administración: Personal administrativo'),
          ],
        ),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: const Text('Entendido'),
          ),
        ],
      ),
    );
  }

  /// Muestra el diálogo de confirmación para eliminar el empleado
  void _mostrarConfirmacionEliminacion() {
    showDialog(
      context: context,
      builder: (BuildContext context) => AlertDialog(
        title: const Row(
          children: [
            Icon(Icons.warning, color: Colors.red),
            SizedBox(width: 8),
            Text('Eliminar Empleado'),
          ],
        ),
        content: Text(
          '¿Está seguro de eliminar al empleado "${_controladorNombreCompleto.text}"?\n\nEsta acción no se puede deshacer.',
          style: const TextStyle(fontSize: 16),
        ),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: const Text('Cancelar'),
          ),
          ElevatedButton(
            onPressed: () {
              Navigator.pop(context);
              _eliminarEmpleado();
            },
            style: ElevatedButton.styleFrom(backgroundColor: Colors.red),
            child: const Text(
              'Eliminar',
              style: TextStyle(color: Colors.white),
            ),
          ),
        ],
      ),
    );
  }

  /// Elimina el empleado de la base de datos
  Future<void> _eliminarEmpleado() async {
    try {
      final String? idEmpleado = widget.empleadoToEdit['id']?.toString();

      if (idEmpleado == null || idEmpleado.isEmpty) {
        throw Exception('ID del empleado no válido');
      }

      // TODO: Implementar eliminación real en Firebase Firestore
      // await FirebaseFirestore.instance
      //     .collection(_nombreColeccion)
      //     .doc(idEmpleado)
      //     .delete();

      // Por ahora, solo simular la eliminación
      print('Eliminando empleado con ID: $idEmpleado');

      _mostrarMensajeExito('Empleado eliminado correctamente');

      // Regresar con indicador de eliminación
      if (mounted) {
        Navigator.pop(context, {'deleted': true, 'id': idEmpleado});
      }
    } catch (error) {
      String mensajeError = _procesarError(error);
      _mostrarMensajeError('Error al eliminar el empleado: $mensajeError');
      print('Error al eliminar empleado: $error');
    }
  }

  /// Muestra el diálogo para restablecer los cambios del formulario
  void _restablecerFormulario() {
    showDialog(
      context: context,
      builder: (BuildContext context) => AlertDialog(
        title: const Row(
          children: [
            Icon(Icons.restore, color: Colors.orange),
            SizedBox(width: 8),
            Text('Restablecer Cambios'),
          ],
        ),
        content: const Text(
          '¿Desea descartar todos los cambios realizados y volver a los valores originales?',
        ),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: const Text('Cancelar'),
          ),
          ElevatedButton(
            onPressed: () {
              Navigator.pop(context);
              _cargarDatosEmpleado(); // Recargar datos originales
              _mostrarMensajeExito('Cambios descartados correctamente');
            },
            style: ElevatedButton.styleFrom(backgroundColor: Colors.orange),
            child: const Text(
              'Restablecer',
              style: TextStyle(color: Colors.white),
            ),
          ),
        ],
      ),
    );
  }

  // ========== MÉTODO BUILD PRINCIPAL ==========

  /// Construye la interfaz principal de la pantalla de edición
  ///
  /// Returns: Widget Scaffold con la estructura completa de la pantalla
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Editar Empleado',
          style: TextStyle(fontWeight: FontWeight.bold),
        ),
        backgroundColor: Colors.blue[700],
        foregroundColor: Colors.white,
        elevation: 2,
        actions: [
          IconButton(
            icon: const Icon(Icons.restore),
            onPressed: _restablecerFormulario,
            tooltip: 'Restablecer cambios',
          ),
          IconButton(
            icon: const Icon(Icons.delete),
            onPressed: _mostrarConfirmacionEliminacion,
            color: Colors.red,
            tooltip: 'Eliminar empleado',
          ),
        ],
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16.0),
        child: Form(
          key: _claveFormulario,
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: [
              // Información del empleado actual
              _construirInfoEmpleadoActual(),

              const SizedBox(height: 20),

              // Campo: Nombre Completo
              _construirCampoNombreCompleto(),

              const SizedBox(height: 20),

              // Campo: DNI
              _construirCampoDNI(),

              const SizedBox(height: 20),

              // Campo: Área
              _construirCampoArea(),

              const SizedBox(height: 20),

              // Campo: Cargo
              _construirCampoCargo(),

              const SizedBox(height: 20),

              // Campo: Fecha de Ingreso
              _construirCampoFechaIngreso(),

              const SizedBox(height: 20),

              // Campo: Estado
              _construirCampoEstado(),

              const SizedBox(height: 30),

              // Botones de acción
              _construirBotonesAccion(),
            ],
          ),
        ),
      ),
    );
  }

  // ========== MÉTODOS DE CONSTRUCCIÓN DE WIDGETS ==========

  /// Construye el widget de información del empleado actual siendo editado
  ///
  /// Returns: Widget Card con la información del empleado
  Widget _construirInfoEmpleadoActual() {
    return Card(
      color: Colors.blue[50],
      elevation: 2,
      child: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            const Row(
              children: [
                Icon(Icons.edit, color: Colors.blue, size: 20),
                SizedBox(width: 8),
                Text(
                  'Editando Empleado:',
                  style: TextStyle(
                    fontWeight: FontWeight.bold,
                    color: Colors.blue,
                    fontSize: 16,
                  ),
                ),
              ],
            ),
            const SizedBox(height: 12),
            _construirFilaInfo(
              'ID:',
              widget.empleadoToEdit['id']?.toString() ?? 'N/A',
            ),
            if (widget.empleadoToEdit['fechaCreacion'] != null) ...[
              const SizedBox(height: 4),
              _construirFilaInfo(
                'Creado:',
                _formatearFecha(widget.empleadoToEdit['fechaCreacion']),
              ),
            ],
            if (widget.empleadoToEdit['fechaActualizacion'] != null) ...[
              const SizedBox(height: 4),
              _construirFilaInfo(
                'Última actualización:',
                _formatearFecha(widget.empleadoToEdit['fechaActualizacion']),
              ),
            ],
          ],
        ),
      ),
    );
  }

  /// Construye una fila de información con etiqueta y valor
  ///
  /// [etiqueta] Etiqueta de la información
  /// [valor] Valor de la información
  /// Returns: Widget Row con la información
  Widget _construirFilaInfo(String etiqueta, String valor) {
    return Row(
      children: [
        Text(
          etiqueta,
          style: const TextStyle(
            fontWeight: FontWeight.w600,
            color: Colors.grey,
          ),
        ),
        const SizedBox(width: 8),
        Expanded(
          child: Text(
            valor,
            style: const TextStyle(fontWeight: FontWeight.w500),
          ),
        ),
      ],
    );
  }

  /// Construye el campo de entrada para el nombre completo
  ///
  /// Returns: Widget TextFormField para el nombre completo
  Widget _construirCampoNombreCompleto() {
    return TextFormField(
      controller: _controladorNombreCompleto,
      decoration: const InputDecoration(
        labelText: 'Nombre Completo *',
        hintText: 'Ej: Juan Carlos Pérez García',
        border: OutlineInputBorder(),
        prefixIcon: Icon(Icons.person, color: Colors.blue),
      ),
      validator: _validarNombreCompleto,
      textInputAction: TextInputAction.next,
      textCapitalization: TextCapitalization.words,
      maxLength: 100,
    );
  }

  /// Construye el campo de entrada para el DNI
  ///
  /// Returns: Widget TextFormField para el DNI
  Widget _construirCampoDNI() {
    return TextFormField(
      controller: _controladorDNI,
      decoration: const InputDecoration(
        labelText: 'DNI *',
        hintText: 'Ej: 71234567',
        border: OutlineInputBorder(),
        prefixIcon: Icon(Icons.badge, color: Colors.green),
        counterText: '8 dígitos',
      ),
      keyboardType: TextInputType.number,
      inputFormatters: [
        FilteringTextInputFormatter.digitsOnly,
        LengthLimitingTextInputFormatter(8),
      ],
      validator: _validarDNI,
      textInputAction: TextInputAction.next,
      maxLength: 8,
    );
  }

  /// Construye el campo de selección de área del empleado
  ///
  /// Returns: Widget Column con dropdown para áreas
  Widget _construirCampoArea() {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Row(
          children: [
            const Text(
              'Área *',
              style: TextStyle(fontWeight: FontWeight.bold, fontSize: 16),
            ),
            const SizedBox(width: 8),
            IconButton(
              icon: const Icon(
                Icons.info_outline,
                size: 18,
                color: Colors.blue,
              ),
              onPressed: _mostrarInfoAreas,
              tooltip: 'Ver información de áreas',
            ),
          ],
        ),
        const SizedBox(height: 8),
        DropdownButtonFormField<String>(
          value: _areaSeleccionada,
          decoration: const InputDecoration(
            border: OutlineInputBorder(),
            contentPadding: EdgeInsets.symmetric(horizontal: 12, vertical: 16),
            prefixIcon: Icon(Icons.business_center, color: Colors.purple),
          ),
          items: _areasDisponibles.map((area) {
            return DropdownMenuItem(
              value: area,
              child: Text(_areaLabels[area] ?? area),
            );
          }).toList(),
          onChanged: (String? nuevoValor) {
            if (nuevoValor != null) {
              setState(() {
                _areaSeleccionada = nuevoValor;
              });
            }
          },
          validator: (String? value) =>
              value == null || value.isEmpty ? 'Seleccione un área' : null,
        ),
      ],
    );
  }

  /// Construye el campo de entrada para el cargo
  ///
  /// Returns: Widget TextFormField para el cargo
  Widget _construirCampoCargo() {
    return TextFormField(
      controller: _controladorCargo,
      decoration: const InputDecoration(
        labelText: 'Cargo *',
        hintText: 'Ej: Chef Principal, Mesero, Administrador',
        border: OutlineInputBorder(),
        prefixIcon: Icon(Icons.work, color: Colors.orange),
      ),
      validator: _validarCargo,
      textInputAction: TextInputAction.next,
      textCapitalization: TextCapitalization.words,
      maxLength: 50,
    );
  }

  /// Construye el campo de entrada para la fecha de ingreso
  ///
  /// Returns: Widget TextFormField para la fecha de ingreso
  Widget _construirCampoFechaIngreso() {
    return TextFormField(
      controller: _controladorFechaIngreso,
      decoration: InputDecoration(
        labelText: 'Fecha de Ingreso *',
        hintText: 'YYYY-MM-DD',
        border: const OutlineInputBorder(),
        prefixIcon: const Icon(Icons.calendar_today, color: Colors.red),
        suffixIcon: IconButton(
          icon: const Icon(Icons.calendar_month),
          onPressed: _mostrarSelectorFecha,
        ),
      ),
      readOnly: true,
      onTap: _mostrarSelectorFecha,
      validator: _validarFechaIngreso,
    );
  }

  /// Construye el campo de selección de estado del empleado
  ///
  /// Returns: Widget Column con dropdown para estados
  Widget _construirCampoEstado() {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        const Text(
          'Estado *',
          style: TextStyle(fontWeight: FontWeight.bold, fontSize: 16),
        ),
        const SizedBox(height: 8),
        DropdownButtonFormField<String>(
          value: _estadoSeleccionado,
          decoration: const InputDecoration(
            border: OutlineInputBorder(),
            contentPadding: EdgeInsets.symmetric(horizontal: 12, vertical: 16),
            prefixIcon: Icon(Icons.flag, color: Colors.purple),
          ),
          items: _estadosDisponibles.map((estado) {
            return DropdownMenuItem(
              value: estado,
              child: Text(
                estado == 'activo' ? 'Activo' : 'Inactivo',
                style: TextStyle(
                  color: estado == 'activo' ? Colors.green : Colors.red,
                ),
              ),
            );
          }).toList(),
          onChanged: (String? nuevoValor) {
            if (nuevoValor != null) {
              setState(() {
                _estadoSeleccionado = nuevoValor;
              });
            }
          },
          validator: (String? value) =>
              value == null || value.isEmpty ? 'Seleccione un estado' : null,
        ),
      ],
    );
  }

  /// Construye los botones de acción del formulario
  ///
  /// Returns: Widget Row con botones de cancelar y actualizar
  Widget _construirBotonesAccion() {
    return Row(
      children: [
        Expanded(
          child: OutlinedButton.icon(
            onPressed: () => Navigator.pop(context),
            label: const Text('Cancelar'),
            style: OutlinedButton.styleFrom(
              padding: const EdgeInsets.symmetric(vertical: 16),
              side: const BorderSide(color: Colors.grey),
            ),
          ),
        ),
        const SizedBox(width: 16),
        Expanded(
          child: ElevatedButton.icon(
            onPressed: _procesarEnvioFormulario,
            label: const Text(
              'Actualizar',
              style: TextStyle(color: Colors.white),
            ),
            style: ElevatedButton.styleFrom(
              padding: const EdgeInsets.symmetric(vertical: 16),
              backgroundColor: Colors.blue,
              elevation: 2,
            ),
          ),
        ),
      ],
    );
  }
}

```