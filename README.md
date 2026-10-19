# Première réunion avec le tuteur

20 octobre 2026 — Trame proposée : 6 diapositives, 10 à 12 minutes, puis discussion.

Objectif : vérifier ma compréhension des données et convenir de la prochaine étape. Les formulations à l’oral sont des propositions à adapter à ce que je sais réellement expliquer.

## 1. Mon point de départ et l’objectif de la réunion — 1 minute

**À afficher**

- Formation en Data Science et IA, expérience en Python et NLP.
- Première prise en main des données cliniques et protéomiques.
- Aujourd’hui : clarifier les données et définir les priorités de travail.

**À dire**

« J’ai commencé à lire l’article et à explorer les fichiers. Mon parcours est surtout en data et en IA, et je découvre la biologie de la leucémie. J’ai donc préparé un état des lieux et quelques questions pour vérifier ma compréhension avant d’aller plus loin. »

Ton CV permet de situer ton expérience technique, notamment en IA/NLP chez Greenpharma. Cette expérience ne suppose pas une formation en biologie. Inutile de détailler tes outils ou de présenter tout ton CV. Si le tuteur connaît déjà ton parcours, cette introduction tient en vingt secondes.

## 2. La question du projet telle que je la comprends — 1 à 2 minutes

**À afficher**

« Les mesures de protéines peuvent-elles apporter une information supplémentaire sur la survie des patients, au-delà des données cliniques disponibles ? »

- L’article décrit des groupes de patients à partir de leurs profils protéiques.
- Je souhaite préciser la place de ces groupes dans notre projet.
- Question au tuteur : quelle est la priorité de la première phase ?

**À dire**

« Dans ma lecture, les auteurs montrent que les profils de protéines peuvent apporter une information complémentaire. J’ai notamment retenu le groupe appelé Mito-AML, associé dans cette étude à une plus forte abondance de protéines mitochondriales et à une survie plus courte. J’aimerais vérifier si notre priorité est de retrouver ces groupes, d’étudier des associations avec la survie ou, à terme, de faire de la prédiction. »

**À garder en tête**

Ces trois objectifs demandent des analyses différentes. Retrouver un groupe ne prouve pas qu’on prédit correctement la survie d’un nouveau patient. Les cinq groupes décrits par l’article ne doivent pas être présentés comme une classification universelle de toute la maladie. Mito-AML est un résultat des auteurs, pas une découverte personnelle ni une conclusion déjà reproduite.

## 3. Les données disponibles — 2 minutes

**À afficher**

| Élément | État des lieux |
| --- | --- |
| Cohorte de découverte | 177 patients |
| Informations cliniques | Caractéristiques des patients, suivi et événements |
| Mesures de protéines | Environ 6 500 groupes protéiques dans le tableau non imputé |
| Versions du protéome | Non imputée et imputée |
| Deuxième cohorte | 75 patients, comparabilité à examiner |

**À dire**

« On dispose de beaucoup de mesures pour un nombre assez limité de patients. Je voudrais d’abord établir précisément quelles informations sont disponibles pour chaque patient, à quel moment elles ont été recueillies et lesquelles sont communes aux différentes cohortes. »

**Questions à poser**

- Que représentent les valeurs de protéines et quelles transformations ont-elles déjà subi ?
- Les mesures moléculaires correspondent-elles uniquement au prélèvement initial, ou existe-t-il des prélèvements répétés ?
- Quelles données complémentaires sont accessibles, notamment les étiquettes des groupes de l’article ?

**Note personnelle**

Le classeur contient 6 536 groupes protéiques avant imputation et 5 207 dans la version imputée. L’article mentionne 6 522 protéines. Conserver cet écart en réserve, sans encombrer la diapositive. Dire « environ 6 500 groupes protéiques » évite de confondre un nombre de lignes du fichier avec un décompte biologique déjà réconcilié. Un suivi clinique au fil du temps n’implique pas que les protéines ont été mesurées plusieurs fois.

## 4. Les points à clarifier avant l’analyse — 3 minutes

**À afficher**

| Observation | Question pour la suite |
| --- | --- |
| 67 décès observés et 110 suivis censurés | Pourquoi et quand le suivi s’arrête-t-il ? |
| Environ 15 % de mesures manquantes dans le protéome non imputé | Comment les absences ont-elles été traitées ? |
| Trois profils très incomplets : F11, F86, F132 | Existe-t-il une explication technique ? |
| Certaines variables décrivent la réponse ou le traitement | À quel moment souhaite-t-on utiliser les informations ? |

**À dire**

« J’ai identifié quelques points qui changent la manière d’analyser les données. Pour la survie, une fin de suivi sans décès observé ne donne pas la durée de vie finale. Pour les protéines, je voudrais comprendre l’origine des valeurs manquantes et la préparation de la version imputée. Enfin, il faut préciser si l’objectif se situe au diagnostic ou plus tard, car les informations disponibles changent. »

**Exemple à avoir sous la main**

Deux patients ont une durée OS de 18 mois. Pour le premier, un décès est enregistré à 18 mois. Pour le second, le suivi s’arrête à 18 mois sans décès enregistré. Ces observations ont des significations différentes. Le second patient apporte de l’information jusqu’à cette date. Il ne faut ni inventer sa date de décès, ni le considérer comme vivant indéfiniment, ni l’exclure simplement pour cette raison.

**Questions prioritaires**

- Quelle date constitue le début du suivi ? Une mise à jour du suivi existe-t-elle ?
- Dispose-t-on du protocole ou du code de filtrage, normalisation et imputation ?
- Comment décider du traitement des trois profils très incomplets ?
- Si l’objectif concerne le diagnostic, quelles variables sont réellement connues à ce moment-là ?

**Note personnelle**

F11, F86 et F132 dépassent chacun 50 % de mesures protéiques manquantes dans les vérifications existantes. Leur exclusion reste une décision à justifier. La censure du suivi et les valeurs manquantes des protéines sont deux problèmes différents. Une valeur absente peut aussi correspondre à une variable non applicable : il faut comprendre sa définition avant de la remplir.

## 5. Le travail proposé pour la prochaine étape — 2 minutes
