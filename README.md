<h2>Sistema de inventario, alertas y restauración de imágenes con GLPI:</h2>

El proyecto consistirá en implementar una herramienta de gestión de inventario, que en este caso será GLPI con varias funcionalidades añadidas. Este sistema estará diseñado para recopilar información sobre todos los equipos dentro de la red con la ayuda de OCS Inventory. También implementaremos un sistema de ticketing para recoger todas las incidencias que ocurran en los clientes.

Además de la gestión y monitoreo continuo de los equipos, queremos añadir la implementación de un sistema de respaldo y restauración de imágenes en los ordenadores. Utilizaremos FOG Project, una herramienta que puede implementar imágenes de disco utilizando el entorno de ejecución de prearranque. Esto asegurará la disponibilidad y la rápida recuperación de los datos en caso de fallos o incidentes. 

Para fortalecer más la seguridad de la red, también se contempla la implementación de una herramienta de análisis de vulnerabilidades automática. Utilizaremos Nessus, que proporcionará escaneos automatizados de vulnerabilidades en los sistemas de la red, permitiendo la identificación automática de posibles debilidades en el software y la configuración de los equipos.

Separaremos los clientes por grupos como si fuera una escuela (Profesor, DAM, DAW, ASIX…) y en función de esta clasificación, automatizar qué sistema operativo, softwares y configuraciones tendrá cada dispositivo para que así, en caso de instalar un nuevo equipo, solamente con indicar a qué grupo pertenece, se configure de la forma más rápida y automática posible.

--------------------------------------------------------------------------------------------------

<h2>Inventory System with Alerts and Image Restoration using GLPI:</h2>


The project will consist of implementing an inventory management tool, which in this case will be GLPI with several added functionalities. This system will be designed to gather detailed information about the hardware, software, and network status of all devices within the network with the help of OCS Inventory. Additionally, an alert system will be integrated to identify and record any abnormal or unauthorized behavior of the devices, thus providing a more comprehensive control.

In addition to the ongoing management and monitoring of devices, we aim to implement a system for backup and image restoration on computers. We will utilize FOG Project, a tool that can deploy disk images using the pre-boot execution environment. This will ensure data availability and quick recovery in case of failures or incidents.

To further strengthen network security, the implementation of an automatic vulnerability analysis tool is also considered. Our primary choice is OpenVAS, which will provide automated vulnerability scans on network systems, allowing for the automatic identification of potential weaknesses in software and equipment configurations.

Our intention is to separate clients into groups similar to a school (Teacher, DAM, DAW, ASIX…) and based on this classification, automate the operating system, software, and configurations for each device so that when installing a new device, simply indicating its group will configure it in the fastest and most automated way possible.
