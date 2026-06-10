---
type: tutoriel
role: documentation process - connexion Claude à GitHub
maison_mere: "[[THE DRILLCAMP]]"
tags:
  - claude
  - github
  - process
  - outils
up: "[[COCKPIT]]"
Dans: "[[PROCESS]]"
related:
  - "[[MOC CLAUDE]]"
  - "[[DrillCamp OS]]"
  - "[[THE DRILLCAMP]]"
---

# Connexion Claude - GitHub

> Comment connecter Claude à un repo GitHub, à quoi ça sert concrètement, et comment s'en servir au quotidien dans le contexte DrillCamp.

---

## Pourquoi cette connexion

Claude ne retient rien entre les conversations. Chaque session repart de zéro sauf ce qui est injecté en contexte — via la mémoire projet, les fichiers attachés, ou le contenu synchronisé.

GitHub résout un problème concret : avoir un espace partagé et permanent où poser des prompts longs, récupérer des livrables (notes, documents, fichiers), et construire une bibliothèque de ressources accessibles depuis n'importe quelle conversation Claude.

---

## Ce que fait concrètement le connecteur GitHub

Le connecteur est activé dans Personnaliser > Connecteurs dans Claude.

Il donne trois capacités :

**Chat** : attacher un fichier directement depuis un repo GitHub dans une conversation, via l'icône trombone. Pas besoin de télécharger et ré-uploader.

**Projects** : synchroniser un repo dans un Projet Claude. Le contenu devient contexte permanent — Claude a accès aux fichiers sans qu'il soit besoin de les attacher à chaque session.

**Claude Code** : navigation de branches, suivi de pull requests, sessions de travail distantes. Usage avancé, pas le sujet principal ici.

---

## La structure du repo drillcamp-workspace

Un seul repo regroupe trois dossiers fonctionnels :

```
drillcamp-workspace/
├── prompts/      ← prompts longs en .md, stockés pour réutilisation
├── obsidian/     ← notes Obsidian produites par Claude, à importer dans le vault
└── Documents/    ← fichiers et documents divers générés ou partagés
```

Repo : [github.com/JulieCOSSIN/drillcamp-workspace](https://github.com/JulieCOSSIN/drillcamp-workspace)

---

## Comment s'en servir au quotidien

### Déposer un prompt long

Quand un prompt dépasse ce qu'il est raisonnable de retaper ou de copier-coller à chaque fois, on le stocke dans `prompts/`.

Convention de nommage :
```
YYYY-MM-DD_sujet-en-minuscules.md
```
Exemple : `2026-06-10_frontend-drillcamp-os.md`

Dans la conversation Claude, on dit simplement : "Va chercher le prompt `prompts/nom-du-fichier.md`" et Claude le lit via le connecteur.

### Récupérer une note Obsidian produite par Claude

En fin de session, Claude peut écrire directement dans `obsidian/`. Le fichier est déposé avec le bon nom. On va ensuite le récupérer depuis GitHub et le glisser dans le bon dossier du vault.

Ce n'est pas un sync automatique vault-GitHub. C'est un espace de transit : Claude produit, GitHub stocke, on importe dans Obsidian quand c'est utile.

### Récupérer un document ou fichier

Même logique dans `Documents/`. Claude y dépose les livrables (HTML, MD, JSON, autre) en fin de session quand la livraison doit persister hors conversation.

---

## GitHub Desktop — le repo dans l'explorateur Windows

GitHub Desktop est l'application officielle de GitHub. Elle crée un dossier local sur le disque, synchronisé avec le repo distant. Le dossier apparaît dans l'explorateur Windows comme n'importe quel autre dossier.

Téléchargement : desktop.github.com (fichier `GitHubDesktopSetup-x64.exe`, gratuit, version 3.5.x).

### Installation et premier clone

1. Installe GitHub Desktop et connecte le compte `JulieCOSSIN`
2. **File → Clone repository** → sélectionne `drillcamp-workspace`
3. Choisis l'emplacement local (ex. `Documents/GitHub/drillcamp-workspace`)
4. Le dossier apparaît immédiatement dans l'explorateur Windows

### Récupérer ce que Claude pousse

Quand Claude dépose un fichier dans le repo depuis une conversation, il n'arrive pas automatiquement sur le disque. Il faut faire un **Pull** :

Dans GitHub Desktop → bouton **Fetch origin** en haut (vérifie s'il y a du nouveau) → puis **Pull origin** si des fichiers sont disponibles.

Le fichier apparaît alors dans le dossier local. On le glisse dans le vault Obsidian depuis l'explorateur Windows.

### Le flux complet avec GitHub Desktop

```
Claude pousse dans obsidian/
    ↓
GitHub Desktop → Fetch origin → Pull
    ↓
Dossier local drillcamp-workspace/obsidian/
    ↓
Glisser la note dans le bon dossier du vault Obsidian
```

---

## Pourquoi ce n'est pas un remplacement du vault

Le repo GitHub n'est pas le vault. Il ne remplace pas Obsidian, il le complète.

| GitHub drillcamp-workspace | Vault Drillcamp Inc |
|---|---|
| Transit et stockage de livrables Claude | PKM vivant, graphe de connaissances |
| Accessible depuis Claude directement | Accessible depuis Obsidian |
| Fichiers bruts, nommage daté | Notes wikilinquées, frontmatter complet |
| Pas de graphe ni de navigation | Navigation par wikilinks et MOC |

Le flux normal : Claude produit dans le repo -> on importe dans le vault quand la note est définitive et mérite d'être intégrée au graphe.

---

## Ce qui reste à faire

- [x] Installer GitHub Desktop et cloner drillcamp-workspace
- [ ] Tester l'attachement d'un fichier depuis GitHub via l'icône trombone dans une conversation
- [ ] Tester la synchronisation du repo dans les settings du Projet Claude
- [ ] Valider la convention de nommage sur la durée

---

> Tour de contrôle : [[COCKPIT]]
> Méthode de travail : [[MOC CLAUDE]]
> Voir aussi : [[DrillCamp OS]] - [[Rôles Claude - Attribution DrillCamp]]
