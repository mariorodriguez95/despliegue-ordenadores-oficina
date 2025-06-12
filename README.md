PROYECTO: CONFIGURACIÓN BASE DE ORDENADORES DE OFICINA CON ANSIBLE
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESUMEN

Este proyecto consiste en automatizar la configuración inicial del número de ordenadores que sea de oficina mediante Ansible desde un nodo controlador. El objetivo es crear un usuario único en cada ordenador, instalar software común y aplicar configuraciones básicas del sistema.

OBJETIVOS

Crear un usuario individual asignado a cada equipo.
Instalar software básico necesario para la oficina.
Configurar parámetros comunes como idioma y zona horaria.
TECNOLOGÍAS UTILIZADAS
Sistemas operativos: Linux (Ubuntu o similar) en nodos y controlador
Herramientas: Ansible
Automatización: playbooks, roles, archivos de variables

PREPARACIÓN DEL ENTORNO

Configurar el nodo controlador con Ansible instalado.
Asegurar acceso SSH sin contraseña a cada uno de los ordenadores.
Crear archivo de inventario con los nodos y sus ips.

CREACIÓN DE LA ESTRUCTURA DE ANSIBLE

ansible-office-setup/inventory/hosts.ini
ansible-office-setup/playbook.yml
ansible-office-setup/users_map.yml
ansible-office-setup/group_vars/all.yml
roles/users/tasks/main.yml
roles/packages/tasks/main.yml

DEFINICIÓN DEL INVENTARIO (inventory/hosts.ini)

En este archivo se listan los 50 ordenadores con sus IPs y se configuran variables comunes como el usuario con el que Ansible se conectará y la ruta de la clave privada SSH.

DEFINICIÓN DEL MAPEADO USUARIOS-HOST (users_map.yml)

Se crea una lista que asocia cada ordenador con su usuario único, por ejemplo: pc01 con ana, pc02 con pedro, etc., hasta los 50 equipos.

VARIABLES COMUNES (group_vars/all.yml)

Se define la lista de paquetes comunes que se instalarán en todos los ordenadores, como firefox, libreoffice, gedit, curl y htop.

PLAYBOOK PRINCIPAL (playbook.yml)

Se define un playbook que se ejecuta en todos los nodos, con privilegios elevados, e incluye los roles 'users' y 'packages'. Además se cargan las variables del archivo de usuarios.

ROL USERS (roles/users/tasks/main.yml)

Este rol se encarga de crear en cada ordenador el usuario único asignado comparando el nombre del host con el listado de usuarios y creando el usuario correspondiente con shell bash y permisos sudo.

ROL PACKAGES (roles/packages/tasks/main.yml)

Este rol instala todos los paquetes comunes definidos en las variables, actualizando primero la caché de paquetes y asegurando su instalación.

EJECUCIÓN

Desde el nodo controlador se ejecuta el playbook usando ansible-playbook apuntando al inventario y al playbook principal.

VERIFICACIÓN

Se comprueba que en cada ordenador se haya creado el usuario correcto y que los programas comunes estén instalados correctamente. También se verifican las configuraciones básicas aplicadas.

LECCIONES APRENDIDAS

Automatización: cómo gestionar usuarios y software en múltiples nodos con roles de Ansible.

Gestión de inventarios: uso de archivos YAML para mapear ordenadores y usuarios.

Escalabilidad: configurar varios equipos desde un solo punto de control simplifica el mantenimiento.
