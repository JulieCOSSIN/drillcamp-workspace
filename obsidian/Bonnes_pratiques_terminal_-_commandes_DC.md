---
type: référence
role: référentiel opérationnel des commandes terminal utilisées dans les workflows DrillCamp
maison_mere: "[[THE DRILLCAMP]]"
tags:
  - terminal
  - git
  - hyperframes
  - vscode
  - process
up: "[[COCKPIT]]"
Dans: "[[PROCESS]]"
related:
  - "[[MOC CLAUDE]]"
  - "[[Workflow - Video Production]]"
  - "[[DrillCamp OS]]"
---

# Bonnes pratiques terminal - Commandes

Terminal principal : **VS Code** (panneau intégré). **GitBash** utilisé ponctuellement pour Git sur Windows. Les commandes `npx` et `npm` ne nécessitent pas GitBash - elles tournent dans le terminal VS Code directement.

Règle de coût : toutes les commandes ci-dessous ne consomment aucun token Claude. Seule l'ouverture d'une session Claude Code (`claude`) dans un dossier projet consomme des tokens.

---

## Navigation et fichiers

Se positionner dans un dossier :

```bash
cd nom-du-dossier
```

Chemin avec espaces (guillemets obligatoires) :

```bash
cd "C:\Users\Julie\Documents\Projets Video Hyperframes"
```

Remonter d'un niveau :

```bash
cd ..
```

Afficher le répertoire courant :

```bash
pwd
```

Lister les fichiers :

```bash
ls
```

Créer un dossier :

```bash
mkdir nom-du-dossier
```

Ouvrir VS Code dans le dossier courant :

```bash
code .
```

---

## Vérifications d'environnement

Version Node.js (minimum v22 pour HyperFrames) :

```bash
node --version
```

Version FFmpeg (minimum 7.x pour le rendu WebM) :

```bash
ffmpeg -version
```

Installer FFmpeg via winget (Windows) :

```bash
winget install ffmpeg
```

---

## Git - Pipeline DrillCamp OS / GitHub

Initialiser un repo Git local :

```bash
git init
```

Vérifier l'état du repo (fichiers modifiés, non suivis) :

```bash
git status
```

Stager tous les changements :

```bash
git add .
```

Commiter avec message :

```bash
git commit -m "feat: connexion Supabase missions"
```

Pousser vers GitHub (déclenche le redéploiement Cloudflare Pages automatiquement) :

```bash
git push origin main
```

Récupérer les modifications depuis GitHub :

```bash
git pull origin main
```

Cloner le repo DrillCamp en local (premier setup ou nouvelle machine) :

```bash
git clone https://github.com/JulieCOSSIN/drillcamp-workspace
```

Historique des commits en format condensé :

```bash
git log --oneline
```

---

## HyperFrames - Workflow vidéo

Vérifier l'environnement complet (Node, FFmpeg, Chrome, mémoire) :

```bash
npx hyperframes doctor
```

Télécharger le Chrome headless bundlé si manquant :

```bash
npx hyperframes browser ensure
```

Initialiser un nouveau projet (crée index.html + hyperframes.json + assets/) :

```bash
npx hyperframes init nom-du-projet --non-interactive
```

Lancer le Studio en live reload (prévisualisation frame-accurate, 0 token) :

```bash
npx hyperframes preview
```

Valider la structure avant rendu :

```bash
npx hyperframes lint
```

Inspecter la composition :

```bash
npx hyperframes inspect
```

Rendre en MP4 :

```bash
npx hyperframes render
```

Rendre en WebM avec canal alpha (watermarks et logos animés) :

```bash
npx hyperframes render --format webm --output "../_renders/dc-2026-06-nom.webm"
```

Retirer le fond d'une facecam avant montage :

```bash
npx hyperframes remove-background mafacecam.mp4
```

Installer ou mettre à jour les skills HyperFrames (Claude Code) :

```bash
npx skills add heygen-com/hyperframes
```

---

## npm

Installer les dépendances après un git clone :

```bash
npm install
```

---

## Pipeline de déploiement DrillCamp OS (rappel)

```
Claude Code modifie le frontend
  → review dans VS Code
  → git add . && git commit -m "..." && git push origin main
  → Cloudflare Pages détecte le push
  → app.drillcamp.fr redéployé en moins de 60 secondes
```

- [ ] Vérifier `git status` avant tout push
- [ ] Message de commit au format `feat:` / `fix:` / `style:` / `refactor:`
- [ ] Toujours `npx hyperframes lint` avant `render`

---

> Tour de contrôle : [[COCKPIT]]
> Dans : [[PROCESS]]
> Entités servies : [[THE DRILLCAMP]] · [[JC PRODUCTIONS]]
> Voir aussi : [[Workflow - Video Production]] · [[DrillCamp OS]] · [[MOC CLAUDE]]
