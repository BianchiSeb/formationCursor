# Petit historique

## Étape 1 : Les Données Descriptives et la Logique Programmée (Les "Méta-données" et l'Intelligence "à la main")

* **Période** : Les débuts de l'informatique jusqu'à l'avènement plus large du Machine Learning (disons, jusqu'aux
  années 1990-2000 pour simplifier).
* **Type de données** :
    * Principalement des bases de données structurées. Ce que vous appelez "méta-données" est une bonne façon de le
      voir : des informations *sur* la réalité, soigneusement organisées.
        * *Exemples* : Fiches clients avec nom, adresse, historique d'achats ; catalogues de produits avec descriptions,
          prix, stock ; données comptables.
    * Ces données sont souvent des descriptions et des mesures du monde, collectées et organisées par des humains.
* **Comment on les utilisait** :
    * Avec des programmes informatiques classiques. Des développeurs écrivaient des règles explicites (logique "si...
      alors... sinon...") pour traiter ces données.
    * L'intelligence était "codée à la main" dans le programme. Le programme ne "comprenait" pas les données, il
      exécutait des instructions.
    * *Exemples d'applications* : Systèmes de gestion de stock, premiers systèmes de recommandation basés sur des règles
      simples (ex: "si achat de produit A, proposer produit B"), moteurs de recherche basés sur des mots-clés exacts.
* **Limites** : Difficile de gérer la complexité du monde réel, incapable de découvrir des relations inattendues, très
  rigide. Si la réalité change, il faut réécrire les règles.

## Étape 2 : L'Apprentissage Automatique (Machine Learning) - La Découverte de Patterns dans les Données (L'Intelligence par Analogie)

* **Période** : Montée en puissance à partir des années 1990-2000, accélération dans les années 2010.
* **Type de données** :
    * On utilise toujours des données structurées, mais aussi de plus en plus de données moins structurées ou
      semi-structurées : logs de navigation web, données de capteurs, etc.
    * Le volume de données disponibles commence à exploser (Big Data).
* **Comment on les utilisait (et on les utilise toujours !)** :
    * Avec des algorithmes de Machine Learning (dont les réseaux de neurones, mais pas uniquement au début).
    * L'IA apprend à détecter des schémas (patterns), des corrélations, des analogies directement à partir des données,
      sans qu'on ait besoin de lui dire explicitement quelles règles chercher.
    * Elle apprend par l'exemple et peut faire des prédictions ou des classifications.
    * *Exemples d'applications* : Filtres anti-spam (apprend ce qui ressemble à un spam), systèmes de recommandation
      plus sophistiqués (Netflix, Amazon : "les gens qui ont aimé X ont aussi aimé Y"), détection de fraude,
      reconnaissance d'images (chats vs chiens), diagnostic médical assisté.
* **Avancée** : Plus flexible, capable de découvrir des relations complexes que les humains n'auraient pas vues.
  L'intelligence "émerge" des données.

## Étape 3 : Les Grands Modèles (Transformers) et les Données Brutes - La Génération à partir de la "Réalité Numérique"

* **Période** : Depuis la fin des années 2010 (notamment avec l'article "Attention Is All You Need" en 2017 qui a
  introduit les Transformers) et aujourd'hui.
* **Type de données** :
    * On passe à une échelle encore supérieure. On utilise des quantités massives de données brutes et non structurées,
      qui sont des représentations directes de la "réalité numérique".
        * *Texte* : L'intégralité (ou presque) d'Internet, des bibliothèques de livres numérisés. Ce ne sont plus juste
          des "méta-données" sur des livres, mais le contenu des livres eux-mêmes.
        * *Images* : Des milliards d'images du web, avec leurs légendes.
        * *Audio, Vidéo, Code...*
* **Comment on les utilise** :
    * Avec des architectures de réseaux de neurones très profondes et puissantes, notamment les Transformers.
    * Ces modèles sont capables d'ingérer et de "comprendre" (au sens statistique de détection de patterns très
      complexes) ces données brutes à une échelle sans précédent.
    * Ils ne se contentent plus de classer ou de prédire, ils peuvent générer du contenu nouveau et original qui
      ressemble aux données sur lesquelles ils ont été entraînés.
    * *Exemples d'applications* : ChatGPT (génération de texte), DALL-E/Midjourney/Stable Diffusion (génération
      d'images), GitHub Copilot (génération de code), traduction automatique de très haute qualité.
* **Avancée majeure** : Capacité à traiter et à modéliser des séquences longues et des dépendances complexes dans les
  données (grâce au mécanisme d'attention des Transformers). Passage de l'analyse à la création. On ne travaille plus
  seulement sur des descriptions de la réalité, mais sur des "morceaux" de cette réalité numérique pour en créer de
  nouveaux.
