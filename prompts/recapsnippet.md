**RÉCAPITULATIF — Session CSS Snippets Obsidian (10 juin 2026)**

**Contexte.** Session dédiée à la création des CSS snippets Obsidian (couche 1 : interface Obsidian, étanche aux fichiers HTML). Deux fichiers produits, itérés et validés partiellement. Julie va faire un dernier retour sur les deux snippets avant de les considérer définitifs, puis on passera à l'étape 2 : création du `CLAUDE.md` à la racine du repo `JulieCOSSIN/drillcamp-workspace`.

* * *

**FICHIER 1 — `drillcamp-inc.css` (vault Drillcamp Inc)**

Chemin d'installation : `C:/Users/Julie/Documents/Drillcamp Inc/.obsidian/snippets/drillcamp-inc.css`

Tokens confirmés :

* Fond : `#101D1B` + gradient subtil `145deg` sur la vue note (effet profondeur liquid glass)
* Accent : `#B89A82` sable chaud (Option C choisie — remplace le terracotta `#AF5A3F`)
* Ardoise : `#739297`
* Police : DM Sans (Apple effect, remplace Plus Jakarta Sans)
* Liquid glass dark : `rgba(20,31,29,0.82)` + `blur(18px)`, border `rgba(255,255,255,0.11)`, shine `rgba(255,255,255,0.16)`

Sidebar — glass cards par entité avec `!important` (pour écraser le thème PLN) :

* Le Cockpit/PROCESS : `rgba(58,82,70,0.42)`, texte blanc `0.75`
* The Drillcamp : `rgba(58,82,70,0.50)`, texte `#94d8b6` (mint)
* JC Productions : `rgba(53,76,65,0.50)`, texte `#d8d694` (or)
* Les Yeux de Julie (Personal Brand) : `rgba(51,70,61,0.48)`, texte `#e8c4a4` (pêche)
* Voice Of Kings : `rgba(49,64,57,0.50)`, texte `#c4b4e8` (lavande)
* DrillSchool/Formation : `rgba(47,59,57,0.50)`, texte `#94c4e8` (bleu ciel)
* Find Your Church : `rgba(44,54,55,0.50)`, texte `#94d8b6` (teal)

Callouts glass sombre : `vision` (sable `184,154,130`), `kpi` (ardoise), `decision` (ambre), `next` (bleu acier), `ressource` (teal FYC).

Tags : `rgba(28,42,41,0.88)` + double inset shadow pour rendre l'effet glass visible.

Propriétés/Frontmatter : `padding-left: 2rem` sur `.metadata-content`.

cssclasses disponibles (à ajouter dans le frontmatter d'une note, visible en mode Lecture) : `mode-matrix` (terminal vert sur noir), `mode-nasa` (spatial bleu acier), `mode-gospel` (chaud or italique).

* * *

**FICHIER 2 — `chambre-haute.css` (vault La Chambre Haute)**

Chemin d'installation : `[vault La Chambre Haute]/.obsidian/snippets/chambre-haute.css`

Tokens confirmés :

* Fond : `#D4CDB8` (parchemin sombre, effet journal/livre ancien — remplace `#F7F4EF`)
* Accent : `#4A8B8C` (teal, confirmé option A)
* Muted : `#7A8A8A`
* Police principale : DM Sans (Apple effect — remplace Lora)
* Titres H1/H2 : Playfair Display (serif impactant, contraste éditorial avec le corps DM Sans)
* H3 : DM Sans 700, `#32302b`, sans uppercase (plus impactant, sombre)
* Liquid glass light : `rgba(212,205,184,0.65)` + `blur(14px)`, border `rgba(255,255,255,0.55)`, shine `rgba(255,255,255,0.80)`

Sidebar : toutes sections en `#32302b !important` (gris très foncé uniforme). Les deux notes racines (Tour de Contrôle, GUIDE) restent en teal `#4A8B8C` pour les distinguer.

Tags : `0.82rem`, glass ivoire avec border teal `rgba(74,139,140,0.25)`.

Propriétés/Frontmatter : `padding-left: 2rem` sur `.metadata-content`.

Callouts glass clair : `insight` (teal), `ressource` (ardoise), `citation` (brun éditorial), `next` (teal).

* * *

**Ce qui reste à faire**

1. Dernier retour de Julie sur les deux snippets (corrections si besoin)
2. Création du `CLAUDE.md` à la racine du repo `drillcamp-workspace` (conventions HTML des deux vaults pour Claude Code + VS Code)
3. Optionnel : mise à jour de la section "HTML par vault" dans `drillcamp-brandbook SKILL.md`

* * *

**Rappel contexte projet.** Repo GitHub : `JulieCOSSIN/drillcamp-workspace`. Token dans la session. Les snippets sont des fichiers `.css` à déposer dans `.obsidian/snippets/` de chaque vault, puis à activer via Réglages > Apparence > CSS Snippets.
