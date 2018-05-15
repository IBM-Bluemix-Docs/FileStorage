---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Instantáneas

Las instantáneas son una característica de {{site.data.keyword.filestorage_full}}. Una instantánea representa el contenido de un volumen en un momento específico. Las instantáneas le permiten proteger los datos sin afectar al rendimiento, con un consumo mínimo de espacio y son consideradas su primera línea de defensa para la protección de datos. Los datos se pueden restaurar de forma rápida y sencilla desde una copia de instantánea si un usuario modifica o suprime accidentalmente los datos de un volumen con la característica de instantánea.

{{site.data.keyword.filestorage_short}} le ofrece dos formas de realizar las instantáneas: mediante una planificación de instantáneas configurable que crea y suprime copias de instantáneas automáticamente para cada volumen de almacenamiento. También puede crear planificaciones de instantáneas adicionales, suprimir copias manualmente y gestionar las planificaciones en base a sus requisitos. La segunda forma es realizar una instantánea manual.

Una copia de instantánea es una imagen de solo lectura de un volumen de {{site.data.keyword.filestorage_short}}, que captura el estado del volumen en un momento específico. Las copias de instantáneas son extremadamente eficientes, por el tiempo necesario en crearlas y por el espacio de almacenamiento. Una copia de instantánea de {{site.data.keyword.filestorage_short}} solo tarda unos segundos en crearse - normalmente menos de 1 segundo, independientemente del tamaño del volumen o del nivel de actividad en el almacenamiento. Una vez creada una copia de instantánea, los cambios en los objetos de datos se reflejan en actualizaciones de la versión actual de los objetos, como si las copias de instantáneas no existieran. Mientras tanto, la copia de los datos permanece completamente estable. 

Una copia de instantánea no genera sobrecarga de rendimiento, los usuarios pueden almacenar fácilmente hasta 50 instantáneas planificadas y 50 instantáneas manuales por volumen de {{site.data.keyword.blockstorageshort}}, todas ellas accesibles como solo lectura y versiones online de los datos.

Las instantáneas permiten a los usuarios

- Crear puntos de recuperación de un punto en el tiempo sin interrupciones
- Revertir los volúmenes a puntos en el tiempo anteriores
- Debe adquirir cierta cantidad de espacio de instantáneas para su volumen para poder realizar instantáneas. El espacio de instantáneas se puede añadir durante el pedido de volumen inicial o después del suministro inicial, a través de la página Detalles y pulsando el botón desplegable Acciones y seleccionando Añadir espacio de instantáneas. Tenga en cuenta que las instantáneas planificadas y manuales comparten el espacio de instantáneas, realice el pedido del espacio en concordancia. Consulte el artículo [Realizar pedido de instantáneas](ordering-snapshots.html) para obtener más detalles y orientación.

## Prácticas recomendadas en torno a las instantáneas
El diseño de instantáneas depende del entorno del cliente. Las siguientes consideraciones de diseño le ayudarán a planificar e implementar copias de instantáneas: 
- 	Pueden crearse hasta 50 instantáneas a través de la planificación y hasta 50 manualmente en cada volumen o LUN. 
- 	No supere el máximo de instantáneas. Asegúrese de que la frecuencia de instantáneas planificadas cumpla sus necesidades de objetivo de tiempo de recuperación (RTO) y objetivo de punto de recuperación (RPO), así como los requisitos empresariales de las aplicaciones planificando las instantáneas por hora, a diario o semanalmente. 
- 	La opción de supresión automática de instantáneas debe utilizarse para controlar el crecimiento del consumo de almacenamiento. <br/>
    **Nota**: el umbral de supresión automática está fijado en 95%.
    
## ¿Cómo consumen espacio de disco las copias de instantáneas?
Las copias de instantáneas minimizan el consumo de disco conservando bloques individuales en lugar de archivos completos. Las copias instantáneas empiezan a consumir espacio adicional solo cuando se cambian o suprimen archivos en el sistema de archivos activo. Cuando esto sucede, los bloques de archivos originales aún se conservan como parte de una o más copias de instantáneas.
En el sistema de archivos activo, los bloques modificados se vuelven a escribir en diferentes ubicaciones del disco o se eliminan como bloques de archivos activos por completo. Como resultado, además del espacio de disco utilizado por los bloques en el sistema de archivos activo modificado, aún se reserva espacio de disco utilizado por los bloques originales para reflejar el estado del sistema de archivos activo antes del cambio.

<table>
    <colgroup>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
    </colgroup>
    <tbody>
      <tr>
        <th colspan="3" style="border: 0.0px;text-align: center;">Uso de espacio de disco antes y después de una copia de instantánea</th>
     </tr><tr>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle1.png" alt="Antes de una copia de instantánea"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle3.png" alt="Después de una copia de instantánea"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle2.png" alt="Cambios después de una copia de instantánea"></td>
     </tr><tr>
        <td style="border: 0.0px;">Antes de crear cualquier copia de instantánea, el espacio de disco solo es consumido por el sistema de archivos activo.</td>
        <td style="border: 0.0px;">Después de crear una copia de instantánea, el sistema de archivos activo y la copia de instantánea apuntan a los mismos bloques de discos. La copia de instantánea no utiliza espacio de disco adicional.</td>
        <td style="border: 0.0px;">Tras suprimir <i>myfile.txt</i> del sistema de archivos activo, la copia de instantánea aún incluye el archivo y hace referencia a sus bloques de discos. Por ello, suprimir los datos del sistema de archivos activo no siempre libera espacio de disco.</td>
      </tr>
    </tbody>
</table>

Para ver cuánto espacio de instantáneas se utiliza, siga las instrucciones del documento [Gestión de instantáneas](working-with-snapshots.html).
