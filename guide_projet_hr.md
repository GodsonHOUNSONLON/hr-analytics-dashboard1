# Guide complet : HR Analytics — Power BI en 5 jours

---

## INSTRUCTIONS POUR NOTEBOOKLM (à lire avant de générer la présentation)

Ce document est un guide pédagogique destiné à un étudiant débutant qui souhaite apprendre Power BI de façon professionnelle et créer un projet portfolio pour son CV.

**Consignes de génération de la présentation :**

- **Ton** : pédagogique, tutoiement constant, encourageant, accessible. Aucun jargon non expliqué.
- **Structure** : une section par journée (Jour 0 à Jour 5 + Conclusion). Dans chaque jour, décompose en plusieurs slides simples.
- **Règle d'or** : **une slide = une idée claire**. Pas de slide fourre-tout. Les slides doivent être courtes.
- **Style visuel attendu** : écrans sombres style macOS, flèches jaunes manuscrites, post-its verts, captures annotées.
- **Checkpoints** : après chaque étape importante, insérer une slide "Checkpoint : ce que tu dois avoir fait".
- **GitHub continu** : à la fin de chaque journée, une slide dédiée "Commit du jour" avec la commande Git exacte à taper.
- **Chaque bloc de code** (DAX, Bash) doit apparaître **en entier** sur une slide dédiée.
- **Cible de volume** : viser environ 50 à 60 slides au total.

---

## CONTEXTE DU PROJET

**Qui tu es :** étudiant en école d'ingénieur ou en formation data, niveau débutant en Power BI. Tu as des bases en Excel et SQL. Tu n'as jamais publié de dashboard professionnel.

**Ce que tu vas construire :** un projet Power BI complet baptisé **"HR Analytics Dashboard"** qui analyse les départs d'employés (attrition) dans une entreprise fictive — 1 470 employés réels du dataset IBM HR. Tu vas couvrir tout le cycle Power BI : import, nettoyage, modélisation simple, DAX, dashboards, publication.

**Pourquoi ce projet va te faire recruter :**
- Il utilise les **outils exactement demandés** dans les offres Data Analyst 2026 : Power Query, DAX, modélisation, Power BI Service
- Le sujet **People Analytics / RH** est un domaine en pleine explosion — toutes les grandes boîtes ont une équipe dédiée
- Il démontre que tu comprends un **enjeu business critique** : l'attrition coûte cher (recrutement, formation, productivité)
- Il est **publié en ligne** (Power BI Service + GitHub) : un recruteur peut interagir en 30 secondes

**À la fin des 5 jours, tu auras :**
- Un fichier `.pbix` propre et publié sur Power BI Service
- Un dépôt GitHub avec README, captures, et fichier source
- Une vidéo de démo de 2 minutes
- Un projet à mettre directement sur ton CV

---

## JOUR 0 — PRÉPARATION ET INSTALLATIONS

**Objectif :** avoir tous les comptes et outils prêts avant de commencer.

### Les 5 outils à installer

1. **Power BI Desktop** (gratuit, Windows uniquement) — l'outil principal. Télécharge depuis le Microsoft Store en cherchant "Power BI Desktop".
2. **Compte Microsoft** (gratuit) — nécessaire pour Power BI Service. Crée-le sur signup.live.com avec ton email étudiant si possible.
3. **Compte GitHub** (gratuit) — pour publier ton projet en portfolio. Crée-le sur github.com.
4. **Git** (gratuit) — pour synchroniser ton code avec GitHub. Télécharge sur git-scm.com.
5. **VS Code** (gratuit) — pour rédiger ton README. Télécharge sur code.visualstudio.com.

### Astuce : compte Microsoft étudiant

Si tu as un email `.edu` ou universitaire français (`prenom.nom@etu.univ-xxx.fr`), va sur **microsoft.com/education** et active un **compte Microsoft 365 Education gratuit**. Ça te donne accès à **Power BI Pro gratuit** et tu peux publier tes rapports en ligne. Sinon, tu utiliseras la version gratuite limitée — ça suffit pour le projet.

### Configuration de Git en local

Dans un terminal (PowerShell ou CMD), tape ces deux commandes :

```bash
git config --global user.name "Ton Prénom Nom"
git config --global user.email "ton.email@gmail.com"
```

### Vérification

```bash
git --version
```

Power BI Desktop : ouvre-le, accepte les conditions.

### Checkpoint fin Jour 0

Tu dois avoir : Power BI Desktop qui s'ouvre, un compte GitHub fonctionnel, Git qui répond à `git --version`, VS Code installé.

---

## JOUR 1 — CADRAGE MÉTIER ET IMPORT DES DONNÉES

**Objectif :** poser le contexte métier, importer les données dans Power BI et faire le premier nettoyage avec Power Query.

### Étape 1 : Comprendre le contexte fictif

Tu vas incarner un Data Analyst dans l'équipe **People Analytics** d'une entreprise. La directrice des Ressources Humaines te demande trois choses :

- Comprendre **qui part** (profil démographique des employés qui démissionnent)
- Comprendre **pourquoi ils partent** (salaire, ancienneté, satisfaction, équilibre de vie)
- Identifier les **départements à risque** pour cibler les actions de rétention

L'enjeu business est énorme : remplacer un employé coûte en moyenne **6 à 9 mois de salaire** entre le recrutement, la formation et la perte de productivité.

### Étape 2 : Lister tes 8 KPIs métiers

Voici les KPIs que tu vas calculer et afficher :

- Nombre total d'employés
- Taux d'attrition global (% de départs)
- Nombre d'employés partis vs restés
- Salaire mensuel moyen
- Ancienneté moyenne
- Taux d'attrition par département
- Taux d'attrition par tranche d'âge
- Score moyen de satisfaction au travail

### Étape 3 : Télécharger le dataset

Va sur **kaggle.com** et cherche **"IBM HR Analytics Employee Attrition"** (auteur : Pavansubhash T). Télécharge le zip.

Dézippe sur ton bureau. Tu obtiens **un seul fichier** : `WA_Fn-UseC_-HR-Employee-Attrition.csv` (~1 470 lignes, 35 colonnes).

C'est un dataset **propre et bien structuré** : pas de valeurs manquantes, pas de colonnes multi-valeurs. Idéal pour se concentrer sur Power BI sans galérer avec le nettoyage.

### Étape 4 : Renommer le fichier

Pour faire plus simple, renomme le fichier en `hr_data.csv`.

### Étape 5 : Créer le dépôt GitHub

Sur github.com, **New repository**. Nomme-le **`hr-analytics-dashboard`**. Coche **Add a README file**. **Create repository**.

### Étape 6 : Cloner le dépôt

Dans un terminal :

```bash
cd Documents
git clone https://github.com/TON_USERNAME/hr-analytics-dashboard.git
cd hr-analytics-dashboard
```

### Étape 7 : Créer la structure du projet

Dans le dossier cloné, crée cette arborescence :

```
hr-analytics-dashboard/
├── README.md
├── data/
├── powerbi/
├── docs/
└── .gitignore
```

Place `hr_data.csv` dans `data/`.

### Étape 8 : Ouvrir Power BI Desktop et importer le CSV

Lance **Power BI Desktop**.

Clique sur **Obtenir des données** → **Texte/CSV** → sélectionne `hr_data.csv` → **Ouvrir**.

Une fenêtre d'aperçu apparaît. Vérifie l'**Origine du fichier** → choisis **65001: Unicode (UTF-8)**.

Clique sur **Transformer les données** pour ouvrir Power Query Editor.

### Étape 9 : Renommer la requête

Renomme la requête en `Employees` (clic droit → **Renommer**).

### Étape 10 : Vérifier les types de colonnes principales

Pour chaque colonne, vérifie le type via l'icône à gauche du nom.

Colonnes texte (catégorielles) :
- `Attrition`, `BusinessTravel`, `Department`, `EducationField`
- `Gender`, `JobRole`, `MaritalStatus`, `OverTime`

Colonnes nombres entiers :
- `Age`, `DailyRate`, `DistanceFromHome`, `Education`
- `EmployeeCount`, `EmployeeNumber`, `EnvironmentSatisfaction`
- `HourlyRate`, `JobInvolvement`, `JobLevel`, `JobSatisfaction`
- `MonthlyIncome`, `MonthlyRate`, `NumCompaniesWorked`
- `PercentSalaryHike`, `PerformanceRating`, `RelationshipSatisfaction`
- `StandardHours`, `StockOptionLevel`, `TotalWorkingYears`
- `TrainingTimesLastYear`, `WorkLifeBalance`, `YearsAtCompany`
- `YearsInCurrentRole`, `YearsSinceLastPromotion`, `YearsWithCurrManager`

Power BI fait normalement bien la détection automatique. Vérifie juste qu'il n'y a pas d'erreurs.

### Étape 11 : Supprimer les colonnes inutiles

Certaines colonnes ne servent à rien pour l'analyse (valeurs constantes pour tout le monde) :

- `EmployeeCount` (toujours = 1)
- `Over18` (toujours = "Y")
- `StandardHours` (toujours = 80)

Sélectionne ces 3 colonnes (Ctrl + clic sur les en-têtes) → clic droit → **Supprimer les colonnes**.

### Étape 12 : Créer une colonne "Attrition_Flag" pour faciliter les calculs

Plus tard pour les mesures DAX, on va vouloir compter les départs facilement. Créons une colonne 1/0 dès maintenant.

Dans Power Query : **Ajouter une colonne** → **Colonne conditionnelle**.
- **Nouveau nom de colonne** : `Attrition_Flag`
- **Si** : `Attrition` **égal à** `Yes` **alors** `1`
- **Sinon** : `0`

Clique sur **OK**.

Vérifie que le type de la nouvelle colonne est **Nombre entier** (clique sur l'icône à gauche du nom).

### Étape 13 : Créer une colonne "Tranche d'âge"

Pour faciliter l'analyse par segment d'âge.

**Ajouter une colonne** → **Colonne conditionnelle**.
- **Nom** : `AgeGroup`
- **Si** `Age` **inférieur à** `30` **alors** `< 30 ans`
- **Sinon si** `Age` **inférieur à** `40` **alors** `30-39 ans`
- **Sinon si** `Age` **inférieur à** `50` **alors** `40-49 ans`
- **Sinon** `50+ ans`

Type : **Texte**.

### Étape 14 : Créer une colonne "Tranche d'ancienneté"

Pareil pour l'ancienneté dans l'entreprise.

**Ajouter une colonne** → **Colonne conditionnelle**.
- **Nom** : `TenureGroup`
- **Si** `YearsAtCompany` **inférieur à** `2` **alors** `< 2 ans`
- **Sinon si** `YearsAtCompany` **inférieur à** `5` **alors** `2-4 ans`
- **Sinon si** `YearsAtCompany` **inférieur à** `10` **alors** `5-9 ans`
- **Sinon** `10+ ans`

Type : **Texte**.

### Étape 15 : Charger les données dans Power BI

Clique sur **Fermer et appliquer**. Power BI charge la table `Employees`.

### Étape 16 : Sauvegarder le fichier .pbix

**Fichier** → **Enregistrer sous** → place-le dans `hr-analytics-dashboard/powerbi/hr_dashboard.pbix`.

### Étape 17 : Premier commit GitHub

```bash
git add .
git commit -m "Jour 1 : Import HR data + nettoyage Power Query (colonnes utiles + tranches d'âge/ancienneté)"
git push origin main
```

### Checkpoint fin Jour 1

Tu dois avoir : 1 table `Employees` propre dans Power BI avec 32 colonnes utiles, 3 colonnes ajoutées (`Attrition_Flag`, `AgeGroup`, `TenureGroup`), ton fichier `.pbix` sauvegardé, ton premier commit visible sur GitHub.

---

## JOUR 2 — ORGANISATION ET TABLE MESURES

**Objectif :** organiser proprement le modèle et préparer la table dédiée aux mesures DAX.

### Étape 1 : Pourquoi un modèle simple ici

Contrairement à un projet e-commerce avec plusieurs tables, ici tu n'as **qu'une seule table**. Pas besoin de modélisation Star Schema complexe : chaque ligne représente un employé avec toutes ses caractéristiques.

C'est **une bonne chose pour un débutant** : tu te concentres sur les visuels et le DAX, pas sur la modélisation.

En entretien, tu pourras dire : *"Le dataset étant déjà dénormalisé en une table d'employés, j'ai privilégié la simplicité du modèle. Pour un cas avec historique de mouvements, j'aurais ajouté une dimension temporelle et une table de faits."*

### Étape 2 : Créer la table mesures dédiée

Bonne pratique pro : ranger toutes les mesures DAX dans une table dédiée pour les organiser.

**Données** → **Entrer des données** → tape une colonne fictive avec une valeur quelconque → nomme la table `_Mesures` → **Charger**.

Le préfixe `_` la fait apparaître en haut de la liste. Tu y rangeras toutes tes mesures demain.

### Étape 3 : Vérifier l'organisation des champs

Bascule en vue **Modèle**. Tu vois :
- Une grosse table `Employees` (avec 35 colonnes)
- Une petite table `_Mesures`

C'est normal et propre.

### Étape 4 : Catégoriser les colonnes utiles

Certaines colonnes peuvent gagner à être catégorisées pour Power BI :

Sélectionne `Department` → ruban **Outils de colonne** → **Trier par colonne** : laisse comme c'est.

Pour `AgeGroup` et `TenureGroup`, on va définir un **ordre d'affichage personnalisé** plus tard via une astuce DAX (sinon Power BI les trie alphabétiquement, ce qui mettrait "10+ ans" avant "2-4 ans").

### Étape 5 : Créer une colonne d'ordre pour AgeGroup

Va en vue **Données**. Sélectionne la table `Employees`. Clique sur **Nouvelle colonne** :

```dax
AgeGroup_Order =
SWITCH(
    Employees[AgeGroup],
    "< 30 ans", 1,
    "30-39 ans", 2,
    "40-49 ans", 3,
    "50+ ans", 4,
    99
)
```

Ensuite, sélectionne la colonne `AgeGroup` → ruban **Outils de colonne** → **Trier par colonne** → choisis `AgeGroup_Order`.

Maintenant `AgeGroup` s'affichera dans le bon ordre dans tous les visuels.

### Étape 6 : Créer une colonne d'ordre pour TenureGroup

Idem, **Nouvelle colonne** :

```dax
TenureGroup_Order =
SWITCH(
    Employees[TenureGroup],
    "< 2 ans", 1,
    "2-4 ans", 2,
    "5-9 ans", 3,
    "10+ ans", 4,
    99
)
```

Trier `TenureGroup` par `TenureGroup_Order`.

### Étape 7 : Sauvegarder et commit

```bash
git add .
git commit -m "Jour 2 : Table _Mesures + colonnes d'ordre pour AgeGroup et TenureGroup"
git push origin main
```

### Checkpoint fin Jour 2

Tu dois avoir : la table `_Mesures` créée, deux colonnes d'ordre ajoutées, et les colonnes `AgeGroup`/`TenureGroup` qui se trient correctement quand tu les utilises dans un visuel test.

---

## JOUR 3 — MESURES DAX

**Objectif :** écrire les mesures DAX qui calculeront tes KPIs métiers. **C'est le cœur technique du projet.**

### Étape 1 : Comprendre ce qu'est une mesure DAX

Une **mesure DAX** est un calcul dynamique qui s'adapte au contexte du visuel. Exemple : la mesure `Taux Attrition` peut afficher 16% globalement, mais 25% dans un graphique filtré sur le département Sales — c'est la même mesure.

C'est la grande force de Power BI sur Excel.

### Étape 2 : Créer la mesure Total Employés

Dans la vue **Données**, clique sur la table `_Mesures`. Clique sur **Nouvelle mesure** dans le ruban.

```dax
Total Employés = COUNTROWS(Employees)
```

Format : **Nombre entier** avec séparateur de milliers.

### Étape 3 : Créer les mesures de comptage des départs

```dax
Nombre Départs = SUM(Employees[Attrition_Flag])
```

```dax
Nombre Restés = [Total Employés] - [Nombre Départs]
```

Format : **Nombre entier**.

### Étape 4 : Créer la mesure star : le Taux d'Attrition

C'est la mesure la plus importante du projet.

```dax
Taux Attrition = DIVIDE([Nombre Départs], [Total Employés])
```

Format : **Pourcentage** avec **1 décimale**.

**Note** : on utilise `DIVIDE` plutôt que `/` car ça gère automatiquement les divisions par zéro.

### Étape 5 : Créer les mesures financières

```dax
Salaire Mensuel Moyen = AVERAGE(Employees[MonthlyIncome])
```

Format : **Devise** ($) avec **0 décimales**.

```dax
Salaire Total = SUM(Employees[MonthlyIncome])
```

Format : **Devise** ($).

### Étape 6 : Créer les mesures d'ancienneté et d'âge

```dax
Ancienneté Moyenne = AVERAGE(Employees[YearsAtCompany])
```

Format : **Nombre décimal** avec **1 décimale**.

```dax
Âge Moyen = AVERAGE(Employees[Age])
```

Format : **Nombre décimal** avec **0 décimales**.

### Étape 7 : Créer les mesures de satisfaction

Le dataset contient plusieurs scores de satisfaction (de 1 à 4). On va calculer leurs moyennes.

```dax
Satisfaction Travail Moy = AVERAGE(Employees[JobSatisfaction])
```

```dax
Équilibre Vie Pro Moy = AVERAGE(Employees[WorkLifeBalance])
```

```dax
Satisfaction Environnement Moy = AVERAGE(Employees[EnvironmentSatisfaction])
```

Format : **Nombre décimal** avec **2 décimales**.

### Étape 8 : Créer une mesure conditionnelle pour qualifier l'attrition

Cette mesure affichera un statut visuel selon le niveau de risque.

```dax
Niveau Risque =
SWITCH(
    TRUE(),
    [Taux Attrition] > 0.20, "🔴 Critique",
    [Taux Attrition] > 0.15, "🟡 Élevé",
    [Taux Attrition] > 0.10, "🟢 Modéré",
    "🔵 Faible"
)
```

### Étape 9 : Créer une mesure de comparaison

Ce sera utile pour comparer un sous-groupe à la moyenne globale.

```dax
Taux Attrition Global =
CALCULATE(
    [Taux Attrition],
    ALL(Employees)
)
```

Format : **Pourcentage** avec **1 décimale**.

Cette mesure donne **toujours** le taux global (16,1%), même quand un filtre est appliqué. Pratique pour comparer.

### Étape 10 : Créer une mesure d'écart à la moyenne

```dax
Écart Attrition vs Global = [Taux Attrition] - [Taux Attrition Global]
```

Format : **Pourcentage** avec **1 décimale**.

Avec cette mesure, un département à 25% d'attrition affichera +8,9% (par rapport au global de 16,1%). Très parlant en visuel.

### Étape 11 : Tester rapidement les mesures

Bascule en vue **Rapport**. Crée une **Carte** (visuel) → dépose `Total Employés`. Tu dois voir **1 470**.

Crée une autre carte avec `Taux Attrition`. Tu dois voir environ **16,1%**.

Une autre avec `Salaire Mensuel Moyen` → environ **6 503 $**.

Si les valeurs sont très différentes, vérifie tes mesures.

### Étape 12 : Supprimer la colonne fantôme dans _Mesures

Dans la table `_Mesures`, supprime la colonne fictive que tu avais créée pour fonder la table. Clic droit sur la colonne → **Supprimer**.

### Étape 13 : Sauvegarder et commit

```bash
git add .
git commit -m "Jour 3 : 11 mesures DAX (taux attrition, salaires, satisfaction, comparaisons)"
git push origin main
```

### Checkpoint fin Jour 3

Tu dois avoir 11 mesures DAX qui retournent des valeurs cohérentes :
- Total Employés ≈ 1 470
- Nombre Départs ≈ 237
- Taux Attrition ≈ 16,1%
- Salaire Mensuel Moyen ≈ 6 503 $
- Ancienneté Moyenne ≈ 7 ans
- Âge Moyen ≈ 37 ans

---

## JOUR 4 — CONSTRUCTION DES DASHBOARDS

**Objectif :** transformer tes données en dashboards interactifs et visuellement professionnels.

### Étape 1 : Définir l'identité visuelle

Pour un dashboard RH, choisis une palette **professionnelle et sobre** :
- **Bleu marine** : `#1B3A57` (couleur principale)
- **Rouge alerte** : `#D62828` (pour signaler les départs)
- **Vert positif** : `#588157` (pour les indicateurs sains)
- **Gris clair** : `#F4F4F4` (fond)

### Étape 2 : Configurer le thème Power BI

**Affichage** → **Thèmes** → **Personnaliser le thème actuel** → définis tes 4 couleurs principales dans **Couleurs des données**.

### Étape 3 : Créer la page d'accueil

Bouton droit sur l'onglet **Page 1** en bas → **Renommer la page** → "Vue d'ensemble".

Insère un **Zone de texte** (ruban **Insertion**) en haut de la page :
- Titre : **👥 HR Analytics Dashboard**
- Sous-titre : *Analyse de l'attrition employés — 1 470 collaborateurs*

### Étape 4 : Vue d'ensemble — KPIs principaux

Place 4 **Cartes** côte à côte :
- Carte 1 : `Total Employés`
- Carte 2 : `Nombre Départs` (en rouge)
- Carte 3 : `Taux Attrition` (en rouge)
- Carte 4 : `Salaire Mensuel Moyen`

Pour chaque carte : dans **Format**, met un titre clair et une couleur de fond cohérente.

### Étape 5 : Vue d'ensemble — Graphique en anneau Restés vs Partis

Insère un **Graphique en anneau** (Donut chart) :
- Légende : crée une mesure rapide ou utilise `Attrition` directement
- Valeurs : `Total Employés`
- Couleurs : Vert pour "No" (restés), Rouge pour "Yes" (partis)

Titre : "Répartition Restés / Partis"

### Étape 6 : Vue d'ensemble — Attrition par département

Insère un **Graphique en barres horizontales** :
- Axe Y : `Department`
- Axe X : `Taux Attrition`
- Tri : décroissant par `Taux Attrition`
- Format conditionnel sur les barres : couleur dégradée du vert au rouge

Titre : "Taux d'attrition par département"

### Étape 7 : Vue d'ensemble — Attrition par tranche d'âge

Insère un **Graphique en colonnes** :
- Axe X : `AgeGroup`
- Axe Y : `Taux Attrition`
- Couleur : bleu marine

Titre : "Taux d'attrition par tranche d'âge"

### Étape 8 : Créer la page "Profils & Démographie"

Bouton droit sur **Vue d'ensemble** → **Dupliquer la page** → renomme en "Profils".

Sur cette page, garde les 4 KPIs en haut, supprime les autres visuels et ajoute :

- **Graphique en barres** : Attrition par sexe (`Gender` × `Taux Attrition`)
- **Graphique en barres** : Attrition par statut marital (`MaritalStatus` × `Taux Attrition`)
- **Graphique en colonnes** : Attrition par niveau d'études (`Education` × `Taux Attrition`)
- **Graphique en colonnes** : Attrition par tranche d'ancienneté (`TenureGroup` × `Taux Attrition`)

### Étape 9 : Créer la page "Satisfaction & Conditions"

Duplique encore. Renomme en "Satisfaction".

- **3 cartes** en haut avec les scores de satisfaction :
  - `Satisfaction Travail Moy`
  - `Équilibre Vie Pro Moy`
  - `Satisfaction Environnement Moy`

- **Graphique en colonnes** : Attrition par score de satisfaction au travail
  - Axe X : `JobSatisfaction` (de 1 à 4)
  - Axe Y : `Taux Attrition`

- **Graphique en colonnes** : Attrition par équilibre vie pro
  - Axe X : `WorkLifeBalance` (de 1 à 4)
  - Axe Y : `Taux Attrition`

- **Graphique en barres** : Attrition selon les heures sup
  - Axe Y : `OverTime` (Yes / No)
  - Axe X : `Taux Attrition`

### Étape 10 : Créer la page "Salaire & Carrière"

Duplique. Renomme en "Salaire & Carrière".

- **Graphique en colonnes** : Salaire moyen par département
  - Axe X : `Department`
  - Axe Y : `Salaire Mensuel Moyen`

- **Nuage de points (Scatter chart)** : relation salaire vs ancienneté
  - Axe X : `YearsAtCompany`
  - Axe Y : `MonthlyIncome`
  - Légende : `Attrition` (pour voir où sont les départs)
  - Détails : `EmployeeNumber`

- **Graphique en barres** : Attrition par niveau hiérarchique
  - Axe Y : `JobLevel` (1 à 5)
  - Axe X : `Taux Attrition`

- **Graphique en colonnes** : Attrition par fréquence de promotion
  - Axe X : `YearsSinceLastPromotion`
  - Axe Y : `Taux Attrition`

### Étape 11 : Ajouter les filtres globaux (Slicers)

Sur chaque page, ajoute 2 **Segments** en haut :
- `Department` (liste déroulante)
- `Gender` (boutons)

Pour rendre les slicers globaux à toutes les pages, va dans **Affichage** → **Synchroniser les segments** → coche les pages où tu veux qu'ils filtrent.

### Étape 12 : Créer la navigation entre pages

Sur chaque page, place 4 boutons en haut (ruban **Insertion** → **Boutons** → **Vide**) :
- "Vue d'ensemble" → action : **Navigation de page** → Vue d'ensemble
- "Profils" → action : **Navigation de page** → Profils
- "Satisfaction" → action : **Navigation de page** → Satisfaction
- "Salaire & Carrière" → action : **Navigation de page** → Salaire & Carrière

### Étape 13 : Page bonus "Insights RH"

Crée une nouvelle page : "Insights".

C'est la page narrative qui fait la différence en entretien. Place 4 zones de texte avec tes interprétations métier :

1. **"Les heures supplémentaires sont le facteur #1 d'attrition"**
   *Les employés en heures sup ont un taux d'attrition de 30,5%, contre 10,4% sans heures sup.*

2. **"Les jeunes (< 30 ans) partent 2x plus que les autres"**
   *Taux d'attrition de 27,9% chez les < 30 ans, contre 12,8% pour les 30-39 ans.*

3. **"Les célibataires sont plus enclins à partir"**
   *Taux d'attrition de 25,5% pour les célibataires, contre 10,1% pour les mariés.*

4. **"Le département Sales a le plus haut taux d'attrition"**
   *20,6% au département Sales, contre 13,8% en R&D.*

À côté de chaque texte, place un visuel mini correspondant.

### Étape 14 : Polir l'ensemble

- Vérifie que tous les visuels sont alignés (utilise les guides automatiques)
- Pas deux titres en doublon sur une page
- Polices cohérentes (titres 14pt, axes 10pt)
- Tous les `Taux Attrition` formatés en %

### Étape 15 : Sauvegarder et commit

```bash
git add .
git commit -m "Jour 4 : 5 pages dashboards (Vue d'ensemble, Profils, Satisfaction, Salaire, Insights)"
git push origin main
```

### Checkpoint fin Jour 4

Tu dois avoir : 5 pages de rapport navigables, des slicers synchronisés, un thème cohérent, et au moins 4 insights métiers explicités sur la page Insights.

---

## JOUR 5 — PUBLICATION ET PORTFOLIO

**Objectif :** publier le rapport en ligne et créer un portfolio GitHub présentable.

### Étape 1 : Créer un compte Power BI Service

Va sur **app.powerbi.com**. Connecte-toi avec ton compte Microsoft (idéalement étudiant `.edu` qui te donne Power BI Pro gratuit).

Si on te demande "où veux-tu créer ton espace ?", choisis **Mon espace de travail**.

### Étape 2 : Publier le rapport depuis Power BI Desktop

Dans Power BI Desktop : ruban **Accueil** → **Publier** → **Mon espace de travail** → **Sélectionner**.

Patiente quelques secondes. Tu verras un message "Publication réussie" avec un lien.

### Étape 3 : Ouvrir le rapport en ligne

Clique sur le lien fourni. Vérifie que tout fonctionne : navigation, filtres, visuels.

### Étape 4 : Activer le partage public

Pour qu'un recruteur puisse voir ton dashboard sans compte :
- Dans Power BI Service, ouvre ton rapport
- **Fichier** → **Incorporer un rapport** → **Publier sur le Web (public)**
- Lis l'avertissement
- Clique sur **Créer le code incorporé**
- Récupère le **lien** et le **code iframe**

⚠️ Le dataset IBM HR est public, donc aucun problème de confidentialité.

### Étape 5 : Capturer les 5 dashboards

Utilise l'**Outil Capture d'écran** Windows pour faire 5 captures soignées (une par page) et place-les dans `docs/`.

Nomme-les : `dashboard_1_vue_ensemble.png`, `dashboard_2_profils.png`, `dashboard_3_satisfaction.png`, `dashboard_4_salaire.png`, `dashboard_5_insights.png`.

### Étape 6 : Rédiger le README pro

Ouvre `README.md` dans VS Code. Remplace tout par :

```markdown
# 👥 HR Analytics Dashboard — Power BI

## 📋 Contexte
Dashboard Power BI complet d'analyse de l'attrition employés
sur un échantillon de 1 470 collaborateurs (dataset IBM HR Analytics).

## 🎯 Objectifs métiers
- Identifier les profils à risque de départ (démographie, ancienneté)
- Comprendre les facteurs d'attrition (satisfaction, salaire, équilibre vie pro)
- Cibler les départements prioritaires pour les actions de rétention

## 🛠️ Stack Technique
- **Power BI Desktop** — modélisation et visualisation
- **Power Query** — nettoyage et création de colonnes catégorielles
- **DAX** — mesures de taux, comparaisons, indicateurs conditionnels
- **Power BI Service** — publication en ligne
- **Git / GitHub** — versioning

## 📊 Dashboards
- **Vue d'ensemble** : KPIs et taux par département
- **Profils** : démographie des partants
- **Satisfaction** : impact des conditions de travail
- **Salaire & Carrière** : relation rémunération / progression
- **Insights** : 4 prises de position métier

![Vue ensemble](docs/dashboard_1_vue_ensemble.png)
![Profils](docs/dashboard_2_profils.png)
![Satisfaction](docs/dashboard_3_satisfaction.png)

## 🧮 Mesures DAX clés
- Taux d'attrition global et par segment
- Comparaison par rapport au taux global (ALL)
- Mesures conditionnelles SWITCH (niveau de risque visuel)
- Moyennes pondérées (salaire, ancienneté, satisfaction)

## 💡 Top 4 insights
1. **Heures sup = facteur #1** — 30,5% d'attrition vs 10,4% sans heures sup
2. **Les < 30 ans partent 2x plus** — 27,9% vs 12,8% pour les 30-39 ans
3. **Célibataires plus enclins à partir** — 25,5% vs 10,1% pour les mariés
4. **Département Sales en alerte** — 20,6% vs 13,8% en R&D

## 🔗 Liens
- 🌐 [Dashboard en ligne](LIEN_POWER_BI)
- 🎬 [Démo vidéo Loom (2 min)](LIEN_LOOM)
- 📁 [Fichier .pbix](powerbi/hr_dashboard.pbix)

## 👤 Auteur
Ton Prénom Nom — [LinkedIn](https://linkedin.com/in/ton-profil)
```

### Étape 7 : Créer le .gitignore

À la racine du projet, crée un fichier `.gitignore` :

```
.DS_Store
*.tmp
~$*
```

### Étape 8 : Vérifier la taille du fichier .pbix

Power BI peut créer des fichiers lourds. Si ton `.pbix` dépasse 100 Mo, GitHub refusera le push.

Vérifie : clic droit sur `hr_dashboard.pbix` → **Propriétés** → taille.

Avec ce dataset (1 470 lignes seulement), tu seras largement sous la limite. Aucun risque.

### Étape 9 : Enregistrer une vidéo de démo (2 minutes)

Utilise **Loom** (gratuit). Plan suggéré :
- **0:00 - 0:15** : qui tu es, contexte du projet, enjeu business de l'attrition
- **0:15 - 0:45** : tu montres la vue d'ensemble et les 2-3 KPIs clés
- **0:45 - 1:15** : tu cliques sur Profils et Satisfaction, tu commentes les insights
- **1:15 - 1:45** : tu montres la page Insights avec tes interprétations
- **1:45 - 2:00** : conclusion + call-to-action LinkedIn

Mets la vidéo sur Loom, récupère le lien, ajoute-le dans le README.

### Étape 10 : Mettre à jour le README avec les vrais liens

Remplace `LIEN_POWER_BI` et `LIEN_LOOM` par tes vrais liens.

### Étape 11 : Commit final

```bash
git add .
git commit -m "Jour 5 : Publication Power BI Service + README pro + démo vidéo"
git push origin main
```

### Étape 12 : Post LinkedIn

Template :

> 👥 Je viens de finaliser un projet Power BI sur l'analyse de l'attrition employés (1 470 collaborateurs analysés) !
>
> 📊 5 dashboards interactifs :
> → Vue d'ensemble & KPIs RH
> → Profils démographiques
> → Satisfaction & conditions de travail
> → Salaire & carrière
> → Insights stratégiques
>
> 🛠️ Stack : Power BI, DAX (taux, comparaisons globales, SWITCH), Power Query
>
> 💡 Insight clé : les heures supplémentaires sont le facteur n°1 d'attrition (30,5% vs 10,4% sans heures sup).
>
> 🎯 Je recherche une **alternance Data Analyst à partir de septembre 2026**.
>
> 👉 Dashboard live : [lien]
> 🎬 Démo 2 minutes : [lien]
> 💻 Code & .pbix : [lien GitHub]
>
> #PowerBI #DataAnalyst #PeopleAnalytics #Alternance #DAX

### Checkpoint final

Tu dois avoir :
- ✅ Un dashboard Power BI publié et accessible en ligne
- ✅ Un dépôt GitHub avec README, captures, et fichier `.pbix`
- ✅ Une vidéo Loom de 2 minutes
- ✅ Un post LinkedIn publié
- ✅ Une ligne sur ton CV avec ce projet

---

## CONCLUSION ET PROCHAINES ÉTAPES

### Ce que tu sais faire maintenant

**Compétences techniques :**
- Power Query (nettoyage, types, colonnes conditionnelles)
- Modélisation simple et tables dédiées (mesures, ordres)
- DAX : mesures de taux (DIVIDE), comparaisons (CALCULATE + ALL), indicateurs conditionnels (SWITCH), agrégations
- Visualisation : choix de visuels adaptés, mise en forme, navigation, slicers synchronisés
- Publication Power BI Service

**Compétences métier :**
- Analyse RH / People Analytics
- Identification de facteurs d'attrition
- Storytelling data avec interprétations actionnables
- Compréhension d'enjeux business RH

### Ce que tu vas mettre sur ton CV

```
Projet HR Analytics Dashboard — Power BI (Projet personnel, 2026)
- Analyse de l'attrition employés sur un échantillon de 1 470 collaborateurs
- 11 mesures DAX (taux d'attrition, comparaisons globales avec ALL, SWITCH)
- 5 pages de rapport interactives avec navigation et page Insights métier
- Publication sur Power BI Service avec partage public
- Stack : Power BI, DAX, Power Query, Git
- [Lien Power BI] | [Démo vidéo] | [GitHub]
```

### Les 5 questions que les recruteurs vont te poser

1. **"Pourquoi avoir choisi un dataset RH ?"**
   - Le People Analytics est un domaine en pleine expansion
   - L'attrition est un enjeu business critique (coût élevé du remplacement)
   - Permet de montrer une compréhension business au-delà de la pure technique

2. **"Différence entre une mesure et une colonne calculée ?"**
   - Une **colonne calculée** est calculée une fois au chargement, stockée dans le modèle, occupe de la mémoire
   - Une **mesure** est calculée dynamiquement selon le contexte du visuel, ne stocke rien
   - Règle : préférer les mesures, sauf si on a besoin de filtrer/grouper sur la valeur (comme `AgeGroup`)

3. **"À quoi sert CALCULATE et la fonction ALL ?"**
   - `CALCULATE` modifie le contexte de filtre d'une mesure
   - `ALL(table)` retire tous les filtres appliqués à une table
   - Ensemble : `CALCULATE([X], ALL(table))` calcule X en ignorant les filtres → utile pour comparer un sous-groupe au total

4. **"Quel est ton insight le plus fort et comment l'as-tu trouvé ?"**
   - Préparer une réponse précise : "Les heures supplémentaires sont le facteur le plus discriminant : 30,5% d'attrition contre 10,4%. J'ai détecté ça en croisant `OverTime` avec mon taux d'attrition dans un graphique en barres."
   - Insister sur la **démarche** plus que sur le chiffre

5. **"Comment optimiser un rapport avec beaucoup de données ?"**
   - Star Schema strict (pas pertinent ici, mais à connaître)
   - Mesures plutôt que colonnes calculées
   - Limiter le nombre de visuels par page (max 6-8)
   - Désactiver l'auto date/time dans les options
   - Supprimer les colonnes inutiles dans Power Query

### Pour aller plus loin

- **Certification Microsoft PL-300** (Power BI Data Analyst) — 165€, ultra valorisée
- Ajouter une **modélisation prédictive** dans Power BI (Quick Insights ou Key Influencers)
- Mettre en place du **Row Level Security** (un manager ne voit que son équipe)
- Connecter le rapport à une base SQL Server au lieu d'un CSV
- Apprendre **Tabular Editor** (outil pro pour DAX avancé, gratuit)

### Message final

Tu viens de boucler un projet Power BI complet en 5 jours sur un sujet **stratégique pour les entreprises**. Tu as un dashboard publié, un GitHub propre, et 11 mesures DAX que tu peux expliquer. Tu es prêt pour les premiers entretiens.

**Bonne chance !**
