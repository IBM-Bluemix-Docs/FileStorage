---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

keywords: File Storage, file storage, NFS, disaster recovery, duplicate volume, replica volume, failover, failback,

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}


# Disaster-Recovery - Failover mit einem nicht zugänglichen Primärdatenträger
{: #dr-inaccessible}

Wenn eine Betriebsunterbrechung oder eine Katastrophe einen Ausfall am primären Standort verursachen, können Kunden die folgenden Aktionen ausführen, um schnell am sekundären Standort auf ihre Daten zuzugreifen.

## Failover mit dem Duplikat eines Replikatdatenträgers am sekundären Standort

1. Melden Sie sich an [der IBM Cloud-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/){:new_window} an und klicken Sie oben links auf das Symbol **Menü**. Wählen Sie **Klassische Infrastruktur** aus.

   Alternativ können Sie sich beim [{{site.data.keyword.slportal}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){:new_window} anmelden.
2. Klicken Sie auf **Speicher** > **{{site.data.keyword.filestorage_short}}**.
3. Klicken Sie in der Liste auf das Replikat der gemeinsam genutzten Dateiressource, um die zugehörige Seite **Details** anzuzeigen.
4. Blättern Sie auf der Seite **Details** nach unten und wählen Sie einen vorhandenen Snapshot aus. Klicken Sie anschießend auf **Aktionen** > **Duplikat**.
5. Nehmen Sie die erforderlichen Aktualisierungen für die Kapazität (Größe erhöhen) oder die IOPs für den neuen Datenträger vor.
6. Sie können den Snapshotbereich bei Bedarf für den Datenträger aktualisieren.
7. Klicken Sie auf **Weiter**, um Ihre Bestellung für das Duplikat abzuschicken.

Sobald der Datenträger erstellt wurde, können Sie ihn einem Host zuordnen und Lese- und Schreiboperationen auf diesem Datenträger vornehmen. Während Daten vom ursprünglichen Datenträger auf den Duplikatdatenträger kopiert werden, wird auf der Detailseite ein Status mit der Information angezeigt, dass die Duplizierung in Bearbeitung ist. Wenn der Duplizierungsprozess abgeschlossen ist, ist der neue Datenträger unabhängig vom Original und kann mit Snapshots und Replikation normal verwaltet werden.

## Rückübertragung an den ursprünglichen primären Standort

Wenn Sie die Produktion an den ursprünglichen primären Standort zurückgeben möchten, müssen Sie die folgenden Schritte ausführen.

1. Melden Sie sich an [der IBM Cloud-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/){:new_window} an und klicken Sie oben links auf das Symbol **Menü**. Wählen Sie **Klassische Infrastruktur** aus.

   Alternativ können Sie sich beim [{{site.data.keyword.slportal}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){:new_window} anmelden.
2. Klicken Sie auf **Speicher** > **{{site.data.keyword.filestorage_short}}**.
3. Klicken Sie auf den LUN-Namen und erstellen Sie einen Snapshotplan (falls noch keiner vorhanden ist).

   Weitere Informationen zu Snapshotplänen finden Sie unter [Snapshots verwalten](/docs/infrastructure/FileStorage?topic=FileStorage-managingSnapshots#addschedule).
   {:tip}
4. Klicken Sie auf **Replikat** und auf **Replikation kaufen**.
5. Wählen Sie einen vorhandenen Snapshotplan aus, den die Replikation befolgen soll. Die Liste enthält alle aktiven Snapshotpläne.
6. Klicken Sie auf **Position** und wählen Sie das Rechenzentrum aus, das der ursprüngliche Produktionsstandort war.
7. Klicken Sie auf **Weiter**.
8. Klicken Sie auf das Kontrollkästchen **Ich habe die Rahmenvereinbarung gelesen** und klicken Sie auf **Bestellung abschicken**.

Nach Abschluss der Replikation müssen Sie ein Duplikat des Datenträgers des neuen Replikats erstellen.
{:important}

1. Gehen Sie zurück zu **Speicher** > **{{site.data.keyword.filestorage_short}}**.
2. Klicken Sie auf das Replikat der LUN in der Liste, um die zugehörige Seite **Details** anzuzeigen.
3. Blättern Sie auf der Seite **Details** nach unten und wählen Sie einen vorhandenen Snapshot aus. Klicken Sie anschießend auf **Aktionen** > **Duplikat**.
4. Nehmen Sie die erforderlichen Aktualisierungen für die Kapazität (Größe erhöhen) oder die IOPs für den neuen Datenträger vor.
5. Aktualisieren Sie bei Bedarf den Snapshotbereich für den neuen Datenträger.
6. Klicken Sie auf **Weiter**, um Ihre Bestellung für das Duplikat abzuschicken.

Wenn der Duplizierungsprozess abgeschlossen ist, können Sie die Replikation und die Datenträger stornieren, die verwendet wurden, um die Daten wieder an den ursprünglichen primären Standort zu bringen. Das Duplikat wird zum primären Speicher, und die Replikation auf den ursprünglichen sekundären Standort kann wieder eingerichtet werden.
