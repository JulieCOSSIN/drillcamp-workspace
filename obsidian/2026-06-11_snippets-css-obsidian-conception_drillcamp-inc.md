---
type: tutoriel
role: retour d'expérience et documentation système
maison_mere: "[[THE DRILLCAMP]]"
tags:
  - obsidian
  - css
  - design
  - process
  - snippets
up: "[[MOC CLAUDE]]"
Dans: "[[MOC CLAUDE]]"
related:
  - "[[MOC CLAUDE]]"
  - "[[COCKPIT]]"
  - "[[Stack IA Contenu Audiovisuel]]"
---

# Concevoir les snippets CSS des vaults Obsidian

## Pourquoi ce chantier

L'environnement de travail DrillCamp repose sur deux vaults Obsidian distincts : **Drillcamp Inc** (opérationnel, sombre) et **La Chambre Haute** (personnel, clair). Dans les deux vaults, des fichiers HTML riches sont déjà embarqués via le plugin Custom Frames — dashboards, stacks techniques, fiches de référence interactives. Ces embeds ont leur propre univers visuel, construit sur la charte DrillCamp.

Problème : l'interface native d'Obsidian, elle, n'avait pas suivi. Fond par défaut, typographie générique, sidebar sans identité. Le résultat : une dissonance entre l'interface Obsidian et les HTML embarqués. On entrait dans une note et on passait d'un environnement austère à un rendu graphique travaillé. Ce n'est pas acceptable pour un système de travail qui se veut cohérent.

L'objectif de ce chantier : **habiller l'interface Obsidian elle-même** pour qu'elle soit visuellement harmonieuse avec les embeds HTML existants et préparer le terrain pour tous les futurs embeds.

Ce chantier s'inscrit dans un processus en trois phases :
1. Snippets CSS (interface Obsidian) - terminé
2. `CLAUDE.md` (conventions partagées entre Claude Chat et Claude Code) - en cours
3. Mise à jour et création des embeds HTML avec les tokens par vault

---

## Qu'est-ce qu'un snippet CSS Obsidian

Un **snippet CSS** est un fichier `.css` déposé dans le dossier `.obsidian/snippets/` à la racine d'un vault. Il s'active via `Réglages > Apparence > CSS Snippets` et agit comme une surcouche de style sur l'interface d'Obsidian.

Concrètement, un snippet peut cibler et modifier :
- La couleur de fond des notes et de l'interface
- La typographie (famille, taille, graisse, interligne)
- La sidebar gauche et ses dossiers
- L'encart Propriétés/Frontmatter
- Les blocs de code
- Les callouts
- Le panneau Paramètres
- Les tags
- Les scrollbars

Ce que le snippet **ne touche pas** : les fichiers HTML embarqués via Custom Frames. Ces HTML ont leur propre système de style (variables CSS dans un bloc `:root` à l'intérieur du fichier). Les deux couches sont **techniquement indépendantes** — mais doivent être visuellement harmonisées.

---

## Snippet vs embed HTML : le squelette et la chair

La meilleure métaphore pour comprendre la relation entre les deux couches :

**Le snippet CSS = le squelette.** Il donne la structure, l'atmosphère, le registre visuel de l'environnement Obsidian lui-même. C'est lui qui décide que le fond est sombre et que la sidebar a des pilules colorées par entité. Sans lui, Obsidian ressemble à une application générique.

**L'embed HTML = la chair.** C'est le contenu riche, interactif, personnalisé qui vit à l'intérieur des notes. Dashboards, cartes de stack, tableaux de bord financiers. Ces HTML ont leur propre masse visuelle — animations, gradients, liquid glass, typographie branded.

Le danger : si les deux couches ne dialoguent pas, on obtient un jardin bien entretenu avec une clôture en parpaing. L'harmonie visuelle nécessite que le squelette et la chair parlent le même langage de couleur, de typographie et de registre de contraste.

---

## Le CLAUDE.md : le ciment entre les deux couches

Le fichier `CLAUDE.md`, positionné à la racine du repo `JulieCOSSIN/drillcamp-workspace`, est le document de référence commun lu automatiquement par **Claude Code** à chaque ouverture de session, et consultable par **Claude Chat** via le projet.

Son rôle pour ce chantier : documenter les conventions HTML de chaque vault — les tokens de couleur, la typographie, les effets liquid glass, les marges — pour que tout nouveau HTML produit dans le futur hérite automatiquement des bons paramètres sans configuration manuelle.

Sans `CLAUDE.md` : chaque nouveau HTML est produit dans le vide, et il faut re-briefer Claude à chaque fois.

Avec `CLAUDE.md` : Claude Code lit les conventions au démarrage, sait que Drillcamp Inc utilise `#101D1B` comme fond et `#B89A82` comme accent, et produit des HTML conformes sans instruction supplémentaire.

---

## Tutoriel — Le snippet Drillcamp Inc

### Identité visuelle cible

Le vault Drillcamp Inc est un espace **opérationnel**. Il incarne l'ADN de DrillCamp : une organisation de conseil et d'accompagnement qui fonctionne avec la rigueur et la discipline d'une unité militaire. Le mot "Drill" vient de l'anglais militaire — les exercices d'entraînement répétés jusqu'à la maîtrise parfaite. DrillCamp s'adresse à des leaders qui pensent comme des généraux : vision stratégique, exécution sans faille, systèmes plutôt qu'improvisation.

L'interface Obsidian de ce vault devait refléter cet univers : **sombre, dense, précis**. Pas d'ornement superflu. Chaque élément a une fonction.

Tokens retenus :
- Fond : `#101D1B` (vert très sombre, quasi-noir)
- Accent : `#B89A82` (sable chaud — nuance plus douce que la terracotta originale)
- Ardoise : `#739297`
- Typographie : DM Sans (Apple-adjacent, lisible, moderne sans être froid)
- Effet liquid glass dark : `rgba(20,31,29,0.82)` + `blur(18px)`

### La sidebar par entité

L'une des décisions les plus structurantes du snippet : **chaque dossier d'entité a sa propre couleur de pilule dans la sidebar**. On identifie immédiatement dans quel univers on se trouve.

| Entité | Couleur texte |
|---|---|
| Le Cockpit / PROCESS | Blanc atténué |
| The Drillcamp | Mint `#94d8b6` |
| JC Productions | Or `#d8d694` |
| Les Yeux de Julie | Pêche `#e8c4a4` |
| Voice Of Kings | Lavande `#c4b4e8` |
| DrillSchool | Bleu acier `#94c4e8` |
| Find Your Church | Mint `#94d8b6` |
| Claude | Gradient terracotta DrillCamp |

### L'encart Propriétés en liquid glass

L'encart Propriétés/Frontmatter (`.metadata-container`) reçoit l'effet liquid glass sombre : fond `rgba(20,31,29,0.82)`, bordure subtile, double inset shadow pour simuler la profondeur. La typographie de l'encart est calibrée à `0.82rem`, qui sert de référence pour toute la hiérarchie de tailles.

### Les blocs de code

Fond `rgba(28,36,44,0.55)` avec `blur(8px)` — un effet glass subtil qui évoque l'interface de la barre de conversation Claude. Le code inline hérite de la couleur accent `rgba(184,154,130,0.90)`.

### Le panneau Paramètres

Traité en liquid glass sombre avec gradient `145deg` pour donner de la profondeur. La taille de police est ancrée à `0.875rem` pour rester lisible indépendamment du slider de taille dans les réglages Obsidian.

---

## Tutoriel — Le snippet La Chambre Haute

### Identité visuelle cible

La Chambre Haute est un espace **intellectuel et personnel** — journal de connaissances, réflexions, fiches de lecture, développement personnel. L'ambiance voulue : un cabinet de lecture éclairé, un parchemin vivant. Calme, aéré, lisible.

Tokens retenus :
- Fond : `#D4CDB8` (parchemin vieilli, plus riche que le blanc)
- Accent : `#4A8B8C` (teal — sérénité et ancrage)
- Typographie : Playfair Display pour H1 (impact éditorial), DM Sans pour le corps
- Effet liquid glass light : `rgba(212,205,184,0.65)` + `blur(14px)`

Le fond `#D4CDB8` a été choisi au lieu du blanc pur pour éviter la fatigue visuelle et donner une chaleur organique à l'espace.

### Les titres

- **H1** : Playfair Display 700 — serif élégant, ancrage éditorial fort
- **H2** : DM Sans 700 — transition vers le corps de texte, structure claire
- **H3** : DM Sans 700, `#32302b`, sans majuscule
- La sidebar et les deux notes racines (Tour de Contrôle, GUIDE) gardent leur couleur teal pour se distinguer

---

## Chapitre spécial — cssclasses et les modes visuels

### Ce qu'est un cssclass dans Obsidian

`cssclasses` est un champ frontmatter standard d'Obsidian. Quand une valeur est déclarée dans ce champ, Obsidian ajoute cette valeur comme classe CSS sur l'élément parent de la note. Le snippet peut alors cibler cette classe pour appliquer des styles spécifiques à cette note uniquement.

Usage dans le frontmatter :
```yaml
cssclasses: mode-matrix
```

Les modes sont actifs **en mode Lecture uniquement** (Ctrl+E). En mode édition, l'interface reste dans son état standard.

### Les trois modes du vault Drillcamp Inc

Le snippet Drillcamp Inc implémente trois modes visuels, directement tirés de la charte graphique DrillCamp. L'identité de marque DrillCamp repose sur quatre registres visuels distincts — l'Épuré Apple (état par défaut du snippet), Matrix/Glitch, NASA/Astronaute et Gospel Hip-Hop. Les trois derniers sont activables via `cssclasses`.

**Mode Matrix/Glitch — `mode-matrix`**
Fond `#050A09`, textes et titres en vert émeraude `#5DCAA5`, typographie monospace. Ce mode évoque l'exécution pure, la technique, le code. Il est approprié pour les notes de processus technique, les stacks, les documentations système. L'ambiance : terminal de commande, surveillance en temps réel.

**Mode NASA/Astronaute — `mode-nasa`**
Fond `#080D15`, titres en bleu acier `#5B8FA8` avec espacement de lettres et majuscules. Ce mode évoque la planification stratégique à grande échelle, la précision de mission. Approprié pour les notes de stratégie, OKRs, feuilles de route. L'ambiance : salle de contrôle mission.

**Mode Gospel Hip-Hop — `mode-gospel`**
Fond `#0D1612`, titres en or `#D4A853` en italique. Ce mode évoque l'énergie, la conviction, la culture. Approprié pour les notes de manifeste, de vision, de personal brand. L'ambiance : studio d'enregistrement, scène.

### Pourquoi ces modes

Ces trois modes ne sont pas arbitraires. Ils sont ancrés dans la charte graphique DrillCamp, qui définit quatre registres visuels pour l'ensemble de l'écosystème de marque. DrillCamp incarne la rencontre de la rigueur militaire (Matrix, NASA) et de la conviction culturelle (Gospel). Avoir ces modes dans le vault permet de coder visuellement l'état d'esprit d'une note au moment de sa rédaction, et de retrouver rapidement les bonnes notes selon leur registre lors d'une session de travail intensive.

---

## Les corrections itératives — ce qu'on a appris

Le snippet Drillcamp Inc a traversé huit versions avant d'être considéré complet. Chaque version a apporté une correction précise à un problème identifié en contexte réel.

### Calibration typographique

La découverte centrale de ce chantier : à 20% de taille de police dans les réglages Obsidian, le body text rendu mesure environ 12px — mais `1rem` CSS reste anché à 16px (base navigateur, indépendant du slider). Cette désynchronisation entre le slider Obsidian et les valeurs rem CSS a causé des décalages de taille apparente entre le corps de texte et l'encart.

Solution : calibrer toute la hiérarchie sur `0.82rem` comme valeur de référence (taille de l'encart Propriétés), puis ajuster proportionnellement les autres éléments à partir de cette ancre.

| Élément | Taille retenue |
|---|---|
| Encart Propriétés | `0.82rem` (référence) |
| Corps de texte (lecture) | `0.82rem` |
| Sidebar / Outline | `0.78rem` |
| Tags | `0.78rem` |
| Inline-title | `1.5rem` ancré (évite l'écrasement à 20%) |
| Paramètres modal | `0.875rem` |

### Alignement encart et embed HTML

Problème identifié : l'encart Propriétés s'affichait décalé par rapport au bloc Custom Frames de l'embed HTML dans la même note. L'embed avait un décalage naturel de 12px depuis le bord de la colonne de contenu — décalage hérité du style par défaut des blocs de code Obsidian.

Correction : `margin-left: 12px !important` sur `.metadata-container`, alignant l'encart exactement sur le bord gauche de l'embed.

### Réduction des marges horizontales

L'encart et l'embed HTML occupaient trop peu de la largeur disponible dans la zone de contenu — marges intérieures d'environ 50px de chaque côté. La demande : rapprocher ces deux zones des sidebars gauche et droite.

Technique utilisée : **marges négatives** sur les deux éléments — `calc(12px - 1.5cm)` à gauche et `-1.5cm` à droite. Les marges négatives font "déborder" l'élément au-delà de la colonne de contenu sans affecter le corps de texte environnant.

Correction supplémentaire pour l'embed : l'embed avait un comportement `width: 100%` implicite qui l'empêchait de s'étendre à droite malgré la marge négative. Solution : `width: calc(100% + 3cm - 12px)` — valeur dérivée mathématiquement des deux extensions (1.5cm × 2) avec compensation de l'offset de 12px.

### Restauration du liquid glass sur l'encart

Lors d'une refactorisation intermédiaire, l'effet liquid glass du `.metadata-container` avait disparu (le bloc CSS avait été écrasé). Restauration complète avec le système de variables CSS (`--lg-dark-bg`, `--lg-dark-blur`, `--lg-dark-border`, `--lg-dark-shine`, `--lg-dark-floor`).

### Mode lecture vs mode édition

Certaines règles CSS ne s'appliquent qu'en mode lecture et nécessitent un ciblage spécifique. La règle `margin-bottom: 3rem` sur l'encart ne fonctionnait qu'en édition sans le combinaison `.markdown-preview-view .metadata-container` + `!important`. Le ciblage double (sélecteur général + sélecteur mode lecture) garantit l'application dans les deux contextes.

---

## État final des deux snippets

| Fichier | Version | Chemin repo |
|---|---|---|
| `drillcamp-inc.css` | v1.8 | `obsidian/snippets/drillcamp-inc.css` |
| `chambre-haute.css` | v1.5 | `obsidian/snippets/chambre-haute.css` |

Installation : `.obsidian/snippets/` dans chaque vault, activation via `Réglages > Apparence > CSS Snippets`.

---

> Tour de contrôle : [[COCKPIT]]
> Entités servies : [[THE DRILLCAMP]] · [[JC PRODUCTIONS]] · [[PERSONAL BRAND]]
