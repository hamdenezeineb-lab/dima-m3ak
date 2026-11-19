# dima-m3ak
# Dima M3ak

### Plateforme intelligente d'aide à la décision ergonomique et jumeau numérique 3D
> **Du signal à l'action : écouter, comprendre et agir pour prévenir les
> troubles musculosquelettiques (TMS).**

Dima M3ak est une plateforme d'aide à la décision ergonomique conçue
pour relier quatre dimensions du travail : **Corps, Tâche, Poste et
Exposition**. Elle aide les professionnels de la prévention à repérer
les situations nécessitant une investigation, à documenter les
évaluations et à suivre les améliorations.

Le cas d'étude de référence est le **poste 3.2 -- Montage chez LEONI**,
caractérisé dans le dossier par des faisceaux pouvant contenir jusqu'à
430 fils, une cadence de 13 faisceaux par heure et un temps de cycle de
276 secondes.
------------------------------------------------------------------------

## 🎯 Objectifs

Dima M3ak vise à :

-   Faciliter le signalement volontaire des gênes ressenties au travail.
-   Relier les signalements aux tâches, aux zones corporelles et aux
    facteurs d'exposition.
-   Aider à analyser les postures et les mouvements répétitifs.
-   Faire ressortir les situations qui méritent une investigation
    prioritaire.
-   Visualiser le poste de travail à l'aide d'un jumeau numérique 3D.
-   Comparer les évaluations avant et après la mise en place
    d'améliorations.

**La plateforme assiste les professionnels : elle ne remplace ni
l'opérateur, ni l'ergonome, ni le responsable HSE.**

## 🏭 Contexte et problème

Le poste 3.2 -- Montage comprend principalement les opérations suivantes
:

1.  Insérer ou encliqueter les cosses.
2.  Raccorder les composants sur le gabarit.
3.  Enrubanner les faisceaux.

La répétition des gestes et les contraintes du poste peuvent solliciter
différentes zones du corps, notamment les épaules, les coudes, les
poignets et les mains.

Le but d'Dima M3ak est de mieux relier les difficultés signalées aux
tâches réellement effectuées et aux observations ergonomiques, afin de
faciliter le choix d'actions de prévention adaptées.

## 👥 Acteurs concernés

  -----------------------------------------------------------------------
  Acteur                              Rôle dans Dima M3ak
  ----------------------------------- -----------------------------------
  **Opératrice / opérateur**          Signale volontairement une gêne et
                                      participe au retour sur les
                                      améliorations.

  **Responsable HSE / ergonome**      Analyse les signalements, examine
                                      les évaluations et suit les
                                      interventions.

  **Ingénieur de conception /         Exploite les informations pour
  méthodes**                          étudier des améliorations du poste
                                      et des outils.
  -----------------------------------------------------------------------

L'opérateur reste au centre de la démarche : la plateforme ne supprime
aucune tâche et n'automatise pas le geste de travail.

## 🔄 Fonctionnement général

Le fonctionnement de la plateforme suit une chaîne en quatre étapes :

1.  **Collecter** --- recueillir les signalements volontaires et les
    observations du poste.
2.  **Organiser** --- associer les informations à une zone corporelle,
    une tâche et un poste.
3.  **Analyser** --- exploiter les observations et les évaluations
    ergonomiques.
4.  **Agir et suivre** --- faire ressortir les priorités, documenter les
    interventions et comparer les situations avant/après.

``` text
Signalement opérateur
        |
        v
Zone corporelle + intensité + tâche
        |
        v
Analyse ergonomique et observations
        |
        v
Lien Corps -> Tâche -> Poste -> Exposition
        |
        v
Priorisation et proposition d'intervention
        |
        v
Validation par le professionnel
        |
        v
Nouvelle évaluation après intervention
```

## 🧩 Fonctionnalités du dashboard

### 1. Automatic Posture Assessment

-   Capture vidéo locale par webcam.
-   Détection de repères corporels en temps réel avec MediaPipe Pose.
-   Extraction de 33 repères corporels et de leurs niveaux de
    visibilité.
-   Calcul géométrique des angles articulaires.
-   Filtrage des estimations instables et rejet des sauts aberrants.
-   Vérification de la vue caméra ; une vue sagittale est nécessaire
    pour l'analyse du cou et du tronc décrite dans le dossier.

Les facteurs qui ne peuvent pas être déterminés de façon fiable par la
caméra doivent être renseignés ou confirmés manuellement.

### 2. RULA / REBA Assessment

-   Moteurs de cotation déterministes basés sur les tables RULA et REBA.
-   Formulaire de confirmation des facteurs non visuels, comme la force,
    la prise et la torsion.
-   Sauvegarde des évaluations dans SQLite.
-   Refus de produire un score complet lorsque les informations
    manuelles nécessaires ne sont pas confirmées.

### 3. Worker Feedback

Un formulaire de signalement volontaire conçu pour être rempli en moins
de 20 secondes.

Informations recueillies :

-   Zone corporelle concernée.
-   Intensité de la gêne sur une échelle de 1 à 10.
-   Tâche réalisée.
-   Moment du poste.
-   Commentaire libre facultatif.

Le formulaire décrit dans le dossier ne collecte pas de nom, de
matricule ou de badge.

### 4. Digital Twin 3D

Jumeau numérique interactif développé avec Three.js et rendu dans le
navigateur.

Il permet notamment de :

-   Visualiser la table, le gabarit, les connecteurs et un mannequin.
-   Faire tourner la scène et zoomer.
-   Sélectionner les groupes de connecteurs A à D.
-   Modifier certains paramètres géométriques du poste.

Le dossier présente notamment une géométrie de référence avec une table
de 95 cm et une portée de 55 cm.

### 5. What-If Simulator

Le simulateur permet d'étudier des scénarios d'aménagement en faisant
varier certains paramètres, par exemple :

-   La hauteur des connecteurs.
-   La portée.
-   L'inclinaison.

Les résultats affichés sont des **estimations de simulation**. Ils ne
constituent pas des mesures ergonomiques réalisées sur le terrain.

### 6. AI Recommendations & Interventions

Le moteur de recommandations s'appuie sur des règles explicables qui
relient :

-   La fréquence et l'intensité des gênes.
-   Les tâches concernées.
-   Les zones du poste.
-   Les seuils et résultats des évaluations RULA/REBA.

Le suivi des interventions utilise un workflow allant de `Proposed` à
`Evaluated`. Les recommandations doivent être examinées et validées par
les professionnels concernés.

------------------------------------------------------------------------

## 🏗️ Architecture technique

Le dossier décrit une application locale organisée autour des
technologies suivantes :

  -----------------------------------------------------------------------
  Couche                  Technologies            Responsabilité
  ----------------------- ----------------------- -----------------------
  Interface web           React, TypeScript       Interface et composants
                                                  interactifs du
                                                  dashboard

  Visualisation 3D        Three.js / WebGL        Jumeau numérique et
                                                  paramètres géométriques

  API backend             Python, FastAPI         Communication et
                                                  traitement local

  Vision par ordinateur   OpenCV, MediaPipe       Détection des repères
                                                  et analyse géométrique

  Calcul numérique        NumPy                   Calcul et traitement
                                                  des angles

  Base de données         SQLite                  Stockage des
                                                  signalements et
                                                  évaluations
  -----------------------------------------------------------------------

### Vue simplifiée de l'architecture

``` text
┌──────────────────────────────────────────┐
│           Interface React / TS           │
│ Dashboard · Feedback · RULA/REBA · 3D    │
└────────────────────┬─────────────────────┘
                     │ API REST
┌────────────────────▼─────────────────────┐
│             Backend FastAPI              │
│ Traitement local · Règles · Évaluations  │
└───────────┬───────────────────┬──────────┘
            │                   │
┌───────────▼──────────┐  ┌─────▼──────────┐
│ OpenCV + MediaPipe   │  │ SQLite         │
│ Repères et angles    │  │ Données utiles │
└──────────────────────┘  └────────────────┘

        Three.js / WebGL
        Jumeau numérique 3D
```

Le traitement vidéo décrit est effectué localement. Le backend utilise
une API REST asynchrone et SQLite pour les données persistées. Le
dossier indique qu'une migration vers PostgreSQL est envisageable pour
un déploiement multi-lignes.

## 🧠 Méthodes et briques d'analyse

  -----------------------------------------------------------------------
  Brique                  Rôle                    Justification
  ----------------------- ----------------------- -----------------------
  **MediaPipe Pose        Extrait 33 repères      Fonctionnement en temps
  Landmarker              corporels à partir des  réel sur CPU standard,
  (BlazePose)**           images.                 sans GPU coûteux.

  **OpenCV + NumPy**      Calcule les angles et   Réduit le bruit,
                          filtre les estimations. détecte les valeurs
                                                  aberrantes et aide à
                                                  contrôler la fiabilité.

  **RULA**                Évalue les postures et  Méthode reconnue et
                          les contraintes         résultats explicables.
                          associées.              

  **REBA**                Complète l'évaluation   Permet d'examiner
                          posturale.              différentes postures et
                                                  zones corporelles.

  **Moteur de corrélation Relie gêne, tâche, zone Produit des
  par règles**            du poste et             recommandations
                          évaluations.            traçables, sans
                                                  prétendre à un
                                                  diagnostic clinique.

  **Three.js**            Affiche le poste en 3D. Visualisation
                                                  interactive dans un
                                                  navigateur, sans
                                                  logiciel CAO lourd.
  -----------------------------------------------------------------------

**Important :** la caméra ne mesure pas tous les facteurs ergonomiques.
La force, la qualité de la prise ou certaines contraintes doivent être
confirmées par une personne compétente. Un score complet ne doit pas
être inventé lorsque les informations requises sont absentes.

## 🔎 Transparence : réel, démo et simulation

Pour présenter le prototype de façon rigoureuse, il est essentiel de
distinguer les fonctionnalités opérationnelles des données de
démonstration et des résultats simulés.

  -----------------------------------------------------------------------
  Module                  Statut décrit dans le   Précision
                          dossier                 
  ----------------------- ----------------------- -----------------------
  Automatic Posture       **Réel / Live**         Capture locale,
  Assessment                                      MediaPipe Pose, calcul
                                                  et filtrage des angles.

  RULA / REBA Assessment  **Réel / Live**         Moteurs de cotation et
                                                  confirmation manuelle
                                                  des facteurs requis.

  Worker Feedback         **Réel / Live**         Formulaire anonyme et
                                                  enregistrement local.

  Digital Twin 3D         **Réel + données de     Scène 3D interactive ;
                          simulation**            certains scores et
                                                  géométries sont des
                                                  données de
                                                  démonstration.

  What-If Simulator       **Simulation**          Les variations
                                                  affichées sont des
                                                  estimations, pas des
                                                  mesures terrain.

  Overview, Body & Task   **Demo Data**           Les graphiques et
  Analysis                                        indicateurs affichés
                                                  utilisent des données
                                                  synthétiques de
                                                  démonstration.

  AI Recommendations,     **Règles + données de   Le moteur de
  Interventions &         démonstration**         corrélation est basé
  Economic Impact                                 sur des règles ; les
                                                  fiches, interventions
                                                  et hypothèses
                                                  financières
                                                  illustratives doivent
                                                  être validées.
  -----------------------------------------------------------------------

Les données de démonstration sont notamment identifiées dans l'interface
par un badge `DEMO DATA`.

### Exemples de données de démonstration

Le dossier cite notamment :

-   KPI de démonstration : 72/100.
-   10 opérateurs.
-   Indicateur de gêne : 7/10 pour l'épaule gauche.
-   Répartition illustrative du cycle : 98 s / 74 s / 62 s / 42 s sur
    276 s.
-   Exemple de hotspot : Groupe A à 81/100.
-   Exemple de variation simulée : 72 → 48, soit une réduction projetée
    de 33 %.

Ces valeurs illustrent l'interface et ne doivent pas être présentées
comme des mesures réelles effectuées chez LEONI.

## 🔐 Confidentialité et facteur humain

Dima M3ak est conçu autour des principes suivants :

-   **Pas de remplacement humain :** aucune tâche n'est supprimée ou
    automatisée par la plateforme.
-   **Participation volontaire :** l'opérateur peut signaler une gêne et
    contribuer aux améliorations.
-   **Données minimisées :** le formulaire de signalement ne demande pas
    de nom, de matricule ou de badge.
-   **Traitement vidéo local :** les images sont traitées localement et
    ne sont pas stockées sous forme identifiable, selon l'architecture
    décrite.
-   **Résultats agrégés :** les tableaux de bord destinés à l'entreprise
    présentent des informations regroupées par poste.
-   **Pas de classement individuel :** les données ne doivent pas servir
    à sanctionner ou classer les opérateurs.

## 📊 Impact et validation

### Impact opérationnel démontré par le prototype

Le dossier identifie plusieurs capacités opérationnelles :

-   Signalement anonyme d'une gêne en moins de 20 secondes.
-   Pré-calcul local des angles articulaires.
-   Pré-remplissage des évaluations RULA/REBA.
-   Identification plus rapide du couple tâche × composant.
-   Participation directe des opérateurs à la réflexion sur le poste.

### Impact industriel à mesurer lors d'un pilote

Les bénéfices suivants restent à confirmer par des essais sur le terrain
:

-   Réduction des scores RULA/REBA après réaménagement physique.
-   Diminution de la fréquence et de l'intensité des gênes déclarées.
-   Évolution de l'absentéisme et du turnover potentiellement liés aux
    TMS.
-   Rentabilité réelle du déploiement.

### Protocole de validation

1.  Réaliser une première évaluation ergonomique du poste.
2.  Recueillir les signalements volontaires.
3.  Identifier les tâches et zones qui nécessitent une investigation.
4.  Proposer et mettre en place une amélioration physique.
5.  Réaliser une nouvelle évaluation RULA/REBA confirmée par un
    ergonome.
6.  Recueillir de nouveaux retours des opérateurs.
7.  Comparer les résultats avant et après.

> **Règle de preuve :** une simulation What-If ne remplace jamais une
> mesure réelle. L'efficacité d'une modification doit être vérifiée
> après son installation physique.

## 💰 Coût et modèle économique

Le dossier privilégie du matériel standard et des logiciels open source
pour limiter le coût et faciliter la maintenance en Tunisie.

### Estimation du MVP

  Poste                                      Estimation
  ------------------------------ ----------------------
  Développement du MVP                4 000 à 8 000 TND
  Mise en service et formation          500 à 1 500 TND
  Hébergement                       50 à 150 TND / mois
  Maintenance                      800 à 2 000 TND / an

Ces montants sont des estimations préliminaires à confirmer par des
devis.

### Retour sur investissement

Pour une hypothèse de **10 postes**, le simulateur économique du dossier
estime un délai de retour sur investissement (*payback*) d'environ **10
mois**, avec une fourchette de **6,3 à 25 mois** selon les scénarios.

Ce résultat est une hypothèse de simulation. Il doit être recalibré avec
les coûts, les données de production et les indicateurs réels de
l'entreprise.

## 🚀 Installation et lancement

### Environnement décrit

-   Node.js pour l'interface React / TypeScript.
-   Python pour le backend FastAPI.
-   Webcam locale pour l'évaluation posturale.
-   Navigateur compatible avec WebGL pour le jumeau numérique 3D.

### Lancement

Le dossier technique indique une application locale accessible à
l'adresse :

``` text
http://localhost:5173
```

**Note :** le dossier ne fournit pas les commandes exactes
d'installation, les fichiers de dépendances ni les variables
d'environnement. Les commandes ci-dessous devront être ajoutées à partir
du dépôt source réel afin de ne pas inventer une procédure de lancement.

## 🛣️ Limites et évolutions

Les prochaines étapes possibles sont :

-   Tester la solution dans des conditions réelles au poste 3.2.
-   Valider les évaluations avec un ergonome.
-   Remplacer progressivement les données de démonstration par des
    données terrain autorisées et anonymisées.
-   Vérifier les recommandations avec les responsables HSE et les
    ingénieurs.
-   Mesurer les effets des aménagements physiques.
-   Étudier le passage de SQLite à PostgreSQL pour un déploiement
    multi-lignes.
-   Recalibrer le modèle économique avec les données réelles de
    l'entreprise.

## 🤝 Équipe et contribution

Dima M3ak est un projet de prévention des TMS associant ergonomie,
vision par ordinateur, développement web et visualisation 3D.

Les contributions peuvent porter sur :

-   L'amélioration de l'interface utilisateur.
-   Les méthodes d'évaluation ergonomique.
-   La visualisation 3D du poste.
-   La protection des données.
-   Les tests et la validation sur le terrain.

------------------------------------------------------------------------

## 📌 Résumé

**Dima M3ak transforme les signalements et les observations
ergonomiques en informations structurées pour aider les professionnels à
mieux cibler les actions de prévention.**

**Écouter. Comprendre. Agir.**

------------------------------------------------------------------------

*Document de présentation technique établi à partir du dossier
Dima M3ak --- Architecture, IA, Conformité & Impact. Les statuts des
fonctionnalités et les chiffres de démonstration doivent être
interprétés selon les distinctions précisées dans ce README.*
