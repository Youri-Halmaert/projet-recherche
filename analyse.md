# Analyses des cohortes allemandes et chinoises

## Cohorte chinoise : étape 05

Ouvrir **05_chine_survie.ipynb** pour l'analyse indépendante des 374 patients chinois : référence âge + sexe + ELN 2017, modèles protéomique et combiné, survie globale (OS) et survie sans événement (EFS, secondaire). La validation interne est imbriquée (5 × 3 partitions), avec standardisation apprise sur les seuls patients d'entraînement. Les fichiers disponibles ne contiennent ni rémission CR1 ni cohorte chinoise externe.

Le protocole est dans `PROTOCOLE_05_CHINE.md` et les résultats dans `outputs/05_chine_survie/`, avec une `SYNTHESE.md`, les prédictions hors entraînement, calibration, incertitude conditionnelle et stabilité des protéines. Les valeurs fournies sont conservées sans nouveau logarithme ; leur correction initiale des lots sur l'ensemble de la cohorte reste une limite. La population inclut PML::RARA, des mineurs et plusieurs traitements : les scores ne sont pas directement comparables aux scores allemands.

```powershell
& '.venv/Scripts/python.exe' 'scripts/run_china_validation.py'
& '.venv/Scripts/python.exe' 'scripts/report_china_validation.py'
& '.venv/Scripts/python.exe' 'scripts/execute_notebook.py' --source '05_chine_survie.py'
```

## Étape actuelle : données imputées, sexe, survie, rémission et validation

Ouvrir **04_impute_sexe_remission_validation.ipynb**. Il présente les résultats enregistrés du nouveau protocole sur les 177 patients de découverte et les 75 patients de validation. La référence clinique contient âge, sexe et ELN ; la survie globale et CR1 sont deux tâches distinctes.

La source est la feuille `Proteome impute log2` du classeur dans `données allemandes/données scalées/`. Les z-scores globaux descriptifs ne sont pas utilisés pour évaluer les modèles. L'analyse porte sur 3 823 gènes communs avec correspondance explicite. L'harmonisation externe utilise une règle fixée avant les scores : z-score par protéine dans chaque cohorte, avec adaptation aux 75 protéomes sans leurs issues.

Le protocole est dans `PROTOCOLE_04_IMPUTE_VALIDATION.md`. Les résultats, verrous, prédictions, figures, contrôles et modèles sont dans `outputs/04_impute_sexe_remission_validation/`. Consulter `SYNTHESE.md` pour les conclusions et limites. Les modèles et prédictions ont été figés avant évaluation externe ; une reprise d'export, documentée dans `external_receipt.json`, n'a modifié ni modèles ni prédictions.

Les commandes de calcul sont `scripts/run_imputed_validation.py prepare`, puis `internal`, puis `external`. Ne pas relancer ces étapes pour choisir une nouvelle méthode après examen des résultats externes. Le programme refuse de réentraîner les modèles finaux existants et de refaire une évaluation terminée. Une reprise de restitution utilise les prédictions déjà figées.

Pour régénérer uniquement la restitution et le notebook :

```powershell
& '.venv/Scripts/python.exe' 'scripts/report_imputed_validation.py'
& '.venv/Scripts/python.exe' 'scripts/execute_notebook.py' --source '04_impute_sexe_remission_validation.py'
```

Les étapes 01 à 03 ci-dessous conservent le protocole historique et ses résultats. Elles n'intègrent pas automatiquement les changements de l'étape 04.

## Première analyse de la cohorte de découverte

Ouvrir **01_prise_en_main.ipynb**. Le notebook présente le dictionnaire des variables, les contrôles d'intégrité, la description clinique, les courbes Kaplan-Meier, la qualité du protéome non imputé et une PCA exploratoire. Les commentaires et sorties sont en français.

Il lit uniquement **Data S1 Discovery Cohort.xlsx**. L'ancien notebook, les deux anciens scripts d'analyse et leurs cinq figures ont été supprimés à la demande de l'utilisateur, après vérification de la nouvelle analyse. La cohorte de validation reste réservée pour une étape ultérieure.

## Exécution

L'environnement `.venv` du projet contient les dépendances nécessaires. Dans VS Code ou un éditeur Jupyter, sélectionner son interpréteur Python, puis exécuter les cellules dans l'ordre.

Pour reconstruire et exécuter depuis le dossier du projet dans PowerShell :

```powershell
& '.venv/Scripts/python.exe' 'scripts/execute_notebook.py'
```

Les cellules sont également disponibles dans `01_prise_en_main.py`, au format texte avec séparateurs `# %%`. **La commande de reconstruction remplace le notebook par ces cellules** : reporter les modifications éventuelles du notebook dans ce fichier avant de reconstruire. La commande s'arrête sur une erreur et conserve les sorties déjà exécutées pour faciliter le diagnostic.

Pour recréer les dépendances dans un environnement Python 3.12 :

```powershell
python -m venv .venv
& '.venv/Scripts/python.exe' -m pip install -r 'requirements-analysis.txt'
```

## Résultats

- `outputs/01_prise_en_main/SYNTHESE.md` : chiffres et points à discuter avec le tuteur.
- `outputs/01_prise_en_main/figures/` : six figures en PNG.
- `outputs/01_prise_en_main/*.csv` : inventaire, dictionnaires et tableaux descriptifs.
- `outputs/01_prise_en_main/manifest.json` : empreinte SHA-256 du classeur, versions et paramètres.

Les tableaux et figures de ce dossier sont régénérés lors d'une exécution. Les classeurs sources ne sont jamais écrits. Les matrices préparées restent en mémoire dans le notebook, avec les patients en lignes et les groupes protéiques en colonnes.

## Choix à connaître

- La deuxième ligne des feuilles protéomiques contient des noms d'acquisition. Les annotations sont dans les quatre dernières colonnes. F103 est conservé comme patient.
- Les valeurs manquantes sont décrites **avant** imputation. Les accessions restent les clés des groupes protéiques, y compris lorsque le symbole de gène est absent.
- La survie utilise le couple durée observée / indicateur de décès. Une médiane de survie non atteinte n'est pas remplacée par la médiane arithmétique des durées observées.
- La PCA descriptive filtre à au moins 80 % de valeurs observées et à une variance positive, impute par médiane et standardise. Elle ne reproduit pas la PCA probabiliste de l'article et ne mesure aucune performance prédictive.
- Les variables obtenues après traitement sont identifiées dans le dictionnaire. Les valeurs FLT3ITD VAF supérieures à 1 sont signalées sans correction arbitraire.

## Associations pronostiques

Ouvrir **02_associations_pronostiques.ipynb** pour l'étape suivante. L'analyse principale retire provisoirement F11, F86 et F132 : 174 patients et 66 décès observés. Le notebook descriptif initial reste à 177 patients et documente la décision.

Cette analyse teste chaque groupe protéique en Cox univarié et en Cox ajusté sur l'âge et ELN. Elle utilise les mesures observées, sans imputation, avec des effectifs par protéine explicitement rapportés. Les p-values sont corrigées par Benjamini-Hochberg. Des diagnostics des risques proportionnels, des sensibilités ciblées et des analyses de voies Reactome/MitoCarta complètent les résultats.

```powershell
& '.venv/Scripts/python.exe' 'scripts/run_associations.py'
& '.venv/Scripts/python.exe' 'scripts/execute_notebook.py' --source '02_associations_pronostiques.py' --timeout 1800
```

Le moteur réutilise les résultats uniquement si les empreintes des sources, du protocole, du code et des références sont identiques. Le calcul complet dure plusieurs minutes et utilise deux processus. Les références publiques sont conservées dans `data/references/` ; leurs URL et empreintes figurent dans le manifeste de cette étape.

Les résultats de l'étape 2 sont dans `outputs/02_associations_pronostiques/` :

- `SYNTHESE.md` : résultats et limites pour le tuteur.
- `cox_toutes_proteines.csv` : tous les tests, états numériques, effectifs, HR, p et q.
- `proteines_fdr05_ajustees.csv` : associations ajustées retenues à FDR 5 %.
- `enrichissements_voies.csv` et `cox_scores_mitochondriaux.csv` : exploration biologique complète.
- `diagnostics_risques_proportionnels.csv` et `sensibilites_candidats.csv` : contrôles ciblés sur les trente associations les mieux classées.
- `figures/` : figures intégrées au notebook.

Les diagnostics et sensibilités sur les candidats sélectionnés sont exploratoires. Ils ne constituent pas une validation indépendante. À la fin de cette étape d'associations, aucun modèle de prédiction individuelle n'est évalué ; l'étape 3 ci-dessous apporte ensuite une validation interne. La cohorte de validation n'est pas utilisée.

Les contrôles de chargement et de statistiques se lancent avec :

```powershell
& '.venv/Scripts/python.exe' -m unittest discover -s tests -v
```

## Stabilité et validation prédictive interne

**03_stabilite_prediction.ipynb** compare un Kaplan-Meier global, un Cox âge + ELN, un Cox Elastic Net protéomique et un modèle combiné. La procédure utilise les mêmes 174 patients, avec cinq partitions externes répétées trois fois et trois partitions internes. Toutes les transformations et la sélection sont apprises dans les sous-ensembles d'apprentissage ; la liste des sept associations ne présélectionne pas les modèles.

```powershell
& '.venv/Scripts/python.exe' 'scripts/run_prediction.py'
& '.venv/Scripts/python.exe' 'scripts/execute_notebook.py' --source '03_stabilite_prediction.py' --timeout 1800
```

Les résultats sont dans `outputs/03_stabilite_prediction/` :

- `SYNTHESE.md` et `comparaison_modeles.csv` : performances internes et limites.
- `metriques_partitions.csv`, `differences_appariees.csv` et `metriques_par_repetition.csv` : scores et comparaisons sur les mêmes partitions.
- `predictions_hors_apprentissage.csv` et `calibration_24_mois.csv` : probabilités obtenues sans entraîner sur le patient évalué, puis calibration descriptive.
- `stabilite_selection_proteines.csv` : fréquences de sélection dans quinze apprentissages externes qui se recouvrent.
- `bootstrap_candidats_resume.csv` : 150 rééchantillonnages conditionnels aux sept candidats précédents ; leurs percentiles ne corrigent pas le biais de sélection initial.
- `audit_partitions.json`, `choix_hyperparametres.csv`, `messages_numeriques.csv` et `manifest.json` : traçabilité des identifiants, paramètres, messages et versions.

Le calcul utilise deux processus et peut prendre plusieurs minutes. Les scores de Brier portent sur 12 et 24 mois, le Brier intégré sur 12-24 mois et le C-index de Uno sur les événements avant 36 mois. Une censure administrative à 48 mois est appliquée au calcul des métriques, avec estimation de la censure sur l'apprentissage ; les modèles utilisent les durées originales.

Les résultats externes ne sont pas utilisés. L'écart-type des partitions répétées décrit leur dispersion et ne constitue pas un intervalle de confiance de quinze expériences indépendantes. Le modèle final destiné à une validation externe devra être fixé et entraîné dans une étape distincte.

Après un arrêt numérique, les choix internes déjà terminés pour huit partitions ont été conservés avec leurs scores et empreintes ; le détail des réglages écartés et leurs messages numériques n'ont pas été conservés pour ces partitions. Les sept autres grilles internes sont complètes. Toutes les prédictions externes ont été recalculées en suivant un chemin de pénalisation du plus fort au réglage retenu, sans utiliser les résultats des tests pour choisir les paramètres. `provenance_reprise.json`, `parametres_partitions_terminees_avant_reprise.csv` et `moteur_avant_reprise.py` documentent cette reprise ; `choice_origin` identifie les choix conservés. Chaque partition terminée dispose désormais d'une sauvegarde complète dans `checkpoints/`.

Après exécution du notebook, `scripts/check_prediction_outputs.py` vérifie les identifiants, toutes les séparations internes et externes, les 2 088 prédictions, les paramètres retenus, les effectifs de sélection et les sorties du notebook. Il enregistre le résultat dans `verification.json`.
