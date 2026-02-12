Guía Técnica: Animación en Krita (San Valentín)
1. Preparación del Entorno
Interfaz: Ve a Ventana > Espacio de trabajo > Animation.

Línea de Tiempo: Asegúrate de ver el panel inferior con números (fotogramas).

FPS (Velocidad): En el panel de línea de tiempo, busca el número 24.00 y cámbialo a 12.00. Esto hará que necesitemos menos dibujos por segundo.

2. Configuración de Capas
En el panel de Capas (derecha), organiza tu proyecto así:

Capa 1 (Fondo): Dibuja un diseño estático. No necesitas crear fotogramas nuevos aquí, solo dibuja una vez.

Capa 2 (Animación): Aquí es donde ocurrirá la magia.

Haz clic derecho en el primer cuadrito (0) de la línea de tiempo.

Selecciona Crear fotograma en blanco.

3. El Proceso de Animación (Ciclo de Dibujo)
Para crear el mensaje (un corazón que late o letras que aparecen):

Dibujar: Realiza el primer trazo.

Avanzar: Haz clic en el siguiente cuadrito (ej. el 2 o 3 para que no sea tan rápido).

Nuevo Frame: Clic derecho > Crear fotograma en blanco.

Papel Cebolla: Haz clic en el icono de la bombilla en la capa. Verás el dibujo anterior en rojo/verde.

Repetir: Dibuja basándote en la guía traslúcida hasta terminar tu mensaje.

4. Configuración de Salida (FFmpeg)
Antes de exportar, Krita necesita "el motor" para crear el GIF.

Ve a Archivo > Renderizar animación.

En la sección Exportar, marca la casilla Imagen de vídeo.

Ruta de FFmpeg: Haz clic en el icono de la carpeta 📂 y busca el archivo ffmpeg.exe que descargaste.

Nota: Sin este archivo, Krita no puede procesar el formato GIF.

5. Exportación Final
Formato: Selecciona GIF animado en el menú desplegable.

Rango de fotogramas: Asegúrate de que el "Primer fotograma" sea 0 y el "Último fotograma" coincida con donde termina tu dibujo.

Renderizar: Presiona Aceptar y espera a que la barra de carga finalice.

💡 Tips para los alumnos:
Ctrl + Z: Su mejor amigo para corregir trazos.

Atajo rápido: Pueden usar las flechas del teclado ← → para moverse entre fotogramas y revisar la fluidez.

Color de Papel Cebolla: Si no ven bien los trazos previos, pueden ajustar la opacidad en el panel de Papel Cebolla (Onion Skin).
https://www.ffmpeg.org/download.html
