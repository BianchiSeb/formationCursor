# La Donnée, la Brique de Base de la Création des LLM

## Le Processus de Création à Partir de la Data

### 1. La Collecte Massive (La Matière Première)

* On commence par rassembler des quantités astronomiques de données.
    * **Pour le texte (comme ChatGPT)** : Des milliards de pages web (comme une grande partie d'Internet via des
      archives comme Common Crawl), des livres numérisés, des articles de Wikipédia, des conversations, du code
      informatique, etc.
    * **Pour les images (comme Midjourney)** : Des millions, voire des milliards d'images récupérées sur internet,
      souvent accompagnées de leurs descriptions textuelles (les "légendes" ou "alt-text"). Des bases de données comme
      LAION (Large-scale Artificial Intelligence Open Network) sont des exemples de tels ensembles de paires
      image-texte.
* *Analogie* : C'est comme si on vidait des camions entiers de livres, journaux, et photos dans un immense hangar.

### 2. Le Pré-traitement et Nettoyage (Rendre les Livres Lisibles)

* Ces données brutes sont souvent "sales" : doublons, contenu de mauvaise qualité, formatages bizarres, parfois du
  contenu indésirable ou biaisé.
* **Nettoyage** : On essaie de filtrer le contenu haineux, les spams, de supprimer les doublons massifs, de corriger des
  erreurs de formatage. C'est une étape cruciale mais imparfaite (d'où certains biais qui peuvent persister).
* **Normalisation** : Mettre le texte dans un format plus uniforme (ex: tout en minuscules, gérer la ponctuation).
* *Analogie* : C'est comme si on triait les livres du hangar : on enlève ceux qui sont illisibles, déchirés, on s'assure
  que les pages sont dans le bon ordre.

### 3. La Transformation en "Langage Machine"

* L'IA ne lit pas comme nous. Il faut transformer ces données en chiffres qu'elle peut traiter.
* **Pour le texte - Tokenisation** : On en a parlé. Le texte est découpé en tokens (mots, sous-mots, caractères). Chaque
  token unique se voit attribuer un identifiant numérique. Donc, une phrase devient une séquence de nombres.
    * *Exemple* : "Le chat" -> `[ID_Le, ID_chat]` -> `[12, 567]` (chiffres fictifs)
* **Pour les images - Pixels et plus** : Une image est déjà une grille de pixels, chaque pixel ayant des valeurs
  numériques (Rouge, Vert, Bleu). Les modèles plus avancés ne travaillent pas directement avec les pixels bruts mais
  apprennent à en extraire des "caractéristiques" (bords, textures, formes simples) via des couches spécialisées (
  convolutionnelles). Pour les modèles génératifs d'images à partir de texte, on utilise souvent des techniques qui
  transforment l'image en une représentation numérique plus compacte et sémantique (un "embedding" d'image).

### 4. L'Importance des Métadonnées (Les "Étiquettes" sur les Livres ou les Rayons)

* Oui, les métadonnées sont souvent cruciales, surtout pour certains types d'IA !
* **Pour les IA génératives d'images à partir de texte (DALL-E, Midjourney, Stable Diffusion)** : C'est la clé ! Les
  images dans leurs bases de données d'entraînement sont associées à des descriptions textuelles.
    * *Exemple de métadonnée* : Image X -> "Un chat roux dormant sur un canapé bleu."
    * L'IA apprend à faire le lien entre les caractéristiques visuelles de l'image X et les mots "chat", "roux", "
      dormant", "canapé", "bleu".
* **Pour les IA textuelles (Grands Modèles de Langage - LLM)** : C'est un peu différent. Souvent, la "métadonnée" est
  plus implicite. Le modèle apprend à partir du contexte brut du texte.
    * Cependant, on peut utiliser des métadonnées pour des tâches spécifiques d'affinage (fine-tuning). Par exemple, si
      on veut qu'un LLM soit bon pour répondre à des questions sur l'histoire, on pourrait l'entraîner davantage sur des
      textes spécifiquement étiquetés "histoire".
    * Pour le pré-entraînement massif, la "métadonnée" peut être simplement la source du document (ex: "Wikipedia", "
      Livre de fiction"). Le modèle apprend des styles et des contenus différents de ces sources.
* *Analogie* : Dans notre bibliothèque, certains livres ont des étiquettes claires ("Science-fiction", "Recette de
  cuisine"). Pour d'autres, l'étudiant doit deviner le sujet en lisant le contenu.

### 5. "Indexation" (Comment l'IA Retrouve l'Information pour Apprendre)

* Le terme "indexation" comme dans une base de données traditionnelle (où l'on crée un index pour chercher vite) n'est
  pas exactement ce qui se passe pendant *l'entraînement principal* d'un grand modèle.
* **Pendant l'entraînement** : L'IA ne "cherche" pas activement dans les données comme nous le ferions avec Google.
  Elle "lit" séquentiellement (ou par lots aléatoires) d'énormes portions de ces données préparées.
* **L'"indexation" est implicite** : En traitant des milliards de tokens ou d'images, le modèle ajuste ses milliards de
  paramètres internes (les "poids" de son réseau de neurones). Ces poids deviennent une représentation compressée et
  généralisée de toute l'information vue. C'est comme si toute la connaissance de la bibliothèque était distillée et
  encodée dans la structure même du cerveau de l'étudiant. Il ne se souvient pas de chaque mot de chaque livre, mais il
  a intégré les règles, les styles, les concepts.
* *Analogie* : L'étudiant ne garde pas un index de chaque page de chaque livre. Mais après avoir lu des milliers de
  livres, son cerveau a organisé l'information, créé des liens entre les concepts, et il peut générer de nouvelles
  phrases basées sur cette compréhension globale.
* **Cas particulier : Retrieval Augmented Generation (RAG)** : Ici, le concept d'indexation est plus direct. Pour
  améliorer les réponses d'un LLM et éviter les hallucinations, on peut lui donner accès à une base de données externe (
  souvent une base de données vectorielles). Cette base de données *est* indexée. Quand vous posez une question, le
  système cherche d'abord des documents pertinents dans cette base indexée, puis fournit ces documents au LLM comme
  contexte pour qu'il génère une réponse plus factuelle. C'est comme si l'étudiant avait le droit de consulter
  rapidement des fiches de notes spécifiques avant de répondre.

## Le Rapport entre la Qualité des Données et les Résultats d’un LLM

### 1. Le Principe Fondamental : L'IA Apprend Ce Qu'On Lui Montre

* Les LLM, et plus généralement les modèles de Machine Learning, sont des **imitateurs statistiques sophistiqués**. Ils
  apprennent à reproduire les patterns, les styles, les structures et, malheureusement aussi, les erreurs et les biais
  présents dans les données d'entraînement.
* Si un LLM est entraîné sur une immense quantité de code :
    * Il apprendra la syntaxe des langages de programmation.
    * Il apprendra les idiomes courants et les bonnes pratiques (s'ils sont suffisamment représentés).
    * Il apprendra aussi les mauvaises pratiques, les bugs fréquents, le code non optimisé, les failles de sécurité, si
      ceux-ci sont massivement présents dans les données d'entraînement.

### 2. Le Cas du Code sur GitHub (et d'Internet en Général)

* **Vaste mais Hétérogène** : GitHub (et d'autres plateformes comme Stack Overflow, des forums, etc., qui constituent
  la "connaissance" web sur le code) est une source de données incroyablement vaste. C'est une force, car cela expose le
  LLM à une immense variété de problèmes et de solutions.
* **Qualité Variable** : Cependant, la qualité de ce code est extrêmement hétérogène. On y trouve :
    * Du code excellent, écrit par des experts, bien documenté, testé.
    * Du code correct, fonctionnel mais pas optimal.
    * Du code d'apprentissage, écrit par des débutants, souvent avec des erreurs ou des mauvaises pratiques.
    * Du code obsolète, utilisant des bibliothèques dépassées ou des approches non recommandées.
    * Du code contenant des bugs subtils ou des failles de sécurité.
* **La "Blague" des Devs** : Elle a un fond de vérité. Si la majorité statistique du code accessible pour l'entraînement
  n'est pas de qualité exemplaire, le LLM aura tendance à refléter cette qualité moyenne, voire médiocre par moments. Il
  est difficile pour le modèle de distinguer intrinsèquement le "bon" du "mauvais" code sans signaux clairs.

### 3. Comment la Qualité des Données Affecte le LLM Générateur de Code

* **Génération de Code Bogué ou Inefficace** : Le LLM peut reproduire des patterns de code qui mènent à des bugs ou qui
  sont sous-optimaux parce qu'il les a vus fréquemment.
* **Introduction de Failles de Sécurité** : S'il a appris sur du code contenant des vulnérabilités courantes (ex:
  injections SQL, XSS mal gérées), il pourrait les reproduire.
* **Difficulté à Suivre les Meilleures Pratiques** : Si les meilleures pratiques sont minoritaires dans les données, le
  LLM aura plus de mal à les adopter systématiquement.
* **"Hallucinations" de Code** : Il peut générer du code qui *ressemble* à du code valide mais qui ne compile pas, ou
  qui utilise des fonctions ou des bibliothèques inexistantes, en se basant sur des patterns partiels ou mal compris.
* **Biais de Style** : Il peut adopter des styles de codage particuliers (bons ou mauvais) qui sont prévalents dans ses
  données.

### 4. Les Efforts pour Améliorer la Qualité (Ce N'est Pas Si Simple)

* **Filtrage et Curation des Données** : Les concepteurs de LLM tentent de filtrer les données d'entraînement. Pour le
  code, cela pourrait signifier :
    * Privilégier les dépôts avec beaucoup d'étoiles, bien maintenus.
    * Utiliser des outils d'analyse statique pour écarter le code de très mauvaise qualité.
    * Pondérer différemment les sources de données (ex: donner plus de poids à la documentation officielle des
      langages).
    * *Limites* : Le filtrage à grande échelle est complexe et coûteux. Définir "qualité" est subjectif. Il y a un
      risque de supprimer des exemples utiles ou de réduire la diversité.
* **Apprentissage par Renforcement à partir de Feedback Humain (RLHF) et Autres Techniques d'Affinage** :
    * Après le pré-entraînement, les modèles sont souvent affinés. Pour le code, on peut demander à des humains
      d'évaluer la qualité du code généré, de corriger les erreurs, ou de fournir de meilleurs exemples. Le modèle
      apprend de ce feedback.
    * *Exemple* : Si le LLM génère du code bogué, un humain le signale, et le modèle est ajusté pour moins reproduire ce
      type d'erreur.
    * *Limites* : Le RLHF est coûteux en ressources humaines et ne peut pas couvrir tous les cas de figure.
* **Données Synthétiques de Haute Qualité** : On pourrait imaginer générer du code "parfait" pour entraîner le modèle,
  mais c'est un défi en soi.
* **Instruction Tuning (Affinage par Instructions)** : Entraîner le modèle sur des paires (instruction, code de haute
  qualité) pour qu'il apprenne à suivre des directives et à produire du code qui répond à des critères de qualité
  spécifiques.

### 5. Nuances et Progrès

* **Pas Tous Nuls** : Malgré les défis, les LLM générateurs de code (comme GitHub Copilot, ChatGPT Code Interpreter,
  etc.) sont devenus étonnamment utiles pour de nombreuses tâches. Ils peuvent accélérer le développement, aider à
  déboguer, suggérer des solutions, traduire entre langages.
* **L'Effet de l'Échelle** : Des modèles plus grands, entraînés sur encore plus de données, semblent parfois capables de
  mieux "distiller" les bons patterns, même à partir de données bruitées, mais ce n'est pas une solution miracle.
* **L'Humain dans la Boucle** : Actuellement, le code généré par l'IA doit toujours être révisé, testé et validé par un
  développeur humain compétent. L'IA est un assistant, pas un remplaçant infaillible.
* **Amélioration Continue** : Le domaine progresse rapidement. Les techniques de filtrage, d'affinage et d'évaluation
  s'améliorent.
