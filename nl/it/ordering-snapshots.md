---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Ordinazione di istantanee

Per creare le istantanee del tuo volume di archiviazione, in modo automatizzato o manualmente, devi acquistare dello spazio per contenerle. Puoi acquistare capacità fino alla tua quantità di volume di archiviazione (durante l'acquisto di volume iniziale e successivamente attenendoti a questa procedura). 

1. Accedi alla tua archiviazione tramite la scheda **Storage** > **{{site.data.keyword.filestorage_short}}** del [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}
2. Nel frame **Snapshots**, fai clic su **Add Snapshot Space**.
3. Nel frame **Snapshots**, fai clic su **Purchase snapshot space now**. 
3. Seleziona la quantità di spazio che ti serve. 
4. Fai clic su **Continue**.
5. Immetti l'eventuale codice promozionale (Promo Code) a tua disposizione e fai clic su **Recalculate**. Gli addebiti per quest'ordine (**Charges for this order**) e il riesame dell'ordine (**Order Review**) presentano i valori predefiniti. 
6. Fai clic sulla casella di spunta **I have read the Master Service Agreement…** e fai clic su **Place Order**. Nel giro di pochi minuti, verrà eseguito il provisioning del tuo spazio per le istantanee.

## Come determinare quanto spazio di istantanea ordinare 

Purtroppo non c'è una prassi ottimale quanto piuttosto una migliore raccomandazione basata sull'applicazione. In linea generale, lo spazio di istantanea viene utilizzato dalle istantanee in base a due informazioni chiave: 
- a quante modifiche è soggetto il tuo file system attivo e 
- per quanto tempo prevedi di conservare le istantanee.  

Essenzialmente, il modo per calcolare la quantità di spazio necessaria è **(Frequenza di modifica)** x **(numero di ore/giorni/settimane/mesi di conservazione)**.  
**Nota**: la primissima istantanea utilizza una quantità trascurabile di spazio poiché è solo una copia dei metadati (puntatori) che indicano i blocchi di file system attivi.  

Un volume con molte modifiche ai dati (ad esempio un database con un'elevata frequenza di modifica) e un lungo periodo di conservazione delle istantanee richiederà più spazio per le istantanee di un volume con una moderata frequenza di modifica (ad esempio, un archivio dati di VM) e una pianificazione di conservazione delle istantanee più moderata.  

Se tu dovessi acquisire 12 istantanee orarie di un volume che contiene 500 GB di dati reali e vedi l'1 percento di modifica tra ciascuna istantanea, ti ritroveresti alla fine ad utilizzare 60 GB per le istantanee.

*(Frequenza di modifica 5 GB) x (12 istantanee orarie) = 60 GB*

Se invece per quei 500 GB di dati effettivi, con 12 istantanee orarie, si verificasse un 10 percento di modifica ogni ora, ti ritroveresti alla fine ad utilizzare 600 GB.

*(Frequenza di modifica 50 GB) x (12 istantanee orarie) = 600 GB*

Pertanto, quanto determini la quantità di spazio di istantanea di cui hai bisogno, considera attentamente la frequenza di modifica. È un fattore che ha un enorme impatto sulla quantità di spazio di istantanea di cui hai bisogno. Mentre la dimensione di un volume si tradurrà probabilmente in una maggiore quantità di modifica, un volume di 500 GB con 5 GB di modifica e un volume di 10 TB con 5 GB di modifica comporterebbero lo stesso utilizzo di spazio di istantanea. 

Inoltre, per la maggior parte dei carichi di lavoro, più grande è un volume e minore è lo spazio da mettere da parte inizialmente per le istantanee.  Ciò è dovuto principalmente all'efficienza dei dati sottostanti della nostra piattaforma, e alla natura della modalità di funzionamento delle istantanee nel nostro ambiente. 


