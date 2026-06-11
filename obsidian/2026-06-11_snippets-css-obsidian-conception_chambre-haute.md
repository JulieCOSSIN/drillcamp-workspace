---
type: tutoriel
role: retour d'expérience
tags:
  - obsidian
  - css
  - design
  - process
  - snippets
up: "[[MOC Claude]]"
related:
  - "[[MOC Claude]]"
  - "[[MOC Tech]]"
  - "[[Comment nous avons structuré nos notes Obsidian avec Claude]]"
---

# Comment j'ai habillé mes vaults Obsidian avec Claude

Il y a quelque chose de légèrement absurde à passer des heures à organiser ses connaissances dans un outil dont l'interface vous laisse froide. J'avais construit deux vaults — l'un opérationnel pour DrillCamp, l'autre personnel pour mes lectures et réflexions — et dans les deux j'avais déjà embarqué des fichiers HTML graphiquement travaillés. Des dashboards, des fiches interactives, des visualisations de stack. Ces HTML étaient beaux. L'interface Obsidian autour, elle, était générique.

Ce chantier a changé ça.

---

## Le contexte : deux vaults, deux univers, une dissonance

**Drillcamp Inc** est mon vault opérationnel. Il pilote une activité de conseil et d'incubation qui fonctionne avec la rigueur d'une unité militaire — systèmes, processus, exécution. Il avait besoin d'un habillage sombre et dense, à la hauteur de l'identité de marque DrillCamp.

**La Chambre Haute**, c'est ici — mon espace de connaissance personnel. Lectures, réflexions, développement, journal. L'endroit où je pense sans avoir à rendre des comptes. Il avait besoin d'un habillage clair et éditorial, chaleureux et propice à la concentration.

Dans les deux vaults, des fichiers HTML embarqués cohabitaient déjà avec les notes markdown. Ces HTML avaient leur propre registre visuel — construit sur la charte DrillCamp pour le vault pro, plus sobre pour le vault perso. Le problème : l'interface Obsidian native ne dialoguait pas avec eux. On passait d'un espace sans caractère à un contenu graphiquement riche, et l'expérience était dissonante.

L'objectif : **habiller l'interface elle-même** pour qu'elle soit cohérente avec les HTML, et préparer le terrain pour tous ceux qu'on créera dans le futur.

---

## Qu'est-ce qu'un snippet CSS Obsidian

Un snippet CSS est un fichier `.css` placé dans le dossier `.obsidian/snippets/` à la racine d'un vault. On l'active en un clic dans `Réglages > Apparence > CSS Snippets`. Une fois actif, il agit comme une couche de style supplémentaire sur l'interface d'Obsidian — il peut tout modifier : la couleur de fond, les titres, la sidebar, les blocs de code, l'encart de propriétés, les callouts.

Ce qu'il ne fait pas : il ne touche pas aux fichiers HTML embarqués via Custom Frames. Ces HTML vivent dans leur propre contexte (un iframe ou une frame dédiée) et ont leur propre système de style. Les deux couches sont indépendantes, mais elles doivent parler le même langage visuel.

---

## Le squelette et la chair

La distinction entre ces deux couches est fondamentale. La meilleure façon de la visualiser :

**Le snippet CSS est le squelette.** Il donne la structure osseuse de l'environnement — le registre visuel de l'interface elle-même. La couleur de fond, la typographie des notes, les pilules de la sidebar, l'atmosphère générale. Sans lui, tous les vaults Obsidian se ressemblent.

**L'embed HTML est la chair.** C'est le contenu riche, dense, interactif, qui vit à l'intérieur des notes. Il a sa propre masse, ses propres animations, ses propres gradients. Il est conçu indépendamment du snippet — mais il hérite de l'atmosphère que le snippet a posée.

Ce qui lie les deux : les conventions de design partagées. Mêmes couleurs de base, même registre de contraste, même famille typographique. Si le squelette est sombre et le muscle clair, l'organisme entier semble fragmenté. S'ils parlent le même langage, l'expérience est fluide et cohérente.

---

## Le CLAUDE.md : la mémoire partagée

Pour que cette cohérence tienne dans le temps — sur plusieurs sessions, avec Claude Code qui construit les HTML et Claude Chat qui conçoit l'architecture — il faut un document de référence commun.

C'est le rôle du `CLAUDE.md`, un fichier positionné à la racine du repo `drillcamp-workspace`. Claude Code le lit automatiquement à chaque démarrage de session. Claude Chat y accède via le projet.

Ce fichier contient les conventions HTML par vault : les tokens de couleur, la typographie, les effets visuels, les marges. Quand je demande à Claude Code de créer un nouveau HTML pour Drillcamp Inc, il sait d'emblée que le fond est `#101D1B`, que l'accent est `#B89A82`, que l'effet est liquid glass sombre. Aucun briefing supplémentaire nécessaire.

Sans `CLAUDE.md`, chaque HTML est produit dans le vide. Avec lui, la cohérence est garantie structurellement.

---

## Comment on a conçu les deux snippets

### Le snippet Drillcamp Inc — l'univers militaire-opérationnel

L'identité de DrillCamp a une dimension militaire assumée. "Drill" vient de l'anglais militaire — les exercices d'entraînement répétés jusqu'à l'automatisme. Le consulting DrillCamp s'adresse à des leaders qui veulent cette même rigueur dans leur organisation. L'interface Obsidian de ce vault devait incarner ça : **sombre, précis, dense**.

Les choix principaux :
- Fond `#101D1B` — vert très sombre, presque noir, professionnel sans être agressif
- Accent sable chaud `#B89A82` — plus doux que la terracotta d'origine, meilleur pour une interface de travail prolongé
- DM Sans pour tout — lisible, moderne, ancrage Apple-adjacent
- Effet liquid glass sombre sur l'encart Propriétés, les callouts, la sidebar
- Sidebar avec une couleur par entité du cabinet : mint pour The Drillcamp, or pour JC Productions, pêche pour les notes personnelles, lavande pour Voice Of Kings, bleu acier pour DrillSchool

### Le snippet La Chambre Haute — l'espace éditorial

Ce vault est un espace de connaissance personnel et intellectuel. L'ambiance voulue : un cabinet de lecture, un parchemin vivant. Chaleureux, aéré, propice à la lecture longue.

Les choix principaux :
- Fond `#D4CDB8` — parchemin vieilli, plus chaleureux que le blanc, moins fatigant à la longue
- Accent teal `#4A8B8C` — sérénité, ancrage
- Playfair Display pour les H1 — serif élégant, impact éditorial fort
- DM Sans pour le corps et les H2/H3 — transition douce vers la lecture
- Effet liquid glass clair sur l'encart et les callouts
- La sidebar uniformément sombre `#32302b`, avec les deux notes racines (Tour de Contrôle, GUIDE) en teal pour les distinguer

---

## Les modes visuels : cssclasses dans Obsidian

### Comment ça marche

`cssclasses` est un champ frontmatter standard qu'Obsidian transforme en classe CSS sur la note. Le snippet peut ensuite cibler cette classe pour appliquer des styles spécifiques à cette note uniquement, sans toucher aux autres.

Exemple d'usage dans le frontmatter d'une note :
```yaml
cssclasses: mode-matrix
```

Les modes sont actifs en **mode Lecture uniquement** (raccourci Ctrl+E). En mode édition, l'interface reste dans son état standard.

### Les trois modes du vault Drillcamp Inc

La charte graphique DrillCamp définit quatre registres visuels : l'Épuré Apple (état par défaut du snippet), Matrix/Glitch, NASA/Astronaute, Gospel Hip-Hop. Les trois derniers sont activables par note via `cssclasses`.

**`mode-matrix`** — fond quasi-noir `#050A09`, textes en vert émeraude, typographie monospace. L'ambiance : terminal de commande, exécution technique pure. Pour les notes de processus, de stack, de documentation système.

**`mode-nasa`** — fond bleu nuit `#080D15`, titres en bleu acier avec lettres espacées et majuscules. L'ambiance : salle de contrôle mission. Pour les notes stratégiques, OKRs, feuilles de route à long terme.

**`mode-gospel`** — fond vert très profond `#0D1612`, titres en or italique. L'ambiance : conviction, énergie, culture. Pour les notes de manifeste, de vision, de personal brand.

### Pourquoi ces modes spécifiquement

Ces modes ne sont pas esthétiques au sens décoratif. Ils encodent des **états d'esprit** liés à l'identité de DrillCamp. La rigueur militaire se retrouve dans Matrix (exécution) et NASA (planification stratégique). La conviction culturelle se retrouve dans Gospel. Coder visuellement l'état d'esprit d'une note permet de retrouver instantanément les bonnes notes selon le mode de travail du moment — et rappelle à chaque ouverture dans quel registre cette note a été pensée.

---

## Ce qu'on a appris en faisant — les corrections itératives

Le snippet Drillcamp Inc est passé par huit versions. Chaque version a résolu un problème réel observé dans l'interface.

### La désynchronisation rem/slider Obsidian

Le premier problème inattendu : à 20% de taille de police dans les réglages Obsidian, le body text affiché mesure environ 12px — mais `1rem` CSS reste à 16px (base navigateur, indépendant du slider). Cette désynchronisation rendait toutes les valeurs en `rem` approximatives.

La solution : choisir une valeur de référence absolue et calibrer toute la hiérarchie à partir d'elle. L'encart Propriétés, visuellement stable et facile à mesurer, est devenu la référence à `0.82rem`. Tous les autres éléments ont été ajustés proportionnellement.

### L'alignement entre l'encart et l'embed HTML

Un problème d'alignement subtil : l'encart Propriétés s'affichait légèrement décalé par rapport au bloc Custom Frames dans la même note. L'embed avait naturellement un décalage de 12px depuis le bord de la colonne — hérité du style par défaut des blocs de code Obsidian. Correction : `margin-left: 12px` sur l'encart pour l'aligner exactement.

### Rapprocher les zones des sidebars

L'encart et l'embed occupaient trop peu de la largeur disponible — des marges intérieures d'environ 50px de chaque côté créaient une sensation de resserrement. On a utilisé des **marges négatives** pour faire "déborder" ces deux éléments au-delà des limites de la colonne de contenu, sans affecter le corps de texte.

Pour l'embed spécifiquement, la marge négative seule ne suffisait pas — son comportement `width: 100%` implicite l'empêchait de s'étendre à droite. Solution mathématique : `width: calc(100% + 3cm - 12px)`, dérivé des deux extensions latérales avec compensation de l'offset de 12px.

### Le syntax highlighting en Chambre Haute

Dans le vault clair, les mots-clés des blocs de code (`cd`, `git`) apparaissaient en jaune-orangé — un héritage du syntax highlighting par défaut d'Obsidian, illisible sur le fond beige. Deux systèmes coexistent dans Obsidian : Prism.js (`.token.*`) en mode lecture, CodeMirror (`.cm-keyword`, `.cm-builtin`) en mode édition. Les deux ont été ciblés et remplacés par le teal profond `#1A5C5D`, parent de l'accent `#4A8B8C` mais suffisamment sombre pour contraster correctement.

---

## État final

| Vault | Snippet | Version finale |
|---|---|---|
| Drillcamp Inc | `drillcamp-inc.css` | v1.8 |
| La Chambre Haute | `chambre-haute.css` | v1.5 |

Les deux fichiers sont dans `obsidian/snippets/` du repo `JulieCOSSIN/drillcamp-workspace`. Installation locale : glisser dans `.obsidian/snippets/` du vault concerné, puis activer dans `Réglages > Apparence > CSS Snippets`.

---

> Dans dossier : [[MOC Claude]]
> Dans [[MOC Connaissances]]
