---

copyright:
  years: 2014, 2018
lastupdated: "2018-06-29"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Commande d'instantanés

Pour créer des instantanés de votre volume de stockage, que ce soit de manière automatisée ou manuelle, vous devez acheter de l'espace dans lequel les conserver. Vous pouvez acquérir une capacité maximale pouvant atteindre la quantité de votre volume de stockage (lors de l'achat initial du volume ou ultérieurement en suivant les étapes ci-après).

1. Accédez à votre stockage via l'onglet **Stockage** > **{{site.data.keyword.filestorage_short}}** du portail [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}.
2. Dans le cadre **Instantanés**, cliquez sur le lien **Ajouter de l'espace d'instantané**.
3. Dans le cadre **Instantanés**, cliquez sur **Achetez maintenant de l'espace pour les instantanés**.
3. Sélectionnez la quantité d'espace dont vous avez besoin.
4. Cliquez sur **Continuer**.
5. Entrez un code promo le cas échéant et cliquez sur **Recalculer**. Les zones **Prix pour cette commande** et **Vérification de la commande** indiquent les valeurs par défaut.
6. Cochez la case **J'ai lu et j'accepte l'intégralité du Contrat cadre de service**, puis cliquez sur **Valider la commande**. Votre espace d'image instantanée est mis à disposition en quelques minutes.

## Calcul de la quantité d'espace d'image instantanée à commander

En règle générale, l'espace d'image instantanée est utilisé par les instantanés en fonction de deux critères essentiels :
- la quantité de modifications apportées à votre système de fichiers actif ;
- la durée de conservation envisagée des instantanés.  

La méthode de calcul de la quantité d'espace nécessaire est la suivante : **(taux de modification)** x **(nombre d'heures/de jours/de semaines/de mois de conservation)**.  
> **Remarque** : le premier instantané utilise une quantité négligeable d'espace car il s'agit uniquement d'une copie des métadonnées (pointeurs) indiquant les blocs du système de fichiers actif. 

Un volume comportant un nombre important de modifications et une longue période de conservation a besoin de davantage d'espace qu'un volume doté d'un taux moyen de modifications et d'un planning de conservation des instantanés modéré. Une base de données avec un nombre élevé de modifications illustre le premier type et un magasin de données VMware illustre le second type.

Si vous prenez 12 instantanés par heure de 500 Go de données réelles et qu'il existe 1 % de modification entre chaque instantané, vous obtenez 60 Go pour les instantanés.

*(5 Go de taux de modification) x (12 instantanés par heure) = 60 Go d'espace utilisé*

A l'inverse, si ces 500 Go de données réelles, avec 12 instantanés par heure, connaissent 10 % de modification toutes les heures, l'espace d'image instantanée qui est utilisé est 600 Go.

*(50 Go de taux de modification) x (12 instantanés par heure) = 600 Go d'espace utilisé*

Vous devez donc tenir compte du taux de modification lorsque vous déterminez la quantité d'espace d'image instantanée dont vous avez besoin. Il influe en effet considérablement sur la quantité d'espace d'instantané dont vous avez besoin. Un plus grand volume est davantage susceptible de changer plus souvent. Toutefois, un volume de 500 Go avec 5 Go de modification et un volume de 10 To avec 5 Go de modification utilisent la même quantité d'espace d'instantané.

De plus, pour la plupart des charges de travail, plus le volume est grand, plus l'espace à prévoir initialement est réduit. Cela est principalement dû aux efficiences des données sous-jacentes et à la nature du fonctionnement des instantanés dans l'environnement.
