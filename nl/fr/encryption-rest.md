---

copyright:
  years: 2014, 2019
lastupdated: "2019-06-18'"

keywords: File Storage, file storage, NFS, security, encryption

subcollection: FileStorage

---
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Chiffrement au repos géré par le fournisseur
{: #encryption}

{{site.data.keyword.cloud}} prend très au sérieux la question de la sécurité et comprend l'importance du chiffrement des données pour assurer leur sécurité. Grâce au chiffrement géré par le fournisseur, {{site.data.keyword.filestorage_full}}, mis à disposition avec un niveau Endurance ou Performance, est chiffré par défaut sans coût supplémentaire et sans impact sur les performances.

Le chiffrement au repos géré par le fournisseur utilise les protocoles suivants conformes aux normes de l'industrie :

* Chiffrement AES-256 conforme aux normes de l'industrie
* Gestion en interne des clés via le protocole conforme aux normes de l'industrie KMIP (Key Management Interoperability Protocol)
* Le stockage est validé par rapport aux normes suivantes :
    - Federal Information Processing Standard (FIPS) Publication 140-2
    - Federal Information Security Management Act (FISMA)
    - Health Insurance Portability and Accountability Act (HIPAA)
    - Payment Card Industry (PCI)
    - Bâle II
    - California Security Breach Information Act (SB 1386)
    - Conformité à la directive européenne concernant la protection des données (95/46/EC).

## Sécurisation de vos instantanés ou de votre stockage répliqué.  

Tous les instantanés et toutes les répliques d'un stockage de fichier chiffré sont également chiffrés par défaut. Il est impossible de désactiver cette fonctionnalité volume par volume.

## Mise à disposition du stockage avec chiffrement

La fonction de chiffrement au repos géré par le fournisseur est disponible dans des [centres de données sélectionnés](/docs/infrastructure/FileStorage?topic=FileStorage-selectDC). La totalité du stockage commandé dans ces centres de données est automatiquement doté du chiffrement des données au repos.

Lorsque vous commandez {{site.data.keyword.filestorage_short}}, sélectionnez un centre de données signalé par un astérisque (`*`). Une icône en forme de verrou figure à droite de la zone Nom du volume pour indiquer que le volume est chiffré. Voir la Figure 1.

![L'icône en forme de verrou indique que le volume est chiffré](/images/encryptedstorage.png)
<caption>Figure 1. Exemple d'icône en forme de verrou indiquant que le volume est chiffré.</caption>

Un stockage non chiffré mis à disposition avant la mise à niveau d'un centre de données **n'est pas** automatiquement chiffré. Si vous disposez d'un stockage non chiffré dans un centre de données mis à niveau et que vous souhaitez le chiffrer, vous devez créer un volume et déplacer vos données. Pour plus d'informations, voir [Migration de stockage de fichier dans des centres de données mis à niveau](/docs/infrastructure/FileStorage?topic=FileStorage-migratestorage)
{:important}