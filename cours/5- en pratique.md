# En Pratique

## Règles d'Or pour un Prompting Efficace

1. **Soyez Clair et Spécifique (Pas de Flou Artistique)**
    * *Pourquoi ?* Les LLM ne lisent pas dans les pensées. Un prompt vague mènera à une réponse vague ou à côté de la
      plaque.
    * *Comment ?*
        * Définissez clairement ce que vous attendez.
        * Précisez le format de sortie souhaité (liste, paragraphe, code, tableau, etc.).
        * Indiquez la longueur approximative (court, détaillé, un paragraphe, 5 points).
        * Évitez les ambiguïtés.
    * *Exemple Mauvais* : "Parle-moi de l'IA."
    * *Exemple Bon* : "Explique en 3 points clés, pour un public débutant, comment l'apprentissage automatique
      fonctionne dans le contexte de l'IA."

2. **Donnez du Contexte (Aidez le LLM à se Situer)**
    * *Pourquoi ?* Le contexte aide le LLM à mieux comprendre votre besoin et à s'appuyer sur des informations
      pertinentes (surtout s'il n'a pas accès à des outils externes pour le récupérer lui-même).
    * *Comment ?*
        * Fournissez les informations de base nécessaires.
        * Mentionnez l'audience cible de la réponse (débutant, expert, enfant).
        * Si vous faites référence à quelque chose de précédent dans la conversation, soyez explicite (même si le LLM a
          une fenêtre de contexte, il peut se perdre).
    * *Exemple Mauvais* : "Écris un email pour annuler."
    * *Exemple Bon* : "Je dois annuler mon rendez-vous chez le dentiste Dr. Martin prévu demain à 14h car j'ai un
      imprévu. Rédige un email court et poli pour l'en informer et proposer de reprendre rendez-vous."

3. **Définissez un Rôle (Mettez le LLM dans la Peau d'un Expert)**
    * *Pourquoi ?* Cela aide le LLM à adopter un ton, un style et un niveau de connaissance appropriés.
    * *Comment ?*
        * Commencez par "Agis comme un..." ou "Tu es un..."
    * *Exemple* : "Agis comme un expert en marketing digital. Propose-moi 5 idées de contenu pour promouvoir une
      nouvelle application de productivité sur Instagram."
    * *Autre exemple* : "Tu es un professeur de sciences pour des enfants de 10 ans. Explique le cycle de l'eau avec des
      mots simples et une analogie."

4. **Utilisez des Exemples (Apprentissage "One-Shot" ou "Few-Shot")**
    * *Pourquoi ?* Montrer au LLM le type de réponse que vous attendez est souvent plus efficace que de le décrire.
    * *Comment ?*
        * Fournissez un ou plusieurs exemples de la tâche que vous voulez qu'il accomplisse, en montrant l'entrée et la
          sortie désirée.
    * *Exemple (Sentiment Analysis "Few-Shot")* :
      ```
      Classe le sentiment de ces phrases comme Positif, Négatif ou Neutre :
      Phrase : 'J'adore ce nouveau film !' Sentiment : Positif
      Phrase : 'Le service était vraiment décevant.' Sentiment : Négatif
      Phrase : 'Le colis est arrivé aujourd'hui.' Sentiment : Neutre
      Phrase : 'Cette nouvelle fonctionnalité est incroyablement utile.' Sentiment : ?
      ```

5. **Décomposez les Tâches Complexes (Diviser pour Mieux Régner)**
    * *Pourquoi ?* Les LLM peuvent avoir du mal avec des instructions trop longues ou multi-étapes.
    * *Comment ?*
        * Séparez une tâche complexe en plusieurs prompts plus petits et plus gérables.
        * Utilisez une approche "chaîne de pensée" (Chain of Thought - CoT) en demandant au LLM d'expliquer son
          raisonnement étape par étape, surtout pour les problèmes logiques.
    * *Exemple (mauvais pour une seule étape)* : "Analyse ce document de 10 pages, résume-le, identifie les 3 arguments
      clés, et rédige une réponse critique."
    * *Exemple (meilleur en plusieurs étapes)* :
        1. Prompt 1 : "Voici un document \[texte du document]. Résume-le en 200 mots."
        2. Prompt 2 : "À partir de ce résumé, quels sont les 3 arguments clés présentés ?"
        3. Prompt 3 : "En te basant sur ces arguments, rédige une critique constructive."
    * *Exemple (Chain of Thought)* : "Résous ce problème mathématique et explique chaque étape de ton raisonnement :
      \[problème]."

6. **Itérez et Affinez (Ne Vous Attendez Pas à la Perfection du Premier Coup)**
    * *Pourquoi ?* Le prompting est souvent un processus itératif. Votre premier prompt ne sera pas toujours parfait.
    * *Comment ?*
        * Si la réponse n'est pas satisfaisante, modifiez votre prompt, ajoutez des précisions, clarifiez vos attentes.
        * Essayez différentes formulations.
        * Demandez au LLM de reformuler sa réponse, de la simplifier, ou de l'aborder sous un autre angle.
    * *Exemple* : Si le LLM donne une réponse trop technique, vous pouvez dire : "C'est bien, mais peux-tu l'expliquer
      comme si tu parlais à quelqu'un qui n'a jamais entendu parler de ce sujet ?"

7. **Spécifiez ce qu'il Faut Éviter (Instructions Négatives)**
    * *Pourquoi ?* Parfois, il est aussi important de dire ce que vous *ne voulez pas* que ce que vous voulez.
    * *Comment ?*
        * "Ne pas utiliser de jargon technique."
        * "Évite les phrases trop longues."
        * "Assure-toi que la réponse ne mentionne pas \[sujet sensible]."
    * *Exemple* : "Rédige une description de produit pour un nouveau café. Mets en avant son goût unique et son origine
      éthique. Évite les superlatifs excessifs comme 'le meilleur du monde'."

8. **Vérifiez et Soyez Critique (N'oubliez pas les Limitations !)**
    * *Pourquoi ?* Rappelez-vous que les LLM peuvent halluciner, avoir des connaissances obsolètes, ou reproduire des
      biais.
    * *Comment ?*
        * Vérifiez toujours les informations factuelles importantes, surtout si vous n'utilisez pas un système RAG avec
          des sources citées.
        * Soyez conscient des biais potentiels dans les réponses.
        * Ne prenez pas tout pour argent comptant. Le LLM est un outil, pas une oracle infaillible.

## Paramètres Fondamentaux pour Contrôler la Génération

### 1. Modèle (Model)

* **Explication** : C'est le choix du "cerveau" spécifique que vous allez utiliser. Différents modèles ont des
  capacités, des tailles de fenêtre de contexte, des coûts et des dates de fin de connaissance différents. (ex: GPT-4,
  GPT-3.5-turbo, Claude 3 Opus, Gemini Pro, etc.).

### 2. Température (Temperature)

* **Explication** : Contrôle le degré d'**aléa** ou de "créativité" dans les réponses.
    * *Valeur basse (proche de 0)* : Réponses plus déterministes, focalisées, prévisibles. Le modèle choisira les mots
      les plus probables. Utile pour des tâches factuelles, du résumé, de la génération de code où la précision est clé.
    * *Valeur haute (ex: 0.7 à 1.5 et plus)* : Réponses plus créatives, surprenantes, diversifiées, voire un peu "
      folles" si trop élevée. Le modèle peut choisir des mots moins probables. Utile pour le brainstorming, l'écriture
      créative, la génération d'idées.
* *Analogie* : Un thermostat pour la créativité.

### 3. Top P (Nucleus Sampling)

* **Explication** : Une autre méthode pour contrôler l'aléa, souvent utilisée en alternative ou en complément de la
  température. Le modèle considère seulement le plus petit ensemble de mots dont la probabilité cumulée dépasse la
  valeur P.
    * *Valeur de 1* : Prend en compte tous les mots (pas de filtrage par probabilité).
    * *Valeur plus basse (ex: 0.95)* : Le modèle ne considère que les mots les plus probables formant 95% de la
      distribution de probabilité pour le token suivant. Cela évite que des mots très improbables soient choisis, même à
      haute température.
* *Utilisation* : Souvent, on règle soit la température, soit le Top P, et on laisse l'autre à sa valeur par défaut (ex:
  Top P à 1 si on joue avec la température).

### 4. Longueur Maximale de Sortie (Output length / Max Tokens)

* **Explication** : Définit le nombre maximum de tokens que la réponse générée par le LLM peut contenir.
* *Pourquoi ?* Pour éviter des réponses infiniment longues (et coûteuses), et pour s'assurer que la réponse reste dans
  des limites gérables.
* *Note* : Le chiffre 65536 mentionné précédemment est très élevé, il pourrait représenter le maximum théorique pour
  certains modèles ou une limite très large. En pratique, on utilise souvent des valeurs bien plus basses (quelques
  centaines ou milliers).

### 5. Séquences d'Arrêt (Stop Sequences / Add stop sequence)

* **Explication** : Vous pouvez spécifier une ou plusieurs séquences de texte (des mots ou des phrases). Si le LLM
  génère l'une de ces séquences, il s'arrêtera immédiatement, même s'il n'a pas atteint la `Output length` maximale.
* *Pourquoi ?* Utile pour contrôler le format de sortie (ex: arrêter après "Utilisateur :"), pour éviter des
  répétitions, ou quand le modèle a terminé une tâche structurée.

## Paramètres Liés aux "Outils" et Capacités Augmentées

*(Cette section fait référence aux fonctionnalités souvent disponibles dans des interfaces comme Google AI Studio ou via
les API des modèles.)*

### 1. Sortie Structurée (Structured output)

* **Explication** : Permet de forcer le LLM à générer sa sortie dans un format spécifique, comme JSON. C'est extrêmement
  utile quand la sortie du LLM doit être utilisée par un autre programme. Le LLM essaiera de remplir les champs d'un
  schéma JSON que vous lui fournissez.

### 2. Exécution de Code (Code execution)

* **Explication** : Permet au LLM (ou plutôt à l'application qui l'entoure) d'exécuter du code (souvent Python) dans un
  environnement sécurisé (sandbox). Le LLM génère le code, l'environnement l'exécute, et le résultat est renvoyé au LLM
  pour qu'il puisse l'utiliser ou le présenter.

### 3. Appel de Fonctions (Function calling)

* **Explication** : Une des fonctionnalités les plus puissantes. Vous définissez des "outils" ou des "fonctions"
  externes (ex: une fonction pour obtenir la météo, une API pour chercher des produits, une base de données). Le LLM
  peut alors décider, en fonction de la question de l'utilisateur, d'appeler une de ces fonctions. Il génère une requête
  structurée (souvent JSON) avec les paramètres nécessaires pour la fonction. L'application exécute la fonction et
  renvoie le résultat au LLM, qui l'utilise pour formuler sa réponse finale.

### 4. Ancrage avec Google Search (Grounding with Google Search)

* **Explication** : C'est une forme de RAG (Retrieval Augmented Generation) intégrée. Si activé, le système peut
  utiliser Google Search pour trouver des informations pertinentes sur le web et les utiliser pour "ancrer" la réponse
  du LLM, la rendant potentiellement plus factuelle et à jour.

### 5. Contexte d'URL (URL context)

* **Explication** : Permet probablement de fournir une ou plusieurs URL directement dans le prompt, et le système se
  chargera de récupérer le contenu de ces URL pour l'utiliser comme contexte pour le LLM. C'est une autre forme de RAG
  simplifiée.

## Autres Paramètres Importants

### 1. Paramètres de Sécurité (Safety settings)

* **Explication** : La plupart des plateformes LLM ont des filtres de sécurité pour bloquer ou modérer le contenu
  haineux, sexuellement explicite, dangereux, etc. Ces paramètres permettent souvent d'ajuster le niveau de sensibilité
  de ces filtres (par exemple, bloquer ou seulement avertir, et pour quelles catégories).

### 2. Nombre de Tokens (Token count)

* **Explication** : Ce n'est pas un paramètre que vous réglez directement dans l'API pour la génération, mais une
  information cruciale. Elle indique la taille actuelle de votre prompt (et potentiellement de l'historique de la
  conversation) en tokens, par rapport à la **fenêtre de contexte maximale** du modèle. Vous devez vous assurer que
  votre entrée + la longueur de sortie maximale souhaitée ne dépassent pas cette fenêtre.
