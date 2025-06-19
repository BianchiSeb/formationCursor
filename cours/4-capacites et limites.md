# Capacités et Limites des LLM

## Donner des Super-Pouvoirs à l'IA : Le Rôle du Contexte et des Données Externes

### 1. Le Contexte "Interne" Limité des LLM (La Fenêtre d'Attention)

* **Rappel** : On a vu que les LLM comme ChatGPT sont entraînés sur d'énormes quantités de données. Cette connaissance
  est "compilée" dans leurs milliards de paramètres.
* **La Fenêtre de Contexte** : Cependant, quand vous interagissez avec un LLM, il ne "repense" pas à l'intégralité de
  ses données d'entraînement à chaque question. Il a une sorte de **mémoire à court terme**, appelée **fenêtre de
  contexte** (ou "context window").
    * Cette fenêtre a une taille limitée (mesurée en nombre de tokens) qui définit la quantité d'information (votre
      question, l'historique de la conversation, et potentiellement des informations supplémentaires) que le LLM peut "
      voir" et prendre en compte *activement* au moment de générer une réponse.
    * Tout ce qui est en dehors de cette fenêtre est essentiellement "oublié" pour cette interaction spécifique (même si
      la connaissance générale reste dans ses poids).
* **Limites de ce contexte interne** :
    * *Connaissances figées* : La connaissance du LLM est figée à la date de la fin de son entraînement. Il ne connaît
      pas les événements récents ou les informations très spécifiques non présentes dans ses données initiales.
    * *Risque d'hallucinations* : S'il n'a pas l'information précise, il peut "inventer" des réponses qui semblent
      plausibles mais sont incorrectes.

### 2. L'Idée : Élargir le Contexte avec des Données Externes "Indexées" (Le Principe du RAG)

* **Le Défi** : Comment donner au LLM accès à des informations à jour, spécifiques à un domaine, ou propriétaires (par
  exemple, les documents internes d'une entreprise) sans avoir à le ré-entraîner complètement (ce qui est coûteux et
  long) ?
* **La Solution - Le RAG** : C'est là qu'intervient l'idée d'utiliser des **données externes "indexées"** pour enrichir
  le contexte fourni au LLM au moment de la question.
    * Imaginez que vous ayez une grande bibliothèque de documents très spécifiques (votre "base de connaissances
      externe").
    * **Étape 1 : Indexation (Préparation de la Bibliothèque)**
        1. On découpe ces documents en morceaux pertinents (chunks).
        2. Pour chaque morceau, on crée un **vecteur d'embedding** (sa "carte d'identité sémantique", comme on l'a vu).
        3. Ces vecteurs sont stockés dans une **base de données vectorielle**, qui est optimisée pour trouver rapidement
           des vecteurs similaires. C'est notre "index sémantique".
    * **Étape 2 : Récupération (Trouver le Bon Livre au Bon Moment)**
        1. Quand vous posez une question au système RAG, votre question est aussi transformée en un vecteur d'embedding.
        2. Le système cherche dans la base de données vectorielle les morceaux de documents dont les embeddings sont les
           plus similaires à celui de votre question. C'est l'étape de **récupération (retrieval)**.
    * **Étape 3 : Augmentation du Contexte (Donner les Notes à l'Expert)**
        1. Les morceaux de documents les plus pertinents ainsi récupérés sont ajoutés au **prompt** (l'instruction) que
           l'on envoie au LLM, en plus de votre question initiale.
        2. *Exemple de prompt augmenté* : "Contexte : \[Morceau de document 1 pertinent], \[Morceau de document 2
           pertinent]. Question : \[Votre question initiale]. Réponds à la question en te basant sur le contexte
           fourni."

### 3. Pourquoi ce Contexte Externe est-il si Puissant ?

* **Accès à des Connaissances à Jour et Spécifiques** : Le LLM peut répondre à des questions sur des sujets récents ou
  des données propriétaires qui n'étaient pas dans son entraînement initial, simplement parce qu'on lui fournit l'
  information pertinente au bon moment.
* **Réduction des Hallucinations** : En "ancrant" la réponse du LLM dans des faits concrets issus des documents
  récupérés, on diminue fortement le risque qu'il invente des informations.
* **Transparence et Citations** : Souvent, les systèmes RAG peuvent indiquer les sources (les morceaux de documents)
  qu'ils ont utilisées pour générer la réponse, ce qui augmente la confiance et permet la vérification.
* **Personnalisation** : On peut "brancher" un LLM généraliste sur différentes bases de connaissances spécifiques pour
  le faire répondre comme un expert dans divers domaines, sans ré-entraînement lourd.
* **Contrôle** : On a un meilleur contrôle sur le type d'informations que le LLM va utiliser.

### 4. Le LLM Utilise Toujours sa "Fenêtre de Contexte"

* Il est important de comprendre que même avec le RAG, le LLM opère toujours dans les limites de sa **fenêtre de
  contexte**.
* Les documents récupérés sont injectés *dans* cette fenêtre. Si l'ensemble de la question originale + les documents
  récupérés est trop grand pour la fenêtre de contexte du LLM, il faudra des stratégies pour le gérer (résumer,
  sélectionner les parties les plus importantes, etc.).
* Le LLM utilise alors sa capacité à comprendre le langage et à raisonner (apprise lors de son entraînement initial)
  pour synthétiser une réponse cohérente à partir de votre question et du contexte supplémentaire fourni.

## Les LLM : Des Cerveaux Puissants, Mais avec des Limites (et Comment On Les Dépasse)

### Partie 1 : Les Limitations Intrinsèques d'un LLM "Nu"

Imaginez un LLM comme un cerveau incroyablement savant, mais qui a été enfermé dans une bibliothèque à une date précise
et n'a plus eu de contact avec l'extérieur depuis. Ce cerveau a des limitations fondamentales :

1. **Connaissances Statiques (Le Problème de la "Date Limite")**
    * *Limitation* : Un LLM ne connaît que les informations présentes dans ses données d'entraînement, et ces
      connaissances sont figées à la date de la fin de cet entraînement (son "knowledge cut-off date"). Il ne connaît
      pas les événements récents, les nouvelles découvertes, ou les informations apparues après cette date.
    * *Analogie* : C'est comme un livre d'histoire qui s'arrête en 2021 ; il ne vous dira rien sur 2023.
    * *Conséquence* : Réponses obsolètes ou incorrectes sur des sujets d'actualité.
2. **Pas d'Accès à l'Information en Temps Réel (Pas d'Internet Intégré)**
    * *Limitation* : Un LLM "nu" ne peut pas naviguer sur internet de lui-même. Il n'a pas de "navigateur web" intégré
      ni la capacité d'initier des requêtes sur le web.
    * *Analogie* : Notre cerveau dans la bibliothèque ne peut pas sortir pour aller chercher le journal du jour.
    * *Conséquence* : Incapacité à fournir des informations ultra-récentes, des cours de bourse en direct, la météo
      actuelle, etc.
3. **Pas de Perception du Temps Présent (Pas de "Date du Jour")**
    * *Limitation* : Un LLM n'a pas de notion intrinsèque de la date ou de l'heure actuelle. Si vous lui demandez "
      Quelle heure est-il ?", il ne peut pas le savoir par lui-même.
    * *Analogie* : Le cerveau dans la bibliothèque n'a ni montre ni calendrier.
    * *Conséquence* : Incapacité à répondre à des questions qui dépendent du temps présent sans aide extérieure.
4. **Incapacité à Exécuter des Actions dans le Monde Extérieur (Pas de "Mains" ou "Jambes")**
    * *Limitation* : Un LLM est un modèle de langage ; il génère du texte. Il ne peut pas, par lui-même, exécuter du
      code sur votre ordinateur, envoyer un email, interagir avec d'autres logiciels, ou manipuler des fichiers.
    * *Analogie* : Notre cerveau peut penser à une recette, mais il a besoin de mains pour la cuisiner.
    * *Conséquence* : Ne peut pas effectuer des tâches qui nécessitent une interaction avec des systèmes externes ou des
      actions concrètes.
5. **Pas de "Compréhension" Profonde ou de Conscience**
    * *Limitation (plus philosophique mais importante)* : Un LLM manipule des patterns statistiques dans le langage. Il
      ne "comprend" pas au sens humain, n'a pas de conscience, de croyances, ou d'intentions propres.
    * *Analogie* : Un perroquet très doué qui peut répéter des phrases complexes et même en inventer de nouvelles qui
      sonnent bien, mais sans en saisir le sens profond.
    * *Conséquence* : Peut générer des réponses qui semblent logiques mais sont factuellement incorrectes (
      hallucinations), ou qui manquent de véritable raisonnement causal ou de bon sens dans des situations nouvelles.
6. **Sensibilité au Prompt (La Qualité de la Question Influence la Réponse)**
    * *Limitation* : La qualité et la formulation de l'instruction (le prompt) ont un impact énorme sur la qualité de la
      réponse. Un prompt vague ou ambigu mènera souvent à une réponse insatisfaisante.
    * *Analogie* : Si vous posez une question floue à un expert, vous obtiendrez probablement une réponse floue.
    * *Conséquence* : Nécessite une certaine habileté de l'utilisateur pour obtenir les meilleurs résultats.

### Partie 2 : Comment les Applications (comme ChatGPT, Gemini) "Augmentent" les LLM

Alors, comment se fait-il que des outils comme ChatGPT ou Gemini semblent pouvoir faire certaines de ces choses ? C'est
parce que les éditeurs de ces applications construisent des systèmes *autour* du LLM de base, en lui greffant des "
outils" ou des "capacités externes".

* **Le LLM comme Cerveau Central, les Outils comme des Extensions** :
    * Le LLM reste le "cerveau" qui traite le langage et raisonne (statistiquement).
    * Les applications lui ajoutent des "super-pouvoirs" en orchestrant des interactions avec d'autres outils/services.
* **Exemples Concrets** :
    1. **Accès à Internet (Simulé)** :
        * *Ce qui se passe en coulisses* :
            1. L'application détecte que la question nécessite une information du web.
            2. Un **outil externe** (un "agent" ou un module de recherche) est activé. Cet outil *peut* aller sur
               internet (ex: via une API de moteur de recherche ou en faisant un "GET" sur une page).
            3. Cet outil récupère le contenu brut (ex: code HTML).
            4. Un autre **outil** (ou le même) peut *parser* ce contenu pour en extraire l'information pertinente (
               enlever les balises HTML, le superflu).
            5. Le **texte nettoyé et pertinent est ensuite fourni au LLM comme contexte** dans son prompt.
            6. Le LLM utilise ce contexte pour formuler une réponse.
        * *L'illusion pour l'utilisateur* : L'utilisateur a l'impression que le LLM a navigué sur le web, mais c'est une
          orchestration d'outils externes dont le LLM utilise le résultat.
    2. **Exécution de Code (Simulée ou Réelle mais Sécurisée)** :
        * *Ce qui se passe en coulisses (ex: ChatGPT Code Interpreter / Advanced Data Analysis)* :
            1. L'utilisateur demande d'exécuter du code ou de faire une tâche qui nécessite du code (ex: "trace un
               graphique de ces données").
            2. Le LLM génère le code Python nécessaire.
            3. Ce **code est ensuite exécuté dans un environnement sécurisé et isolé** (un "sandbox") géré par
               l'application, *en dehors du LLM lui-même*.
            4. Les résultats de l'exécution (sorties, graphiques, erreurs) sont renvoyés à l'application.
            5. Ces résultats sont **fournis au LLM comme observation/contexte**.
            6. Le LLM interprète ces résultats et formule une réponse ou une explication à l'utilisateur.
        * *L'illusion pour l'utilisateur* : Le LLM semble exécuter du code, mais il ne fait que le générer et
          interpréter les résultats d'une exécution externe.
    3. **Connaissance de la Date/Heure Actuelle** :
        * *Ce qui se passe en coulisses* : L'application récupère simplement la date/heure actuelle du système sur
          lequel elle tourne et l'injecte dans le prompt du LLM si nécessaire. "Aujourd'hui nous sommes le \[date
          actuelle]. Peux-tu..."
    4. **Utilisation de Plugins / Outils Spécifiques** :
        * Les systèmes de plugins permettent au LLM d'accéder à des capacités très variées (réserver un vol, commander à
          manger, interagir avec une base de données spécifique) via des API. Le LLM apprend à "appeler" ces outils
          quand c'est pertinent, en leur fournissant les bons paramètres, et interprète ensuite leurs réponses.

**Conclusion pour cette partie :**

* Il est essentiel de distinguer le **LLM de base** (le "moteur" de langage avec ses limitations intrinsèques) de l'*
  *application complète** que vous utilisez.
* Les applications modernes "augmentent" les LLM en les connectant à des outils externes, leur donnant ainsi des
  capacités qui vont bien au-delà de ce qu'un LLM seul pourrait faire.
* Cette orchestration est ce qui rend ces outils si puissants et polyvalents, mais il est bon de comprendre que le "
  miracle" repose souvent sur une ingénierie logicielle intelligente autour du LLM, et pas seulement sur le LLM
  lui-même.
