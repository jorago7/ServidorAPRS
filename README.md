# APRS Track Direct

**APRS Track Direct** es un conjunto de herramientas diseñadas para facilitar la creación y operación de un sitio web basado en APRS. Es compatible con datos de fuentes como APRS-IS, CWOP-IS, OGN y otros sistemas que cumplan con la especificación APRS.

Este conjunto incluye:

- **Recolector de Datos APRS**: Recopila datos desde fuentes compatibles con APRS.
- **Servidor WebSocket**: Facilita la comunicación en tiempo real.
- **Librería JavaScript**: Una librería versátil para operaciones del lado del cliente (incluye funcionalidad WebSocket y más).
- **Sitio Web de Ejemplo**: Una plantilla completamente funcional para un despliegue rápido o personalización adicional.

---

## ¿Qué es APRS?

El **Sistema Automático de Reporte de Paquetes (APRS, por sus siglas en inglés)** es un protocolo de comunicación digital utilizado por radioaficionados en todo el mundo para compartir información táctica en tiempo real.

Los datos típicos que se comparten a través de APRS incluyen:

- Coordenadas GPS, altitud, velocidad y rumbo.
- Mensajes, alertas y boletines.
- Reportes meteorológicos y datos de telemetría.

APRS permite que estaciones móviles, fijas y meteorológicas transmitan información en tiempo real sobre su estado y ubicación, utilizando infraestructura de radioaficionados y redes de internet interconectadas.

---

## Primeros Pasos

Siga estos pasos para configurar un entorno de desarrollo local o desplegar un sitio web público basado en APRS.

> **Nota:** Estas instrucciones son guías generales. Podrían requerirse ajustes según sus necesidades específicas. Se recomienda revisar el código fuente para comprender mejor su funcionamiento.

### Requisitos Previos

Asegúrese de tener instalados **Docker** y el complemento **Docker Compose**. Puede seguir la [guía oficial de instalación de Docker](https://docs.docker.com/engine/install/).

### Configuración

Edite los siguientes archivos de configuración según sus necesidades:

- `config/trackdirect.ini`: Configuración principal del recolector de datos APRS.
- `config/aprsc.conf`: Configuración del servidor APRS (si aplica).
- `config/postgresql.conf`: Parámetros de la base de datos PostgreSQL.

### Ejecución de la Aplicación

Ejecute el siguiente comando:

```bash
docker compose up

Si desea ejecutar el contenedor en segundo plano (modo daemon), agregue -d al comando y utilice:

bash
Copiar
Editar
docker compose logs -f
para visualizar la salida cuando lo desee. Para detener los contenedores, use:

bash
Copiar
Editar
docker compose down
Si todo está correctamente configurado, podrá abrir su navegador y acceder a: http://127.0.0.1.

Notas de Desarrollo
Librería JavaScript de Track Direct
La librería JavaScript de Track Direct proporciona todas las funcionalidades relacionadas con el mapa, incluyendo:

Renderizado de mapas mediante Google Maps API o Leaflet.

Comunicación en tiempo real con el servidor backend mediante WebSocket.

Soporte para funcionalidades interactivas, tales como:

Filtros por tipo de estación.

Visualización de trayectorias.

Información en ventanas emergentes (popups).

Actualización automática del estado de las estaciones.

Recompilación de la librería
Si realiza cambios en la librería (ubicada en el directorio jslib), debe reconstruirla para que los cambios se reflejen en el sitio web (htdocs). Para hacerlo:
```
pip3 install jsmin
~/trackdirect/jslib/build.sh
```
Esto comprimirá y copiará los archivos necesarios para que estén disponibles desde el frontend.


Adaptación del Sitio Web (htdocs)
El directorio htdocs contiene el sitio web de ejemplo listo para desplegar. Puede utilizarlo como base para su propia personalización o diseño.

Recomendaciones para producción:
Proveedor de mapas: Edite index.php para seleccionar entre Google Maps o Leaflet.

Estética: Personalice los íconos, colores, capas y controles según su identidad visual.

Filtros: Agregue filtros para mostrar estaciones específicas (vehículos, clima, balizas, etc.).

Términos de uso: Asegúrese de cumplir con los términos del proveedor de mapas si planea publicar el sitio web.

Mejora del Rendimiento de la Base de Datos
Para manejar grandes volúmenes de datos eficientemente, es importante ajustar los parámetros de PostgreSQL. Las siguientes configuraciones son recomendadas:
```
shared_buffers = 2048MB              # I recommend 25% of total RAM
synchronous_commit=off               # Avoid writing to disk for every commit
commit_delay=`100000`                # Will result in a 0.1s commit delay
```
💡 Nota: Estas configuraciones ya están predefinidas en la base de datos proporcionada por los contenedores Docker.

También puede considerar activar índices para las columnas más consultadas (como timestamp, callsign, latitude y longitude) si personaliza el esquema de la base de datos.

Contribuciones
¡Las contribuciones son bienvenidas! Puede:

Hacer un fork del repositorio.

Crear una nueva rama con su mejora.

Realizar un pull request.

Cualquier mejora en funcionalidad, documentación o corrección de errores es apreciada. ¡Gracias por apoyar este proyecto!

Descargo de Responsabilidad
Estas herramientas de software se proporcionan "tal cual" y "con todos sus defectos". No se ofrecen garantías sobre:

Seguridad.

Idoneidad para un propósito particular.

Errores u omisiones.

Componentes potencialmente dañinos.

Usted es el único responsable de:

Asegurar que los datos recopilados y publicados cumplan con las normativas de protección de datos aplicables.

La protección y respaldo de su infraestructura y datos.

El equipo de desarrollo no será responsable por daños directos o indirectos derivados del uso, modificación o distribución de este software.


