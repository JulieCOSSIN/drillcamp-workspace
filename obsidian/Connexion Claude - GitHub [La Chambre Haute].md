---
type: tutoriel
role: retour d'expérience - connexion Claude à GitHub
tags:
  - claude
  - github
  - outils
  - process
up: "[[MOC Claude]]"
related:
  - "[[MOC Tech]]"
  - "[[Rôles Claude - définition et suggestion]]"
---

# Connexion Claude - GitHub

> Comment connecter Claude à un repo GitHub, à quoi ça sert concrètement, et comment s'en servir au quotidien.

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
Exemple : `2026-06-10_reflexion-leadership.md`

Dans la conversation Claude, on dit simplement : "Va chercher le prompt `prompts/nom-du-fichier.md`" et Claude le lit via le connecteur.

### Récupérer une note Obsidian produite par Claude

En fin de session, Claude peut écrire directement dans `obsidian/`. Le fichier est déposé avec le bon nom. On va ensuite le récupérer depuis GitHub et le glisser dans le bon dossier du vault.

Ce n'est pas un sync automatique vault-GitHub. C'est un espace de transit : Claude produit, GitHub stocke, on importe dans Obsidian quand c'est utile.

### Récupérer un document ou fichier

Même logique dans `Documents/`. Claude y dépose les livrables (HTML, MD, JSON, autre) en fin de session quand la livraison doit persister hors conversation.

---

## Pourquoi ce n'est pas un remplacement du vault

Le repo GitHub n'est pas le vault. Il ne remplace pas Obsidian, il le complète.

| GitHub drillcamp-workspace | Vault La Chambre Haute |
|---|---|
| Transit et stockage de livrables Claude | PKM vivant, graphe de connaissances |
| Accessible depuis Claude directement | Accessible depuis Obsidian |
| Fichiers bruts, nommage daté | Notes wikilinquées, frontmatter complet |
| Pas de graphe ni de navigation | Navigation par wikilinks et MOC |

Le flux normal : Claude produit dans le repo -> on importe dans le vault quand la note est définitive et mérite d'être intégrée au graphe.

---

## Ce qui reste à faire

- [ ] Tester l'attachement d'un fichier depuis GitHub via l'icône trombone dans une conversation
- [ ] Tester la synchronisation du repo dans les settings du Projet Claude
- [ ] Valider la convention de nommage sur la durée

---

> Document parent : [[MOC Claude]]
> Dans dossier : [[MOC Tech]] - Dans [[MOC Connaissances]]
> Voir aussi : [[Rôles Claude - définition et suggestion]] - [[Comment nous avons conçu le DrillCamp OS]]
