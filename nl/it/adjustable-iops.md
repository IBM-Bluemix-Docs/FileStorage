---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-24"

keywords: File Storage, adjusting IOPS, increase IOPS, decrease IOPS, modify IOPS

subcollection: FileStorage

---
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Regolazione dell'IOPS
{: #adjustingIOPS}

Con questa nuova funzione, gli utenti dell'archiviazione {{site.data.keyword.filestorage_full}} possono regolare l'IOPS del loro {{site.data.keyword.filestorage_short}} esistente immediatamente. Non hanno bisogno di creare un duplicato o copiare manualmente i dati nella nuova archiviazione. Gli utenti non riscontrano alcun tipo di interruzione o mancanza di accesso all'archiviazione mentre viene eseguita la regolazione.

La fatturazione per l'archiviazione viene aggiornata per aggiungere la differenza calcolata proporzionalmente del nuovo prezzo al ciclo di fatturazione corrente. La nuova quantità completa viene fatturata nel ciclo di fatturazione successivo.


## Vantaggi dell'IOPS regolabile

- Gestione dei costi – alcuni dei nostri clienti potrebbero avere bisogno di un IOPS elevato solo durante i tempi di utilizzo di picco. Ad esempio, un grosso negozio al dettaglio ha un utilizzo di picco durante i periodi festivi e potrebbe avere bisogno di un IOPS sulla sua archiviazione più elevato rispetto a quello necessario nel bel mezzo dell'estate. Questa funzione consente loro di gestire i loro costi e pagare un IOPS più elevato solo quando ne hanno bisogno.

## Limitazioni
{: #limitsofadjustIOPS}

Questa funzione è disponibile solo in [data center selezionati](/docs/infrastructure/FileStorage?topic=FileStorage-selectDC).

I clienti non possono passare da Endurance a Performance e viceversa quando regolano il loro IOPS. Gli utenti possono specificare un nuovo livello IOPS o un livello IOPS per la loro archiviazione sulla base dei seguenti criteri e delle seguenti limitazioni.

- Se il volume originale è un livello Endurance 0,25, il livello IOPS non può essere aggiornato.
- Se il volume originale è Performance con meno di, o uguale a, 0,30 IOPS/GB, le opzioni disponibili includono solo le combinazioni di dimensione e IOPS che danno come risultato meno di, o uguale a, 0,30 IOPS/GB.
- Se il volume originale è Performance con più di 0,30 IOPS/GB, le opzioni disponibili includono solo le combinazioni di dimensione e IOPS che danno come risultato più di 0,30 IOPS/GB.

## Effetto della regolazione dell'IOPS sulla replica

Se per il volume è implementata la replica, quest'ultima viene aggiornata automaticamente in modo che corrisponda alla selezione IOPS di quello primario.

## Regolazione dell'IOPS sulla tua archiviazione
{: #adjustingsteps}

1. Vai al tuo elenco di {{site.data.keyword.filestorage_short}}. Dalla console {{site.data.keyword.cloud}}, fai clic su **Classic Infrastructure** > **Storage** > **{{site.data.keyword.filestorage_short}}**.
2. Seleziona il volume dall'elenco e fai clic su **...** > **Modify Share**
3. In **Storage IOPS Options**, effettua una nuova selezione:
    - Per Endurance (IOPS a livelli), seleziona un livello IOPS superiore a 0,25 IOPS/GB della tua archiviazione. Puoi aumentare il livello IOPS in qualsiasi momento. Tuttavia, la diminuzione è disponibile solo una volta al mese.
    - Per Performance (IOPS allocato), specifica la nuova opzione IOPS per la tua archiviazione immettendo un valore compreso nell'intervallo 100 - 48.000 IOPS. (Assicurati di esaminare gli eventuali limiti specifici richiesti in base alla dimensione nel modulo dell'ordine).
4. Riesamina la tua selezione e la nuova determinazione del prezzo.
5. Fai clic sulla casella di spunta **I have read the Master Service Agreement...** e fai clic su **Place Order**.
6. La tua nuova allocazione di archiviazione è disponibile in pochi minuti.

In alternativa, puoi aggiornare il tuo IOPS tramite la SLCLI.
```
# slcli file volume-modify --help
Usage: slcli file volume-modify [OPTIONS] VOLUME_ID

Options:
  -c, --new-size INTEGER        New Size of file volume in GB. ***If no size
                                is given, the original size of volume is
                                used.***
                                Potential Sizes: [20, 40, 80, 100,
                                250, 500, 1000, 2000, 4000, 8000, 12000]
                                Minimum: [the original size of the volume]
  -i, --new-iops INTEGER        Performance Storage IOPS, between 100 and 6000
                                in multiples of 100 [only for performance
                                volumes] ***If no IOPS value is specified, the
                                original IOPS value of the volume will be
                                used.***
                                Requirements: [If original IOPS/GB
                                for the volume is less than 0.3, new IOPS/GB
                                must also be less than 0.3. If original
                                IOPS/GB for the volume is greater than or
                                equal to 0.3, new IOPS/GB for the volume must
                                also be greater than or equal to 0.3.]
  -t, --new-tier [0.25|2|4|10]  Endurance Storage Tier (IOPS per GB) [only for
                                endurance volumes] ***If no tier is specified,
                                the original tier of the volume will be
                                used.***
                                Requirements: [If original IOPS/GB
                                for the volume is 0.25, new IOPS/GB for the
                                volume must also be 0.25. If original IOPS/GB
                                for the volume is greater than 0.25, new
                                IOPS/GB for the volume must also be greater
                                than 0.25.]
  -h, --help      Show this message and exit.
```
