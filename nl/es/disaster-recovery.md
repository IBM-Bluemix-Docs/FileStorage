---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-10"

keywords: File Storage, file storage, NFS, disaster recovery, duplicate volume, replica volume, failover, failback,

subcollection: FileStorage

---
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}


# Recuperación tras desastre: migración tras error con un volumen primario inaccesible
{: #dr-inaccessible}

Si un error catastrófico o un desastre ocasionan la caída del sitio principal, los clientes pueden llevar a cabo las siguientes acciones para acceder rápidamente a sus datos en el sitio secundario.

## Migración tras error con un duplicado de un volumen de réplica en el sitio secundario

1. Inicie la sesión en la [consola de {{site.data.keyword.cloud}}](https://{DomainName}/){: external} y pulse el icono de **menú** de la parte superior izquierda. Seleccione **Infraestructura clásica**.
2. Pulse **Almacenamiento** > **{{site.data.keyword.filestorage_short}}**.
3. Pulse en la réplica de la compartición de archivos de la lista para visualizar su página de **Detalles**.
4. En la página **Detalles**, desplácese hacia abajo y seleccione una instantánea existente; luego pulse **Acciones** > **Duplicar**.
5. Realice las actualizaciones necesarias en la capacidad (para aumentar el tamaño) o en IOPS para el nuevo volumen.
6. Puede actualizar el espacio de instantáneas para el nuevo volumen si es necesario.
7. Pulse **Continuar** para realizar el orden de los duplicados.

Tan pronto como se haya creado el volumen podrá adjuntarlo a un host y realizar operaciones de lectura/escritura sobre dicho volumen. Mientras los datos se estén copiando desde el volumen original en el duplicado, puede ver un estado en la página de detalles que muestra que la duplicación está en curso. Cuando se complete el proceso de duplicación, el nuevo volumen pasa a ser independiente del original y se puede gestionar con instantáneas y réplica, como es habitual.

## Restablecimiento del sitio primario original

Si desea devolver la producción al sitio primario original, debe seguir los pasos siguientes.

1. Inicie la sesión en la [consola de {{site.data.keyword.cloud}}](https://{DomainName}/){: external} y pulse el icono de **menú** de la parte superior izquierda. Seleccione **Infraestructura clásica**.
2. Pulse **Almacenamiento** > **{{site.data.keyword.filestorage_short}}**.
3. Pulse el nombre del volumen y cree una planificación de instantánea (si no hay ya una).

   Para obtener más información sobre la planificación de instantáneas, consulte [Gestión de instantáneas](/docs/infrastructure/FileStorage?topic=FileStorage-managingSnapshots#addschedule).
   {:tip}
4. Pulse **Réplica** y pulse **Adquirir una réplica**.
5. Seleccione la planificación de instantáneas existente que quiera que siga la réplica. La lista contiene todas las planificaciones de instantáneas activas.
6. Pulse **Ubicación** y seleccione el centro de datos que era el sitio de producción original.
7. Pulse **Continuar**.
8. Marque el recuadro de selección **He leído el Acuerdo de servicio maestro…** y pulse **Realizar pedido**.

Una vez finalizada la réplica, tiene que crear un volumen duplicado de la nueva réplica.
{:important}

1. Vuelva a **Almacenamiento** > **{{site.data.keyword.filestorage_short}}**.
2. Pulse la réplica del volumen en la lista para ver su página **Detalles**.
3. En la página **Detalles**, desplácese hacia abajo y seleccione una instantánea existente; luego pulse **Acciones** > **Duplicar**.
4. Realice las actualizaciones necesarias en la capacidad (para aumentar el tamaño) o en IOPS para el nuevo volumen.
5. Actualice el espacio de instantánea para el nuevo volumen si es necesario.
6. Pulse **Continuar** para realizar el orden de los duplicados.

Cuando finalice el proceso de duplicación, puede cancelar la réplica y los volúmenes utilizados para devolver los datos al sitio primario original. El duplicado se convierte en el almacenamiento primario y se puede volver a establecer la réplica en el sitio secundario original.
