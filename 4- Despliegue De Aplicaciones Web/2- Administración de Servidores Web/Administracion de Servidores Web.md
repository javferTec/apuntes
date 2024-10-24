# ADMINISTRACIÓN DE SERVIDORES WEB

Hay dos tipos de servidores web:

- **[Servidores Web Externos](./servidores%20web%20externos.md)**: Son programas completos que hacen de servidor Web. Una vez instalados/ejecutados se añade el código específico de la aplicación en la carpeta del servidor que indique la documentación. Algunas herramientas son: Apache2 y Nginx.

- **[Servidores Web Integrados](./servidores%20web%20integrados.md)** (o librerías de servidores web):  Se hace una aplicación (por ejemplo en Java) y se añade como una librería (un JAR) , el código del Servidor Web. Se puede hacer con NodeJS y la librería Express.


## **DIFERENCIAS ENTRE AMBOS**

**Servidor Externo:** gasta menos RAM pero cada proyecto no es independiente, todos comparten el mismo servidor.

**Servidor Integrado:**  gasta mas RAM, pero es más versátil, se utiliza virtualización (docker).