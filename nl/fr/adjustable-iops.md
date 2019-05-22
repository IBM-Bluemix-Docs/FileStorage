---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords: File Storage, adjusting IOPS, increase IOPS, decrease IOPS, modify IOPS

subcollection: FileStorage

---
{:external: target="_blank" .external}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Ajustement des IOPS (opérations d'entrée-sortie par seconde)
{: #adjustingIOPS}

Cette nouvelle fonctionnalité permet aux utilisateurs du stockage {{site.data.keyword.filestorage_full}} d'ajuster immédiatement les IOPS de leur {{site.data.keyword.filestorage_short}} existant. Ils n'ont pas besoin de créer un doublon ou de copier manuellement les données vers un nouveau stockage. Les utilisateurs ne sont confrontés à aucune indisponibilité, ni manque d'accès au stockage lorsque l'ajustement a lieu.

La facturation du stockage est mise à jour : la différence calculée au prorata du nouveau prix est ajoutée au cycle de facturation en cours. Le nouveau montant total est facturé dans le cycle de facturation suivant.


## Avantages des IOPS ajustables

- Gestion des coûts – Certains clients ont besoin d'un nombre élevé d'IOPS uniquement pendant les pics d'utilisation. Par exemple, un grand magasin de détail connaît un pic d'utilisation pendant les jours fériés et peut alors souhaiter bénéficier d'un nombre d'IOPS plus élevé sur son stockage que par rapport au milieu de l'été. Cette fonctionnalité lui permet de gérer ses coûts et de payer pour un nombre d'IOPS plus élevé uniquement en cas de besoin.

## Limitations
{: #limitsofadjustIOPS}

Cette fonctionnalité est disponible uniquement dans des [centres de données sélectionnés](/docs/infrastructure/FileStorage?topic=FileStorage-news).

Les clients ne peuvent pas basculer entre les volumes Endurance et Performance lorsqu'ils ajustent leurs IOPS. Les utilisateurs peuvent indiquer un nouveau niveau d'IOPS pour leur stockage en fonction des restrictions et critères suivants :

- Si le volume d'origine est de type Endurance avec un niveau de 0,25, il n'est pas possible de le mettre à jour.
- Si le volume d'origine est de type Performance avec un niveau inférieur ou égal à 0,30 IOPS/Go, les options disponibles incluent uniquement les combinaisons de taille et d'IOPS qui génèrent un niveau inférieur ou égal à 0,30 IOPS/Go.
- Si le volume d'origine est de type Performance avec un niveau supérieur à 0,30 IOPS/Go, les options disponibles incluent uniquement les combinaisons de taille et d'IOPS qui génèrent un niveau supérieur à 0,30 IOPS/Go.

## Effet de l'ajustement des IOPS sur la réplication

Si la réplication est activée sur le volume, la réplique est automatiquement mise à jour afin de correspondre à la sélection des IOPS du volume principal.

## Ajustement des IOPS sur votre stockage
{: #adjustingsteps}

1. Accédez à votre liste de {{site.data.keyword.filestorage_short}}
    - A partir du portail client, cliquez sur **Storage** > **{{site.data.keyword.filestorage_short}}** OU
    - A partir de la console {{site.data.keyword.BluSoftlayer_full}}, cliquez sur **Infrastructure** > **Stockage** > **{{site.data.keyword.filestorage_short}}**.
2. Sélectionnez le volume dans la liste et cliquez sur **Actions** > **Modifier le volume**
3. Sous les options d'IOPS de stockage, effectuez une nouvelle sélection :
    - Pour Endurance (IOPS hiérarchisées), sélectionnez un niveau d'IOPS supérieur à 0,25 IOPS/Go de votre stockage. Vous pouvez augmenter le niveau d'IOPS à tout moment. Toutefois, vous ne pouvez le diminuer qu'une seule fois par mois.
    - Pour Performance (IOPS allouées), indiquez la nouvelle option d'IOPS pour votre stockage en saisissant une valeur comprise entre 100 et 48 000 IOPS. (Prenez soin de tenir compte des limites spécifiques requises par la taille dans le formulaire de commande.)
4. Vérifiez votre sélection et la nouvelle tarification.
5. Cochez la case **J'ai lu et j'accepte l'intégralité du Contrat cadre de service**, puis cliquez sur **Valider la commande**.
6. Votre nouvelle allocation de stockage est disponible en quelques minutes.

Vous pouvez également mettre à jour votre IOPS via l'interface SLCLI.
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
