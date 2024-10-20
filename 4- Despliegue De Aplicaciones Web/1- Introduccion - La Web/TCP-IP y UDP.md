# TCP/IP Y UDP

Tanto TCP/IP como UDP son protocolos que forman parte de la suite de protocolos **Internet Protocol _(IP)_**, pero cada uno tiene un comportamiento diferente.

**TCP/IP** antes de transferir establece una conexión entre el servidor y el receptor, garantizando que ambos están listos para intercambiar información. Además, **garantiza la entrega correcta de datos**, ya que divide los datos en segmentos y asegura que lleguen en el orden correcto. La desventaja es que al ser más fiable es más lento.

_Algunas aplicaciones comunes son navegación web (HTTP/HTTPS), correo electrónico (SMTP), transferencia de archivos (FTP)._


Mientras que **UDP** no establece una conexión previa para enviar datos. Simplemente envía los datos sin asegurarse de que lleguen correctamente, lo cual no garantiza fiabilidad a pesar de ser más rápido.

_Algunas aplicaciones comunes son streaming de video y audio, juegos en línea, transmisiones en tiempo real, VoIP, donde la velocidad es más importante que la fiabilidad._

## Comparación resumida:

- **TCP**: Fiable, orientado a la conexión, control de flujo, reenvía datos perdidos, más lento.
- **UDP**: No fiable, sin conexión, más rápido, pero sin garantía de entrega o de orden.

