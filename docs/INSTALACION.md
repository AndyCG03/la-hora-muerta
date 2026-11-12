# Instalación

- [Android](#android)
- [Windows](#windows)
- [Comprobar la descarga (opcional)](#comprobar-la-descarga-opcional)
- [Actualizar a una versión nueva](#actualizar-a-una-versión-nueva)
- [Solución de problemas](#solución-de-problemas)
- [Desinstalar](#desinstalar)

---

## Android

**Requisitos:** Android 7.0 o superior, procesador de 64 bits (arm64) y soporte Vulkan (la gran mayoría de teléfonos desde 2018). Unos 200 MB libres.

1. Descarga [**LaHoraMuerta.apk**](https://github.com/AndyCG03/la-hora-muerta/releases/latest/download/LaHoraMuerta.apk) desde el teléfono, o desde el ordenador y pásalo al teléfono.
2. Abre el archivo desde **Descargas** o desde tu gestor de archivos.
3. Android avisará de que la app viene de una **fuente desconocida**: pulsa **Configuración**, activa **Permitir de esta fuente** y vuelve atrás.
4. Pulsa **Instalar**. Si Google Play Protect muestra un aviso de *app no reconocida*, es lo habitual con apps que no vienen de la tienda: elige **Instalar de todas formas**.
5. Abre **La Hora Muerta** desde el menú de aplicaciones. Gira el teléfono en horizontal.

> El juego no pide ningún permiso salvo el de **vibración**, que usa en los sustos.

### Con cable USB (avanzado)

Con la *depuración USB* activada y las [herramientas de Android](https://developer.android.com/tools/releases/platform-tools) instaladas:

```bash
adb install -r LaHoraMuerta.apk
```

## Windows

**Requisitos:** Windows 10 u 11 de 64 bits y una tarjeta gráfica compatible con DirectX 12. Unos 300 MB libres.

1. Descarga [**LaHoraMuerta-Windows.exe**](https://github.com/AndyCG03/la-hora-muerta/releases/latest/download/LaHoraMuerta-Windows.exe).
2. Guárdalo en una carpeta propia, por ejemplo `Juegos\La Hora Muerta`.
3. Ábrelo con doble clic. No necesita instalación.
4. Si Windows SmartScreen muestra *Windows protegió su PC* (ocurre con programas sin firma comercial), pulsa **Más información → Ejecutar de todas formas**.

## Comprobar la descarga (opcional)

Cada versión publica un archivo `SHA256SUMS.txt` con la huella de cada descarga. Para comprobar que tu archivo está completo y no se ha modificado:

**Windows (PowerShell)**

```powershell
Get-FileHash .\LaHoraMuerta-Windows.exe -Algorithm SHA256
```

**macOS / Linux**

```bash
sha256sum LaHoraMuerta.apk
```

El resultado debe coincidir con el de `SHA256SUMS.txt`.

## Actualizar a una versión nueva

- **Android:** instala el APK nuevo **encima** del anterior, sin desinstalar. Todas las versiones están firmadas con la misma clave, así que se conservan la partida guardada y las opciones.
- **Windows:** sustituye el `.exe` por el nuevo. La partida guardada no está junto al ejecutable, así que se conserva.

## Solución de problemas

| Problema | Solución |
|---|---|
| Android dice «App no instalada» | Desinstala antes cualquier versión que no venga de este repositorio, o comprueba que hay espacio libre. |
| El juego se cierra al abrirlo en Android | Tu teléfono puede no tener Vulkan o ser de 32 bits. Abre una incidencia con el modelo. |
| Va lento o se calienta el teléfono | *Opciones → Gráficos*: calidad **Baja** y baja la escala de renderizado. |
| No se oye nada | Comprueba el volumen del sistema y *Opciones → Sonido*. Los auriculares ayudan mucho. |
| Textos en inglés | *Opciones → Idioma*. Las voces siempre están en inglés; los subtítulos siguen tu idioma. |
| Demasiado difícil | *Opciones → Dificultad → Fácil*. Se aplica al momento. |
| El ratón no gira la cámara (Windows) | Haz clic dentro de la ventana del juego. |

¿No está aquí tu problema? [Abre una incidencia](https://github.com/AndyCG03/la-hora-muerta/issues/new/choose).

## Desinstalar

- **Android:** mantén pulsado el icono → **Desinstalar**. Se borran también la partida y las opciones.
- **Windows:** borra el `.exe`. La partida y las opciones quedan en `%APPDATA%\Godot\app_userdata\La Hora Muerta`; borra esa carpeta para eliminarlas también.
