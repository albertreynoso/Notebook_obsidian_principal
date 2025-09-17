## Configuración con Android Studio

### Install and set up Flutter

Now that you've installed Git and VS Code, follow these steps to use VS Code to install and set up Flutter.

1. ### Launch VS Code
    
    If not already open, open VS Code by searching for it with Spotlight or opening it manually from the directory where it's installed.
    
2. ### Add the Flutter extension to VS Code
    
    To add the Dart and Flutter extensions to VS Code, visit the [Flutter extension's marketplace page](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter), and click **Install**. If prompted by your browser, allow it to open VS Code.
    
3. ### Install Flutter with VS Code
    
    1. Open the command palette in VS Code.
        
        Go to **View** > **Command Palette** or press Control + Shift + P.
        
    2. In the command palette, type `flutter`.
        
    3. Select **Flutter: New Project**.
        
    4. VS Code prompts you to locate the Flutter SDK on your computer. Select **Download SDK**.
        
    5. When the **Select Folder for Flutter SDK** dialog displays, choose where you want to install Flutter.
        
    6. Click **Clone Flutter**.
        
        While downloading Flutter, VS Code displays this pop-up notification:
        
        ```
        Downloading the Flutter SDK. This may take a few minutes.
        ```
        
        content_copy
        
        This download takes a few minutes. If you suspect that the download has hung, click **Cancel** then start the installation again.
        
    7. Click **Add SDK to PATH**.
        
        When successful, a notification displays:
        
        ```
        The Flutter SDK was added to your PATH
        ```
        
        content_copy
        
    8. VS Code might display a Google Analytics notice.
        
        If you agree, click **OK**.
        
    9. To ensure that Flutter is available in all terminals:
        
        1. Close, then reopen all terminal windows.
        2. Restart VS Code.
4. ### Validate your setup
    
    To ensure you installed Flutter correctly, run `flutter doctor -v` in your preferred terminal.
    
    If the command isn't found or there's an error, check out [Flutter installation troubleshooting](https://docs.flutter.dev/install/troubleshoot).
### Android Studio

To create a Flutter app with Android Studio, you first need to [install Flutter](https://docs.flutter.dev/get-started/install) and [set up Android Studio](https://docs.flutter.dev/tools/android-studio#installation-and-setup) for Flutter development. Then follow these steps:

1. **Launch Android Studio**
    
    Open Android Studio with the Dart and Flutter plugins installed.
    
2. ### Begin project creation
    
    If you're on the IDE welcome dialog that says **Welcome to Android Studio**, find and click the **New Flutter Project** button in the center.
    
    If you already have a project open, either close it or go to **File** > **New** > **New Flutter Project...**.
    
3. ### Choose a project type
    
    In the **New Project** dialog, under **Generators** in the left panel, select **Flutter**.
    
4. ### Verify Flutter SDK setup
    
    At the top of the right panel, ensure the **Flutter SDK path** value matches the location of the Flutter SDK you'd like to develop with. If not, update it by choosing or specifying the correct one.
    
5. ### Configure your project
    
    Click **Next** to continue to project configuration. Multiple configuration options should appear.
    
    In the **Project name** field, enter a name for your app that follows the `lowercase_with_underscores` naming convention, following the [Effective Dart](https://dart.dev/effective-dart/style#do-name-packages-and-file-system-entities-using-lowercase-with-underscores) guidelines.
    
    If you're not creating an application, select another template from the **Project type** dropdown.
    
    If you're creating an app that you might publish in the future, set the **Organization** field [to your company domain](https://docs.flutter.dev/tools/android-studio#set-the-company-domain).
    
    The other fields can be kept as is or configured according to your project's needs.
    
6. ### Finish project creation
    
    Once you've completed the configuration of your project, click **Create** to begin project initialization.
    
7. ### Wait for workspace initialization
    
    Android Studio will now initialize your workspace, bootstrap your project file structure, and retrieve your app's dependencies. This might take a while and can be tracked at the bottom of the window.
    
8. ### Run your app
    
    Your new app should now be created and open in Android Studio. To try your new app, follow the steps to [run and debug](https://docs.flutter.dev/tools/android-studio#running-and-debugging) in Android Studio.


## Configuración de tecnologias
###  Google Maps API: Pasos para crear y configurar tu clave de 
#### 1. Acceder a Google Cloud Console
- **Ve a [Google Cloud Console](https://console.cloud.google.com/)**
- **Inicia sesión con tu cuenta de Google**
#### 2. Crear un nuevo proyecto (o seleccionar uno existente)

- **Haz clic en el selector de proyectos en la parte superior**
- **→ "Nuevo proyecto"**
- **Asigna un nombre y haz clic en "Crear"**
#### 3. Habilitar las APIs necesarias

- **En el menú lateral, ve a "APIs y Servicios" > "Biblioteca"**
- **Busca y habilita estas APIs:**
    - **Maps SDK for Android**
    - **Maps SDK for iOS**
    - **Places API (opcional pero recomendado)**
#### 4. Crear credenciales

- **Ve a "APIs y Servicios" > "Credenciales"**
- **Haz clic en "+ Crear credenciales" → "Clave de API"**
- **Se generará tu clave API**
#### 5. Configurar restricciones de la clave (IMPORTANTE)**

- Haz clic en **"Restringir clave"** en la clave recién creada
- **Restricciones de aplicación**:
    - Para **Android**:
        - Agrega el nombre de tu paquete (ej: `com.tudominio.app`)
        - Agrega tu huella digital SHA-1 (ver más abajo)
        - El nombre de paquete se encuentra aquí:
          ![[Pasted image 20250917102741.png]]
        - La clave SHA-1 se encuentra aquí:
          ![[Pasted image 20250917102913.png]]
          ![[Pasted image 20250917102946.png]]

    - Para **iOS**:
        - Agrega el ID del bundle (ej: `com.tudominio.app`)    
- **Restricciones de APIs**:
    - Selecciona solo las APIs de Maps que habilitaste

#### Configura en la app
- **Insertar la api aquí:**
          ![[Pasted image 20250917102634.png]]
- **Ejecuta el comando pub get para que el paquete de google empiece a funcionar**
![[Pasted image 20250917103557.png]]
- **Ejecuta la app**

### Otro servicio
## Otras cosas 
## Otras cosas 
