# Informe calculo - pi

## Julian Briñez
## Francisco Morales

# Calculo pi 

## Tabla de Contenido
- [Introducción al Cálculo π\pi](#introducción-al-cálculo-πpi)
- [¿Qué es un Proceso en el Cálculo π\pi?](#qué-es-un-proceso-en-el-cálculo-πpi)
- [Comunicación entre Procesos](#comunicación-entre-procesos)
- [Creación y Uso de Canales](#creación-y-uso-de-canales)
- [Dinamismo y Flujo de Información](#dinamismo-y-flujo-de-información)
- [Aplicaciones en la Ciencia Computacional Básica](#aplicaciones-en-la-ciencia-computacional-básica)
- [Aplicaciones en la Ciencia Computacional Intermedia](#aplicaciones-en-la-ciencia-computacional-intermedia)
- [Ejemplo Práctico: Un Protocolo de Comunicación](#ejemplo-práctico-un-protocolo-de-comunicación)
- [Conclusión](#conclusión)


## Introducción al Cálculo π\pi
El cálculo π\pi es un modelo matemático diseñado para analizar y describir sistemas que interactúan de manera dinámica, como redes de computadoras, sistemas distribuidos y agentes móviles. La nomenclatura del cálculo π\pi juega un papel crucial para representar los elementos que forman parte de estos sistemas: procesos, canales, datos y patrones. Los procesos son las entidades computacionales que realizan tareas, como enviar o recibir información. Los canales, identificados con nombres como c, a o b, son las vías que conectan los procesos. Además, se utilizan variables para recibir y manipular datos, y patrones para estructurar cómo se descompone la información transmitida. Esta nomenclatura precisa permite modelar interacciones complejas de forma clara y efectiva.

---

## ¿Qué es un Proceso en el Cálculo π\pi?
En el cálculo π\pi, un proceso es una entidad computacional que ejecuta acciones específicas, como enviar datos, recibir datos o realizar cálculos internos. Los procesos se representan con letras como P, Q, R y realizan sus tareas interactuando a través de canales. Un canal, identificado con un nombre único como c, a o b, permite la comunicación entre procesos. Las operaciones básicas son:
- `!` para enviar datos por un canal.
- `?` para recibir datos desde un canal.

Los datos transmitidos se representan mediante tuplas, como `(v1,v2)`, donde cada elemento es un valor específico. Las variables, como `x` y `y`, son marcadores que capturan los datos recibidos.

```plaintext
P1 = c!〈"Hola"〉 | stop
P2 = c?(x) print(x) | stop
Sistema = P1 | P2
```

- `P1` define un proceso que usa `c!` para enviar `"Hola"` por el canal `c` y luego se detiene.
- `P2` define un proceso que usa `c?` para recibir datos del canal `c`, guardarlos en la variable `x` y mostrarlos.
- `Sistema` combina `P1` y `P2` en paralelo, permitiendo la interacción entre ambos.

---

## Comunicación entre Procesos
La interacción en el cálculo π\pi se realiza mediante canales que conectan procesos. Un canal, identificado por un nombre como `c`, actúa como un tubo a través del cual fluyen los datos. Los datos que viajan por el canal pueden ser valores simples como `"Hola"` o estructuras más complejas como `(v1,v2)`. El operador `!` indica que un proceso está enviando datos, mientras que `?` denota que otro proceso los está recibiendo.

```plaintext
Enviar = c!〈"Dato1"〉 | c!〈"Dato2"〉 | stop
Recibir = c?(x) print(x) | c?(y) print(y) | stop
Sistema = Enviar | Recibir
```

- `Enviar` utiliza `c!` para enviar `"Dato1"` y `"Dato2"` por el canal `c`.
- `Recibir` utiliza `c?` para capturar los datos enviados por `Enviar`. El primer dato recibido se guarda en `x` y el segundo en `y`.
- `Sistema` pone a los procesos `Enviar` y `Recibir` en paralelo, permitiendo la transmisión y recepción de datos.

---

## Creación y Uso de Canales
Una característica poderosa del cálculo π\pi es la capacidad de crear canales privados, identificados con `(new c)`. Esto asegura que ciertos canales sean accesibles únicamente por los procesos que los crean. Por ejemplo, un canal privado `c` permite que dos procesos se comuniquen sin interferencia de terceros.

```plaintext
P1 = (new c)(c!〈"Dato privado"〉 | stop)
P2 = (new c)(c?(x) print(x) | stop)
Sistema = P1 | P2
```

- `P1` crea un canal privado `c` con `(new c)` y envía `"Dato privado"`.
- `P2` también crea un canal privado `c`, pero su `c` es independiente del `c` de `P1`.
- `Sistema` pone a ambos procesos en paralelo, pero sus canales privados garantizan que no interactúen entre sí.

---

## Dinamismo y Flujo de Información
El cálculo π\pi permite que los canales mismos sean transmitidos como datos, lo que añade un nivel de flexibilidad y dinamismo. Un canal, identificado como `c`, puede ser enviado por otro canal, como `a`. Esto permite que los procesos establezcan nuevas conexiones dinámicamente.

```plaintext
Servidor = a!〈c〉 | stop
Cliente = a?(x) x!〈"Mensaje seguro"〉 | stop
Sistema = Servidor | Cliente
```

- `Servidor` envía el canal `c` al cliente a través del canal principal `a`.
- `Cliente` recibe el canal `c` (almacenado como `x`) y lo usa para enviar `"Mensaje seguro"`.
- `Sistema` permite que ambos procesos interactúen y ajusten sus canales dinámicamente.

---

## Aplicaciones en la Ciencia Computacional Básica
En un nivel básico, el cálculo π\pi modela cómo interactúan los componentes de un sistema computacional. Por ejemplo, un router que recibe paquetes de datos, los procesa y los reenvía puede representarse con canales como entrada y salida.

```plaintext
Router = entrada?(paquete) salida!〈paquete〉 | Router
```

El proceso `Router` recibe un paquete en el canal `entrada`, lo almacena temporalmente en la variable `paquete` y luego lo reenvía por el canal `salida`. Esta estructura puede repetirse indefinidamente, modelando el comportamiento continuo de un router.

---

## Aplicaciones en la Ciencia Computacional Intermedia
En sistemas más complejos, como aplicaciones distribuidas o sistemas en la nube, el cálculo π\pi ayuda a modelar y verificar interacciones entre procesos. Por ejemplo, un sistema de almacenamiento en la nube donde los usuarios envían solicitudes para acceder a recursos podría representarse como:

```plaintext
Cliente = solicitud!〈"Leer archivo"〉 | stop
Servidor = solicitud?(req) procesar!〈req〉 | stop
```

Aquí, los canales `solicitud` y `procesar` permiten modelar la comunicación entre el cliente y el servidor.
- `Cliente` envía una solicitud de lectura, y `Servidor` procesa esta solicitud antes de responder.

---

## Ejemplo Práctico: Un Protocolo de Comunicación
Para ilustrar un uso práctico del cálculo π\pi, considera un sistema de mensajería donde un usuario envía un mensaje y espera una confirmación (acknowledgment). Esto se logra mediante dos canales: uno para el mensaje (`c`) y otro para la confirmación (`ack`).

```plaintext
Usuario1 = c!〈"Mensaje", ack〉 | ack?() stop
Usuario2 = c?(m, ack) print(m) | ack!〈〉 stop
Sistema = Usuario1 | Usuario2
```

- `Usuario1` envía `"Mensaje"` junto con el canal `ack` para la confirmación.
- `Usuario2` recibe el mensaje `m` y el canal de confirmación `ack`. Luego imprime el mensaje y envía la confirmación.
- `Sistema` modela toda la interacción, asegurando que el mensaje se transmita y que haya una confirmación explícita.

---

## Conclusión
El cálculo π\pi es una herramienta matemática poderosa y versátil para modelar sistemas distribuidos e interactivos, donde los procesos, las conexiones y la comunicación son dinámicos y cambiantes. Su nomenclatura precisa permite describir con claridad los componentes fundamentales de un sistema, como los canales de comunicación, los datos transmitidos y las acciones realizadas por los procesos. Además, su capacidad para manejar canales privados y transmitir canales como datos lo convierte en un modelo ideal para sistemas modernos como redes de computadoras, aplicaciones en la nube y protocolos de comunicación.

Mediante ejemplos prácticos como el envío y recepción de mensajes o el manejo de confirmaciones, hemos visto cómo se aplican estos conceptos en escenarios reales. Desde la simulación de interacciones básicas en redes hasta la construcción de sistemas distribuidos más avanzados, el cálculo π\pi ofrece un marco formal para garantizar que las interacciones sean correctas, seguras y eficientes.

Para los estudiantes de ciencias computacionales, el cálculo π\pi no solo proporciona una forma de comprender cómo se comportan los sistemas interactivos, sino que también abre la puerta a la creación y análisis de nuevos modelos, contribuyendo al diseño de tecnologías innovadoras que respondan a los retos del mundo moderno. Con una comprensión sólida de su nomenclatura y aplicaciones, los futuros desarrolladores e ingenieros estarán mejor preparados para construir soluciones confiables y escalables en el ámbito computacional.
