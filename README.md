SimpleChat - Chat Distribuido con JGroups
Este proyecto implementa una aplicación de chat distribuido que utiliza JGroups para la comunicación entre nodos. Cada instancia del chat se une a un clúster llamado ChatCluster y se comunica con otros nodos, compartiendo mensajes en tiempo real. Además, el estado (historial de mensajes) es replicado entre los nodos, permitiendo que los nuevos miembros del clúster sincronicen el historial existente.

Descripción del Código
La clase SimpleChat implementa la interfaz Receiver de JGroups, lo que permite recibir mensajes y gestionar eventos de vista (como cambios en el clúster).

Componentes Principales
Inicialización del Canal de JGroups:
Al iniciar, la aplicación crea un canal (JChannel) y se conecta al clúster ChatCluster. Luego, solicita el estado del historial de mensajes (si está disponible) desde otro miembro del clúster.

Método viewAccepted(View new_view):
Este método se activa cada vez que ocurre un cambio en el clúster, como cuando un nodo se une o sale. Simplemente imprime la vista actual del clúster.

Método receive(Message msg):
Este método se invoca cada vez que se recibe un mensaje. Añade el mensaje al historial (state) y lo imprime en la consola.


Bucle de Evento eventLoop():
Este bucle permite al usuario ingresar mensajes desde la consola. Cada mensaje se envía como un ObjectMessage al canal, que luego lo distribuye a todos los demás miembros del clúster.

Gestión de Estado:

getState(OutputStream output): Serializa el historial de mensajes (state) y lo envía a nuevos nodos que se unan al clúster.
setState(InputStream input): Recibe el historial de mensajes de otro nodo al unirse, lo deserializa y lo añade al historial local.


Aquí tienes una descripción para el archivo README.md que explica el código de SimpleChat, una aplicación de chat simple utilizando JGroups para la comunicación distribuida:

SimpleChat - Chat Distribuido con JGroups
Este proyecto implementa una aplicación de chat distribuido que utiliza JGroups para la comunicación entre nodos. Cada instancia del chat se une a un clúster llamado ChatCluster y se comunica con otros nodos, compartiendo mensajes en tiempo real. Además, el estado (historial de mensajes) es replicado entre los nodos, permitiendo que los nuevos miembros del clúster sincronicen el historial existente.

Descripción del Código
La clase SimpleChat implementa la interfaz Receiver de JGroups, lo que permite recibir mensajes y gestionar eventos de vista (como cambios en el clúster).

Componentes Principales
Inicialización del Canal de JGroups:
Al iniciar, la aplicación crea un canal (JChannel) y se conecta al clúster ChatCluster. Luego, solicita el estado del historial de mensajes (si está disponible) desde otro miembro del clúster.

Método viewAccepted(View new_view):
Este método se activa cada vez que ocurre un cambio en el clúster, como cuando un nodo se une o sale. Simplemente imprime la vista actual del clúster.

Método receive(Message msg):
Este método se invoca cada vez que se recibe un mensaje. Añade el mensaje al historial (state) y lo imprime en la consola.

Bucle de Evento eventLoop():
Este bucle permite al usuario ingresar mensajes desde la consola. Cada mensaje se envía como un ObjectMessage al canal, que luego lo distribuye a todos los demás miembros del clúster.

Gestión de Estado:

getState(OutputStream output): Serializa el historial de mensajes (state) y lo envía a nuevos nodos que se unan al clúster.
setState(InputStream input): Recibe el historial de mensajes de otro nodo al unirse, lo deserializa y lo añade al historial local.
Ejecución
Cada instancia del chat inicia una sesión de usuario y se conecta al clúster. Los mensajes se envían y reciben en tiempo real, y los nuevos usuarios sincronizan el historial de mensajes automáticamente al unirse.
