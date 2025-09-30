# Documentation Git - TechCorp Solutions

**Entreprise :** TechCorp Solutions  
**Équipe :** Beso (Lead Developer), Yewinthlaing04 (Developer), Adja (Developer), lewis (Developer)  
**Projet :** Group2   
**Repository :** https://github.com/besogogoladze/Group2

---

## Table des matières

1. [Introduction à TechCorp](#introduction)
2. [Comment utiliser Git - Guide complet](#guide-git)
3. [Notre workflow Gitflow](#workflow)
4. [Commandes essentielles](#commandes)
5. [Bonnes pratiques](#bonnes-pratiques)

---

## Introduction à TechCorp {#introduction}

Bienvenue chez TechCorp Solutions ! Ce document est votre guide pour comprendre comment nous utilisons Git dans notre équipe de 4 développeurs.


### Notre projet

- **Nom :** Group2
- **URL :** https://github.com/besogogoladze/Group2
- **Branches principales :** `main` et `dev1`

---

## Comment utiliser Git - Guide complet {#guide-git}

### Étape 1 : Installer Git

#### Windows
1. Télécharger Git depuis [git-scm.com](https://git-scm.com/)
2. Exécuter l'installateur
3. Suivre les étapes avec les options par défaut
4. Vérifier l'installation :
```bash
git --version
```

#### macOS
```bash
brew install git
```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git
```

### Étape 2 : Configurer Git (OBLIGATOIRE)

Avant de commencer, vous devez configurer votre identité :

```bash
# Votre nom (apparaîtra dans tous vos commits)
git config --global user.name "Votre Nom"

# Votre email
git config --global user.email "votre.email@techcorp.com"

# Vérifier que c'est bien configuré
git config --list
```

### Étape 3 : Cloner le projet TechCorp

```bash
# 1. Ouvrir votre terminal (Git Bash sur Windows)

# 2. Naviguer vers le dossier où vous voulez le projet
cd C:/Users/VotreNom/Documents

# 3. Cloner le repository
git clone https://github.com/besogogoladze/Group2.git

# 4. Entrer dans le dossier du projet
cd Group2
```

**Ce que vous avez maintenant :**
- Une copie complète du projet sur votre ordinateur
- Tout l'historique des commits
- Toutes les branches distantes

### Étape 4 : Voir les branches disponibles

```bash
# Voir les branches locales
git branch

# Résultat :
# * main    <- vous êtes sur main (étoile indique la branche actuelle)

# Voir TOUTES les branches (locales + distantes)
git branch -a

# Résultat :
# * main
#   remotes/origin/HEAD -> origin/main
#   remotes/origin/dev1
#   remotes/origin/main
```

### Étape 5 : Basculer sur la branche de développement

Chez TechCorp, nous travaillons sur la branche `dev1`, PAS sur `main`.

```bash
# Basculer vers dev1
git checkout dev1

# Résultat :
# Branch 'dev1' set up to track remote branch 'dev1' from 'origin'.
# Switched to a new branch 'dev1'

# Vérifier que vous êtes bien sur dev1
git branch

# Résultat :
# * dev1    <- l'étoile est maintenant sur dev1
#   main
```

### Étape 6 : Récupérer les dernières modifications

**TOUJOURS faire ceci avant de commencer à travailler :**

```bash
# Récupérer les modifications des autres développeurs
git pull origin dev1
```

**Pourquoi ?** Vos collègues ont peut-être poussé du code pendant que vous étiez absent. Vous devez avoir la dernière version.

### Étape 7 : Travailler sur les fichiers

```bash
# 1. Vérifier l'état actuel
git status

# 2. Modifier des fichiers
# Ouvrir README.md avec votre éditeur (VS Code, Notepad++, etc.)
# Faire vos modifications 

# 3. Voir ce qui a changé
git status
# Résultat : modified: README.md

git diff README.md
# Montre les lignes ajoutées/supprimées
```

### Étape 8 : Sauvegarder vos modifications (commit)

```bash
# 1. Ajouter les fichiers modifiés au staging
git add README.md
# OU ajouter tous les fichiers modifiés
git add .

# 2. Vérifier ce qui est prêt à être commité
git status
# Résultat : Changes to be committed: modified: README.md

# 3. Créer un commit avec un message clair
git commit -m "docs: ajout de ma section dans le README"
```

**Structure du message de commit :**
```
type: description courte

Types courants :
- docs: pour la documentation
- feat: pour une nouvelle fonctionnalité
- fix: pour une correction de bug
- style: pour du formatage
```

### Étape 9 : Envoyer vers GitHub

```bash
# 1. Pull avant de push (au cas où quelqu'un a pushé entre temps)
git pull origin dev1

# 2. Pousser vos commits
git push origin dev1
```

**Si conflit lors du pull :**
```bash
# Git vous dira quels fichiers ont des conflits
# Ouvrir ces fichiers, vous verrez :

<<<<<<< HEAD
Votre version
=======
Version de votre collègue
>>>>>>> dev1

# 3. Choisir quelle version garder ou combiner les deux
# 4. Supprimer les marqueurs <<<<<<< ======= >>>>>>>
# 5. Sauvegarder le fichier

# 6. Ajouter et commiter la résolution
git add README.md
git commit -m "merge: résolution conflit README"
git push origin dev1
```

### Résumé du cycle de travail quotidien

```bash
# Le matin en arrivant :
git checkout dev1
git pull origin dev1

# Pendant le travail :
# ... modifier des fichiers ...
git add .
git commit -m "type: description"

# Plusieurs fois dans la journée :
git pull origin dev1  # Récupérer le travail des autres
git push origin dev1  # Envoyer votre travail

# Avant de partir le soir :
git add .
git commit -m "docs: fin de journée"
git push origin dev1
```

---

## Notre workflow Gitflow {#workflow}

### Qu'est-ce que Gitflow ?

Gitflow est un modèle de gestion de branches Git qui organise le travail en équipe de manière structurée.

### Pourquoi nous utilisons Gitflow chez TechCorp

**Structure claire :** Deux branches principales (`main` et `dev1`)  
**Séparation des environnements :** 
- `main` = Production (code stable, testé)
- `dev1` = Développement (travail quotidien)

**Facilite la collaboration** entre nos 4 développeurs  
**Évite les bugs en production** grâce aux revues de code

### Structure de nos branches

```
main (PRODUCTION)
  │
  │ Merge seulement après validation complète
  │
  └── dev1 (DÉVELOPPEMENT)
        │
        │ Travail quotidien des 4 développeurs
        │
        ├── Beso travaille ici
        ├── Yewinthlaing04 travaille ici
        ├── Membre 3 travaille ici
        └── Membre 4 travaille ici
```

### Règles du workflow TechCorp

#### Règle 1 : Ne JAMAIS travailler directement sur main

```bash
# MAUVAIS ❌
git checkout main
git add .
git commit -m "modification"
git push origin main

# BON ✅
git checkout dev1
git add .
git commit -m "modification"
git push origin dev1
```

**Pourquoi ?** `main` est notre code de production. Un bug sur `main` affecte nos utilisateurs immédiatement.

#### Règle 2 : Toujours partir de dev1 à jour

```bash
# Avant de commencer à travailler
git checkout dev1
git pull origin dev1

# Maintenant vous avez la dernière version
# Vous pouvez travailler sans risque de conflit
```

#### Règle 3 : Commiter fréquemment

```bash
# Chaque fois que votre code fonctionne, commitez !

# Au lieu de :
# Travailler 4 heures → 1 gros commit

# Faire :
# Travailler 30 min → commit
# Travailler 30 min → commit
# Travailler 30 min → commit
# etc.
```

**Avantages :**
- Historique clair de ce qui a été fait
- Facile de revenir en arrière si problème
- Vos collègues voient votre progression

#### Règle 4 : Pull avant de push

```bash
# TOUJOURS faire ça :
git pull origin dev1
git push origin dev1

# Pourquoi ? Un collègue a peut-être pushé entre temps
```

#### Règle 5 : Communication avec l'équipe

Avant de travailler sur un fichier, prévenir l'équipe :

**Sur Discord/Slack :**
```
Beso : "Je travaille sur README.md section Installation"
Yewinthlaing04 : "OK, je prends la section Commandes de base"
Membre 3 : "Je fais la section Workflow"
Membre 4 : "Je m'occupe des Bonnes pratiques"
```

Cela évite que deux personnes modifient la même partie en même temps.

### Processus complet d'une fonctionnalité

#### Scénario : Ajouter une nouvelle section dans le README

```bash
# 1. Partir de dev1 à jour
git checkout dev1
git pull origin dev1

# 2. (Optionnel) Créer une branche feature
git checkout -b feature/ma-section
# Ou travailler directement sur dev1 si petit changement

# 3. Modifier le README
# Ajouter votre section

# 4. Commiter régulièrement
git add README.md
git commit -m "docs: début de ma section"
# ... continuer à travailler ...
git commit -m "docs: finalisation de ma section"

# 5. Pousser votre branche
git push origin feature/ma-section
# Ou si vous travaillez sur dev1 :
git push origin dev1

# 6. (Si branche feature) Créer une Pull Request sur GitHub
# Aller sur GitHub → Pull Requests → New Pull Request
# Source: feature/ma-section → Target: dev1

# 7. Demander une revue à vos collègues
# Assigner Beso, Membre 3, Membre 4 comme reviewers

# 8. Après approbation, merger dans dev1

# 9. Nettoyer la branche feature
git checkout dev1
git pull origin dev1
git branch -d feature/ma-section
```

### Quand merger dev1 dans main ?

**Uniquement quand :**
- Toutes les fonctionnalités sont terminées
- Tous les tests sont OK
- Le code a été revu par l'équipe
- On est prêt à déployer en production

**Processus :**
```bash
# 1. S'assurer que dev1 est stable
git checkout dev1
git pull origin dev1

# 2. Créer une Pull Request sur GitHub
# dev1 → main

# 3. Revue complète par le Lead (Beso)

# 4. Après validation, merger

# 5. Créer un tag de version
git checkout main
git pull origin main
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin --tags
```

### Schéma visuel du workflow

```
Temps ────────────────────────────────────────>

main:    o─────────────────────────M──────────> (production)
                                    │
                              (Merge quand stable)
                                    │
dev1:    o───┬───┬───┬───┬───┬─────┘──────────> (développement)
             │   │   │   │   │
             │   │   │   │   └─ Membre 4 push
             │   │   │   └───── Membre 3 push
             │   │   └────────── Yewinthlaing04 push
             │   └──────────────── Beso push
             └──────────────────── Tous pull
```

---

## Commandes essentielles {#commandes}

### Commandes de base

```bash
# Voir l'état actuel
git status

# Voir l'historique des commits
git log
git log --oneline
git log --oneline --graph --all

# Voir les différences
git diff                    # Changements non stagés
git diff --staged          # Changements stagés
git diff README.md         # Différences sur un fichier

# Ajouter des fichiers
git add fichier.txt
git add .                  # Tout ajouter

# Commiter
git commit -m "message"
git commit -am "message"   # Add + commit (fichiers déjà trackés)

# Pousser
git push origin dev1

# Récupérer
git pull origin dev1
git fetch origin           # Télécharge sans fusionner
```

### Gestion des branches

```bash
# Lister les branches
git branch                 # Branches locales
git branch -a             # Toutes les branches

# Créer une branche
git branch feature/nouvelle-fonctionnalite

# Changer de branche
git checkout dev1
git switch dev1           # Nouvelle syntaxe

# Créer et changer de branche
git checkout -b feature/ma-branche

# Supprimer une branche
git branch -d feature/ancienne-branche
git branch -D feature/ancienne-branche  # Forcer
```

### Annuler des modifications

```bash
# Annuler les modifications non commitées
git restore fichier.txt
git restore .              # Tout annuler

# Retirer du staging
git restore --staged fichier.txt

# Annuler le dernier commit (garder les modifications)
git reset --soft HEAD~1

# Annuler le dernier commit (supprimer les modifications)
git reset --hard HEAD~1
```

### Gérer les conflits

```bash
# Lors d'un pull, si conflit :
git pull origin dev1
# CONFLICT in README.md

# 1. Ouvrir le fichier, vous verrez :
<<<<<<< HEAD
Votre version
=======
Version distante
>>>>>>> origin/dev1

# 2. Éditer pour résoudre
# 3. Supprimer les marqueurs <<<< ==== >>>>
# 4. Sauvegarder

# 5. Marquer comme résolu
git add README.md
git commit -m "merge: résolution conflit"
git push origin dev1
```

### Outils pratiques

```bash
# Stash : mettre de côté temporairement
git stash                  # Sauvegarder
git stash list            # Voir les stash
git stash pop             # Récupérer

# Voir qui a modifié chaque ligne
git blame fichier.txt

# Chercher dans l'historique
git log --grep="mot-clé"
git log --author="Beso"
```

---

## Bonnes pratiques {#bonnes-pratiques}

### 1. Messages de commit clairs

**Format recommandé :**
```
type: description courte (max 50 caractères)
```

**Types :**
- `docs:` documentation
- `feat:` nouvelle fonctionnalité
- `fix:` correction de bug
- `refactor:` refactoring du code
- `test:` ajout de tests
- `style:` formatage

**Exemples :**
```bash
git commit -m "docs: ajout section installation"
git commit -m "feat: ajout du système d'authentification"
git commit -m "fix: correction bug de connexion"
git commit -m "refactor: simplification de la fonction login"
```

### 2. Commiter souvent

**Règle : Chaque fois que ça marche, commitez !**

```bash
# BON ✅
git commit -m "docs: ajout titre section"
git commit -m "docs: ajout contenu section"
git commit -m "docs: ajout exemples"

# MAUVAIS ❌
# ... travailler 4 heures ...
git commit -m "ajout de tout"
```

### 3. Pull avant de push

```bash
# TOUJOURS :
git pull origin dev1
git push origin dev1
```

### 4. Ne jamais commiter de fichiers sensibles

**Ne JAMAIS commiter :**
- Mots de passe
- Clés API
- Tokens
- Fichiers `.env`

**Utiliser .gitignore :**
```gitignore
# Fichier .gitignore à la racine

# Environnement
.env
.env.local

# Dépendances
node_modules/
vendor/

# IDE
.vscode/
.idea/

# Système
.DS_Store
Thumbs.db

# Logs
*.log
```

### 5. Communiquer avec l'équipe

Avant de travailler sur un fichier important, prévenir sur Discord/Slack.

### 6. Tester avant de push

```bash
# Vérifier que tout fonctionne
# Relire vos modifications
git diff

# Puis push
git push origin dev1
```

### 7. Faire des revues de code

Quand un collègue crée une Pull Request, prendre le temps de :
- Lire le code
- Tester localement si nécessaire
- Laisser des commentaires constructifs
- Approuver ou demander des modifications

---

## Résumé : Votre premier jour chez TechCorp

```bash
# 1. Installer Git
# Télécharger depuis git-scm.com

# 2. Configurer votre identité
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@techcorp.com"

# 3. Cloner le projet
git clone https://github.com/besogogoladze/Group2.git
cd Group2

# 4. Basculer sur dev1
git checkout dev1

# 5. Récupérer la dernière version
git pull origin dev1

# 6. Travailler
# Modifier des fichiers

# 7. Sauvegarder votre travail
git add .
git commit -m "docs: ma première contribution"

# 8. Envoyer votre travail
git pull origin dev1
git push origin dev1

# 9. Répéter les étapes 5-8 tout au long de la journée
```

**Bienvenue dans l'équipe TechCorp ! 🚀**

---

## Aide rapide

**Vous êtes perdu ?** Tapez ces commandes :
```bash
git status        # Où suis-je ? Qu'ai-je modifié ?
git branch        # Sur quelle branche suis-je ?
git log --oneline # Qu'est-ce qui a été fait récemment ?
```

**En cas de problème, contacter :**
- Beso (Lead Developer)
- Ou consulter la documentation Git officielle
