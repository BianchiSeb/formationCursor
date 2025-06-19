# Concepts Clés

## Le Token

* **Comment l'IA "voit" et "manipule" le texte ? Les Tokens.**
    * Quand une IA générative comme ChatGPT travaille avec du texte, elle ne voit pas les mots comme nous. Elle
      décompose le texte en plus petites unités appelées **tokens**.
    * Un token peut être un mot entier ('chat'), une partie d'un mot ('généra-' '-tive'), un signe de
      ponctuation ('.', '?'), ou même un caractère.
    * *Analogie* : Imaginez les tokens comme des briques de Lego. L'IA apprend comment ces briques s'assemblent pour
      former des phrases, des paragraphes, des textes cohérents.
* **Pourquoi les tokens sont importants ?**
    * C'est l'unité de base avec laquelle l'IA "pense" et "écrit".
    * Pendant son apprentissage, l'IA apprend à prédire le token suivant le plus probable dans une séquence. Si elle
      voit "Le chat est sur le...", elle va prédire que "tapis", "toit", ou "lit" sont des tokens probables pour suivre,
      basés sur tout ce qu'elle a lu.
    * Quand elle génère du texte, elle choisit un token, puis un autre, et ainsi de suite, en essayant toujours de faire
      la suite la plus logique et cohérente possible par rapport à ce qu'elle a appris et à l'instruction qu'on lui a
      donnée (le prompt).

## Le Transformer

* **L'idée clé** : Les Transformers sont très forts pour comprendre l'importance de chaque mot dans une phrase (ou pixel
  dans une image) en regardant *tous les autres mots (ou pixels) en même temps*.
* **L'explication** :
    * Imaginez que vous lisez une très longue phrase, ou même un paragraphe entier. Pour bien comprendre le sens d'un
      mot précis, vous ne regardez pas seulement ce mot isolé. Vous regardez les mots qui viennent avant, ceux qui
      viennent après, et même ceux qui sont plus loin mais qui sont liés.
    * Par exemple, dans la phrase : "La **banque** où j'ai déposé mon argent est au bord de la rivière." Le mot "banque"
      pourrait signifier un banc pour s'asseoir ou un établissement financier. C'est en regardant "déposé mon argent"
      et "rivière" que vous comprenez de quelle "banque" il s'agit.
    * Les **Transformers**, c'est un peu comme un expert en contexte super intelligent. Quand on leur donne du texte (ou
      une image), ils ont un mécanisme spécial appelé **"attention"**.
    * Ce mécanisme d'attention leur permet de peser l'importance de chaque mot par rapport à tous les autres mots de la
      phrase, simultanément. Ils peuvent "voir" quelles parties du texte sont les plus pertinentes pour comprendre un
      mot donné, même si ces parties sont éloignées.
    * C'est grâce à ça qu'ils sont si bons pour comprendre le sens profond du langage, les nuances, et même pour générer
      des textes longs et cohérents. Ils ne se contentent pas de prédire le mot suivant en regardant juste les quelques
      mots précédents, ils ont une vision globale du contexte.

## L’Embedding

### 1. Le Problème : Comment Donner du Sens aux Tokens pour l'IA ?

* L'IA a besoin de comprendre que "chat" est plus proche de "chien" ou "animal" que de "voiture" ou "manger".
* Elle a besoin de capturer les nuances : "roi" est à "reine" ce que "homme" est à "femme".
* Comment représenter numériquement ces relations et ce sens ?

### 2. La Solution : Les Vecteurs (Word Embeddings) - La "Carte d'Identité" Sémantique des Tokens

* **L'Idée** : Au lieu d'un simple numéro d'identification, chaque token va être représenté par une liste de nombres,
  appelée un **vecteur** (ou "embedding" en anglais, qu'on pourrait traduire par "plongement" ou "incorporation").
* **Analogie Visuelle (2D/3D simplifiée)** :
    * Imaginez un grand espace, comme une carte. Chaque token va être placé comme un point sur cette carte.
    * La position de ce point (ses coordonnées sur la carte) est définie par les nombres de son vecteur.
    * Et la magie, c'est que les tokens qui ont des sens similaires ou qui sont souvent utilisés dans des contextes
      similaires vont se retrouver proches les uns des autres sur cette carte.
* **Plus en détail (mais toujours simple)** :
    * Ce vecteur n'a pas seulement 2 ou 3 nombres (comme sur une carte simple), mais souvent des **centaines de nombres
      ** (par exemple, 768 ou 1536 nombres pour les grands modèles) !
    * Chacun de ces nombres dans le vecteur représente une sorte de caractéristique abstraite du token, apprise par l'IA
      pendant son entraînement. On ne sait pas toujours exactement à quoi correspond chaque dimension, mais l'ensemble
      capture des relations sémantiques.
    * Par exemple (c'est une simplification extrême !), une dimension pourrait représenter "animalité", une autre "objet
      manufacturé", une autre "action", etc. Le token "chat" aurait une valeur élevée pour "animalité" et basse pour "
      objet manufacturé".
* **Comment sont-ils appris ?**
    * Ces vecteurs sont **appris automatiquement** pendant l'entraînement du modèle sur des milliards de phrases.
    * L'IA apprend que les mots qui apparaissent dans des contextes similaires (par exemple, "Le ___ miaule" et "J'ai
      caressé le ___") doivent avoir des vecteurs similaires.
    * C'est un des aspects fondamentaux du Machine Learning appliqué au langage.

### 3. Pourquoi c'est Puissant ? (Note : La numérotation a été ajustée pour la cohérence)

* **Calcul de Similarité** : L'IA peut maintenant mesurer la similarité sémantique entre deux tokens simplement en
  comparant leurs vecteurs (par exemple, en calculant la "distance" entre leurs points sur la carte).
* **Analogies** : Elle peut faire des "opérations mathématiques" sur ces vecteurs pour découvrir des analogies.
  L'exemple classique est : `Vecteur('Roi') - Vecteur('Homme') + Vecteur('Femme') ≈ Vecteur('Reine')`. (Peut-être un peu
  avancé pour les débutants, mais fascinant).
* **Base pour les Transformers** : Ces vecteurs de tokens sont ensuite l'information d'entrée que les Transformers vont
  manipuler avec leur mécanisme d'attention pour comprendre le contexte global et générer du texte. Le Transformer ne
  travaille pas sur les ID des tokens, mais sur ces représentations vectorielles riches en sens.
