CONTEXTE — Session Obsidian CSS + Conventions HTML (10 juin 2026)

SUJET DE LA SESSION
Amélioration de l'esthétique des notes Obsidian. Alternatives à Custom Frames
pour la mise en valeur visuelle. Conventions HTML par vault. Git Bash. Clarification
des deux couches de styling. Où ancrer les conventions pour qu'elles soient lues
par Claude, Claude Design, Claude Code et VS Code.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ALTERNATIVES À CUSTOM FRAMES
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Custom Frames reste pertinent pour les outils interactifs (DC Finance, Dashboard OS).
   Pour la mise en forme visuelle des notes standard, les alternatives plus légères sont :
- CSS Snippets : fichiers .css dans .obsidian/snippets/ de chaque vault.
  Activés via Réglages > Apparence > CSS Snippets. Token cssclasses en frontmatter
  pour appliquer des styles par note.
- Callouts retravaillés : blocs [!type] stylisables via snippets. Permet des
  encadrés custom (vision, decision, kpi, next, ressource) sans HTML.
- Thème de base : un thème communautaire (Minimal, AnuPpuccin) comme fondation
  avant d'ajouter les snippets.
- iframe native : <iframe> dans une note Obsidian avec Trusted frames activé.
  Même résultat que Custom Frames, sans plugin.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
2. LES DEUX COUCHES DE STYLING — DISTINCTION CRITIQUE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Ces deux systèmes sont étanches l'un à l'autre. Ils ne se parlent pas.

COUCHE 1 — CSS Snippets (.obsidian/snippets/)
  Cible : l'interface Obsidian elle-même.
  Ce qu'ils changent : fond de l'éditeur, titres H1/H2/H3, callouts,
  sidebar, typographie des notes markdown.
  Activé par : toggle dans Réglages > Apparence > CSS Snippets.
  Usage : toutes les notes markdown du vault.

COUCHE 2 — Convention HTML CONFIG (en haut de chaque fichier .html)
  Cible : les fichiers HTML embarqués via Custom Frames ou iframe.
  Ce qu'ils changent : tout le rendu du HTML interactif (DC Finance,
  Stack IA, Dashboard, etc.).
  Activé par : simplement en ouvrant le fichier HTML dans la note.
  Usage : uniquement les outils HTML interactifs.

Pour des vaults cohérents de bout en bout, les deux couches sont
nécessaires et complémentaires.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
3. DOSSIERS SNIPPETS CRÉÉS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Julie a créé .obsidian/snippets/ dans les deux vaults :
  Drillcamp Inc/.obsidian/snippets/    ← prêt, vide
  La Chambre Haute/.obsidian/snippets/ ← prêt, vide

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
4. REPO GITHUB — STRUCTURE ET GIT BASH
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Repo : github.com/JulieCOSSIN/drillcamp-workspace
Structure :
  prompts/    ← prompts longs .md pour réutilisation
  obsidian/   ← notes produites par Claude, à importer dans le vault
  Documents/  ← livrables divers

Commandes Git Bash pour commit + push :
  cd Documents/GitHub/drillcamp-workspace
  git add .
  git commit -m "description du commit"
  git push
  git status  ← pour voir ce que Git a détecté avant de commiter

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
5. ANALYSE VISUELLE DES DEUX VAULTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Drillcamp Inc (thème sombre opérationnel) :
  Fond #101D1B, texte blanc, accents terracotta et vert par entité.
  Sidebar avec pills colorés par dossier/entité.
  Blocs de code sombres, syntaxe orange.
  Dense, informationnel, cohérent avec la charte DrillCamp.

La Chambre Haute (thème liseuse clair) :
  Fond blanc/crème (#F7F4EF), texte quasi-noir.
  Accents teal dans la barre de titre et les liens.
  Blocs de code gris clair, spacieux.
  Aéré, éditorial, personnel — opposé volontaire à Drillcamp Inc.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
6. CONVENTIONS HTML CONFIG PAR VAULT (COUCHE 2)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Section CONFIG en haut de chaque fichier HTML — seule section à
modifier pour adapter le contenu. Même principe que la Stack IA.

Drillcamp Inc :
  --bg: #101D1B / --accent: #AF5A3F / --muted: #739297
  --font-display: Plus Jakarta Sans / --font-data: Inter
  Cartes glass sombres, mode apple par défaut.

La Chambre Haute :
  --bg: #F7F4EF / --accent: #4A8B8C / --muted: #7A8A8A
  --font-display: Lora (serif éditorial) / --font-data: Inter
  Cartes blanches cassées, mode liseuse.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
7. CSS SNIPPETS À GÉNÉRER (COUCHE 1) — PROCHAINE ÉTAPE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Non encore générés. À produire dans la prochaine session.

Drillcamp Inc — snippet à créer :
  Fichier : drillcamp-inc.css dans .obsidian/snippets/
  Cibles : fond éditeur #101D1B, titres en Plus Jakarta Sans,
  callouts custom (vision, kpi, decision, next),
  cssclasses par mode visuel.

La Chambre Haute — snippet à créer :
  Fichier : chambre-haute.css dans .obsidian/snippets/
  Cibles : fond crème #F7F4EF, titres en Lora,
  callouts éditoriaux (insight, ressource, citation, next),
  espacement généreux, lecture fluide.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
8. OÙ ANCRER LES CONVENTIONS — LES 4 CONTEXTES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Chaque outil Claude lit les conventions depuis un endroit différent.
Il faut une seule source de vérité dupliquée aux bons endroits.

CLAUDE (conversation / projet)
  Lit : les fichiers en mémoire projet.
  Où mettre la convention : uploader une version synthétique
  dans le projet Claude. Déjà en place pour drillcamp-brandbook.
  À ajouter : convention HTML par vault en mémoire projet.

CLAUDE DESIGN (Visualizer)
  Lit : le skill drillcamp-brandbook via read_me avant chaque génération.
  Où mettre la convention : dans SKILL.md du skill drillcamp-brandbook,
  dans une section dédiée "HTML par vault".

CLAUDE CODE + VS CODE (extension Claude)
  Lit : automatiquement le fichier CLAUDE.md à la racine du repo
  à chaque session. Si absent, repart de zéro à chaque fois.
  Où mettre la convention : créer CLAUDE.md à la racine de
  drillcamp-workspace avec les tokens et conventions des deux vaults.

STRUCTURE CIBLE :
  drillcamp-workspace/
  └── CLAUDE.md                     ← à créer (Claude Code + VS Code)

  /mnt/skills/user/drillcamp-brandbook/
  └── SKILL.md                      ← à mettre à jour (Claude Design + Claude chat)

  Projet Claude (mémoire projet)
  └── convention HTML vault          ← à uploader (Claude chat)

PLAN D'EXÉCUTION (3 étapes) :

1. Créer CLAUDE.md à la racine du repo drillcamp-workspace
2. Ajouter une section "HTML par vault" dans drillcamp-brandbook SKILL.md
3. Uploader la convention synthétique en mémoire projet

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PROCHAINES ÉTAPES (à prioriser par Julie)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Créer CLAUDE.md à la racine du repo drillcamp-workspace

Mettre à jour drillcamp-brandbook SKILL.md (section HTML par vault)

Uploader la convention en mémoire projet

Générer drillcamp-inc.css (snippet Couche 1)

Générer chambre-haute.css (snippet Couche 1)

Choisir un thème de base compatible pour chaque vault

Tester un HTML La Chambre Haute en mode liseuse (Couche 2)

Valider les callouts custom dans les deux vaults



--------- 

avant de créer le claude.md , pose toi des questions afin de personnaliser les 2 conventions car je veux personnaliser encore les conventions
