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

**À afficher**

1. Construire un dictionnaire des variables : sens, unité, moment de mesure.
2. Documenter la qualité des données et les étapes de préparation existantes.
3. Réaliser quelques descriptions simples, puis les discuter ensemble.
4. Définir l’analyse suivante à partir de ces vérifications.

**À dire**

« Pour le prochain point, je propose de préparer un tableau des variables et un bilan de qualité, avec quelques graphiques simples. Nous pourrons ensuite choisir une première analyse adaptée à la question retenue. L’exploration des groupes peut être une piste si elle est utile au projet. »

**Livrable proposé**

Un notebook court et reproductible, accompagné d’une page de synthèse : données disponibles, points résolus, questions restantes. Prévoir deux ou trois graphiques au maximum, chacun associé à une question.

**Pistes à garder en réserve**

Une projection 2D des profils peut aider à décrire les ressemblances entre patients, mais elle demande déjà des choix de filtrage et d’imputation. Elle ne démontre pas à elle seule l’existence de sous-types biologiques. MOFA et la reproduction des 28 facteurs de l’article constituent un chantier distinct, à engager seulement si cela sert la priorité choisie et si les données nécessaires sont accessibles.

## 6. Les décisions à prendre ensemble — 1 minute

**À afficher**

- Quelle question traiter en premier ?
- Avec quelles données et quelles règles de préparation ?
- Quel livrable apporter au prochain rendez-vous ?

**À dire pour conclure**

« J’aimerais repartir avec une question prioritaire et un périmètre clair pour le prochain point. Est-ce que ce travail de description et de vérification vous paraît être la bonne première étape ? Quelles notions biologiques dois-je comprendre en priorité pour interpréter correctement les données ? »

Pendant la réunion, noter la décision, l’action à réaliser et les informations que le tuteur peut fournir. Fixer une échéance réaliste ensemble.

## Ce que j’ajouterais à tes notes

- **Une petite frise temporelle** : prélèvement initial, début du traitement, réponse à J15, suite du suivi. Demander au tuteur de confirmer l’ordre et les dates disponibles. Elle rend concrète la question « qu’est-ce qui est connu au moment où l’on veut estimer la survie ? ».
- **Un dictionnaire de données** : une colonne pour le nom informatique, une définition en français simple, l’unité et le moment de mesure. Demander également ce que signifie une case vide.
- **Une demande d’accompagnement biologique ciblée** : demander une ou deux ressources introductives et les quelques notions indispensables au projet. Tu peux demander un exemple d’interprétation d’un profil de patient sans demander un cours complet.
- **Une comparaison minimale des cohortes** : population incluse, traitements, période et technique de mesure. Tes hypothèses sur l’alimentation, le microbiote ou la culture ne sont pas documentées ici. Commencer par les différences observables.
- **Une distinction entre constat et proposition** : « j’ai observé », « les auteurs rapportent », « je propose » et « j’aimerais vérifier ». Utiliser ces formulations seulement quand elles décrivent fidèlement ton travail.

## Ce que je simplifierais ou reporterais

| Idée de tes notes | Formulation adaptée à cette première réunion |
| --- | --- |
| « Reconstruire » la survie des personnes encore suivies | Comprendre le suivi censuré et la manière de le prendre en compte. |
| Choisir KNN ou MICE | Comprendre pourquoi les valeurs manquent et comment les auteurs ont imputé. |
| Tracer chaque protéine contre la « durée de vie » | Commencer par décrire les mesures. Une durée de suivi censurée ne se lit pas comme une durée de vie connue. |
| Retrouver les clusters avec PCA, UMAP, K-means | Demander si reproduire les groupes est une priorité et si leurs étiquettes sont disponibles. |
| « Valeurs fausses dans le papier » | Présenter un écart précis entre sources et demander son explication. |
| Faire deux modèles, avant et après traitement | D’abord définir le moment de la question. Une analyse après J15 exige un cadre temporel adapté. |
| Absence de patients sains | Vérifier leur utilité pour la question retenue. Comparer la survie entre patients atteints de LAM ne requiert pas automatiquement un groupe sain. |
| Reproduire les 28 facteurs MOFA ou trouver de nouveaux sous-groupes | Conserver comme perspective, sans en faire un engagement pour la prochaine réunion. |
| Présenter la validation croisée | Garder le principe d’une évaluation sur des patients non utilisés pour ajuster la méthode, et reporter les détails. |

Pour une future évaluation prédictive, les étapes apprises sur les données, y compris l’imputation ou la sélection de variables, devront respecter la séparation entre apprentissage et évaluation. Cela justifie de comprendre la version déjà imputée, sans avoir à choisir une architecture demain.

## Questions de réserve si le tuteur souhaite approfondir

- Le sous-type Mito-AML est-il déjà attribué aux patients des fichiers ?
- La priorité porte-t-elle sur les protéines seules ou sur plusieurs types de données moléculaires ?
- Quelles différences entre cohortes limitent leur comparaison ou leur regroupement ?
- Quel horizon de suivi serait pertinent pour la question de recherche ?
- Existe-t-il des métadonnées de qualité des prélèvements et des lots de mesure ?
- Comment expliquer les écarts entre les nombres de protéines du texte et des fichiers ?

## Repères et sources

Trame reconstruite à partir des six photos du dossier `notes perso`, en tenant compte du CV fourni. Les chiffres sont repris des vérifications déjà présentes dans `outputs/01_prise_en_main/SYNTHESE.md` et `outputs/preparation_tuteur/verified_data.json`. Ils n’ont pas été recalculés dans cette préparation. Aucun modèle n’a été entraîné pour cette trame.

L’article fourni de Jayavelu et al., *The proteogenomic subtypes of acute myeloid leukemia*, Cancer Cell (2022), étaye les mentions des groupes protéomiques, de Mito-AML et de MOFA. Ces résultats restent attribués aux auteurs. [Article et DOI](https://doi.org/10.1016/j.ccell.2022.02.006).

Pour le vocabulaire, le [National Cancer Institute définit la survie globale](https://www.cancer.gov/publications/dictionaries/cancer-terms/def/overall-survival). Le point de départ exact doit être vérifié dans les données du projet. La [documentation scikit-learn sur les fuites de données](https://scikit-learn.org/stable/common_pitfalls.html) précise pourquoi les transformations apprises doivent utiliser seulement les données d’apprentissage.
