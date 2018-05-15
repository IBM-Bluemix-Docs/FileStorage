---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Istantanee

Le istantanee sono una funzione di {{site.data.keyword.filestorage_full}}. Un'istantanea rappresenta il contenuto di un volume a uno specifico punto temporale. Le istantanee ti consentono di proteggere i tuoi dati senza ripercussioni sulle prestazioni, con un consumo minimo di spazio e sono considerate la prima linea di difesa per la protezione dei dati. Con la funzione di istantanea, se un utente modifica o elimina accidentalmente dei dati cruciali da un volume può ripristinarli in modo facile e veloce da una copia istantanea.

{{site.data.keyword.filestorage_short}} ti fornisce due modi per acquisire le tue istantanee: uno consiste in una pianificazione delle istantanee configurabile che crea ed elimina le copie di istantanea automaticamente per ciascun volume di archiviazione. Puoi anche creare delle pianificazioni delle istantanee aggiuntive, eliminare manualmente delle copie e gestire le pianificazioni in base ai tuoi requisiti. Il secondo modo consiste nell'acquisire un'istantanea manuale.

Una copia istantanea è un'immagine di sola lettura di un volume {{site.data.keyword.filestorage_short}} che acquisisce lo stato del volume a un punto temporale. Le copie istantanea sono estremamente efficienti sia per quanto riguarda il tempo necessario per crearle che per quanto riguarda lo spazio di archiviazione. La creazione di una copia istantanea {{site.data.keyword.filestorage_short}} impiega solo pochi secondi, di norma meno di 1 secondo, indipendentemente dalla dimensione del volume o dal livello di attività sull'archiviazione. Dopo che una copia istantanea è stata creata, le modifiche agli oggetti di dati sono riflesse negli aggiornamenti alla versione corrente degli oggetti, come se le copie istantanea non esistessero. Nel frattempo, la copia dei dati rimane completamente stabile. 

Una copia istantanea non comporta alcun sovraccarico delle prestazioni; gli utenti possono facilmente archiviare fino a 50 istantanee pianificate e 50 istantanee manuali per volume {{site.data.keyword.blockstorageshort}}, tutte accessibili come versioni di sola lettura e online dei dati.

Le istantanee consentono agli utenti di

- Creare, in un modo che non interrompe le operazioni, dei punti di ripristino a un punto temporale
- Ripristinare i volumi a punti temporali precedenti
- Devi acquistare dello spazio per le istantanee per il tuo volume al fine di acquisirne delle istantanee. Lo spazio per le istantanee può essere aggiunto durante l'ordinazione di volumi iniziale o dopo il provisioning iniziale tramite la pagina Volume Details, facendo clic sul pulsante a discesa Actions e selezionando Add Snapshot Space. Tieni presente che le istantanee pianificate e manuali condividono lo spazio per le istantanee; ordina quindi il tuo spazio di conseguenza. Vedi l'articolo [Ordinazione di istantanee](ordering-snapshots.html) per ulteriori dettagli e istruzioni. 

## Prassi ottimali per le istantanee
La progettazione dell'istantanea dipende dall'ambiente del cliente. Le seguenti considerazioni sulla progettazione ti aiuteranno a pianificare e implementare copie istantanea. 
- 	Puoi creare fino a 50 istantanee tramite la pianificazione e fino a 50 manualmente su ogni volume o LUN. 
- 	Non acquisire troppe istantanee. Assicurati che la tua frequenza di istantanee pianificate soddisfi le tue esigenze di obiettivo del tempo di ripristino (RTO) e obiettivo del punto di ripristino (RPO) nonché i tuoi requisiti di business applicativi pianificando istantanee orarie, giornaliere o settimanali. 
- 	La funzione di eliminazione automatica (AutoDelete) di istantanea deve essere utilizzata per controllare la crescita del consumo dell'archiviazione. <br/>
    **Nota**: la soglia di AutoDelete è fissata al 95%.
    
## In che modo le copie di istantanee consumano spazio su disco?
Le copie istantanea riducono al minimo il consumo di disco preservando i singoli blocchi invece dei file interi. Le copie istantanea iniziano a consumare spazio extra solo quando i file nel file system attivo vengono modificati o eliminati. Quando ciò si verifica, i blocchi file originali continuano a essere conservati come parte di una o più copie istantanea.
Nel file system attivo, i blocchi modificati vengono riscritti in ubicazioni differenti sul disco oppure completamente rimossi come blocchi file attivi. Di conseguenza, oltre allo spazio su disco utilizzato dai blocchi nel file system attivo modificato, lo spazio su disco utilizzato dai blocchi originali continua a essere riservato per riflettere lo stesso del file system attivo prima della modifica.

<table>
    <colgroup>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
      <col style="width: 33.3%;"/>
    </colgroup>
    <tbody>
      <tr>
        <th colspan="3" style="border: 0.0px;text-align: center;">Utilizzo dello spazio su disco prima e dopo la copia istantanea</th>
     </tr><tr>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle1.png" alt="Prima della copia istantanea"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle3.png" alt="Dopo la copia istantanea"></td>
        <td style="border: 0.0px;text-align: center;"><img src="/images/bfcircle2.png" alt="Modifiche dopo la copia istantanea"></td>
     </tr><tr>
        <td style="border: 0.0px;">Prima che venga creata qualsiasi copia istantanea, lo spazio su disco è consumato solo dal file system attivo.</td>
        <td style="border: 0.0px;">Dopo la creazione di una copia istantanea, il file system attivo e la copia istantanea puntano agli stessi blocchi disco. La copia istantanea non usa spazio su disco extra.</td>
        <td style="border: 0.0px;">Dopo che <i>myfile.txt</i> è stato eliminato dal file system attivo, la copia istantanea continua a includere il file e i riferimenti ai suoi blocchi disco. Per tale motivo l'eliminazione dei dati del file system attivo non sempre libera spazio su disco.</td>
      </tr>
    </tbody>
</table>

Per visualizzare quando spazio di istantanea è utilizzato, attieniti alle istruzioni nel documento [Gestione delle istantanee](working-with-snapshots.html). 
