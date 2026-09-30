# ADR-0001 : Ajouter un composant ETL

## Statut

Accepted

## Contexte et problème

- une charge importante de certains partenaires rend lent / indisponible le service auprès des clients
- certains modules de l'application ont plusieurs responsabilités (servir requêtes clients / ingérer les données)
  violation du principe de responsabilité unique

## Decision Drivers

- meilleure maintenabilité / déployabilité des modules (serveur / ingestion)
- meilleure disponibilité du service pour les clients

## Options considérées

### Option 1 :  séparer le code "ETL" dans un nouveau composant distinct en réutilisant le code existant

**Avantages** :
- nous avons les modules existants, donc pas besoin de réécrire le code
- nous avons les compétences pour le faire.
- économique en temps et en argent

**Inconvénients** :
- il faudra assurer l'évolution du code existant en cas d'augementation de sources différents

### Option 2 :  utiliser un "ETL" opensource et gratuit (pentaho, informatica)

**Avantages** :
- composant mature et robuste, gestion du temps réel, gestion des erreurs
- intergace graphique: langage agnostique

**Inconvénients** :
- courbe d'apprentissage pour l'équipe
- coût d'installation et maintenance (mise à jour, sécurité, etc.)

### Option 3:  utiliser un "ETL" payant (talend via qlik)

**Avantages** :
- solution complète, accès cloud, support technique

**Inconvénients** :
- çà cout un bras et une jambe


## Décision

pourquoi l'option 1 est retenue:
- nous avons les modules existants, donc pas besoin de réécrire le code
- nous avons les compétences pour le faire.
- pas lignes budgétaires ni temps à allouer

## Conséquences

### Positives

* [Conséquence positive 1]

### Négatives

* [Conséquence négative 1]

### Neutres

* [Conséquence neutre 1]

## Liens

[Liens vers les documents de référence, les discussions, les benchmarks, etc.]