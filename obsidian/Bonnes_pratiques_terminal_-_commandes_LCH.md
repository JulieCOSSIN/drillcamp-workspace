---
type: référence
role: référentiel des commandes terminal essentielles pour les workflows quotidiens
tags:
  - tech
  - terminal
  - git
  - hyperframes
  - vscode
up: "[[MOC Tech]]"
related:
  - "[[MOC Claude]]"
  - "[[Workflow - Video Production]]"
---

# Bonnes pratiques avec son terminal - Commandes

Terminal principal : VS Code (panneau Terminal intégré). GitBash utilisé ponctuellement pour Git en contexte Windows.

---

## Navigation et dossiers

Se déplacer dans un dossier :

```bash
cd nom-du-dossier
```

Se déplacer avec un chemin contenant des espaces (guillemets obligatoires) :

```bash
cd "C:\Users\Julie\Documents\Projets Video Hyperframes"
```

Remonter d'un niveau :

```bash
cd ..
```

Afficher le chemin courant (où suis-je ?) :

```bash
pwd
```

Lister les fichiers du dossier courant :

```bash
ls
```

Créer un nouveau dossier :

```bash
mkdir nom-du-dossier
```

Ouvrir VS Code dans le dossier courant :

```bash
code .
```

---

## Vérification d'environnement

Vérifier la version de Node.js installée (minimum v22) :

```bash
node --version
```

Vérifier que FFmpeg est disponible et sa version :

```bash
ffmpeg -version
```

Installer FFmpeg via le gestionnaire de paquets Windows :

```bash
winget install ffmpeg
```

---

## Git - Cycle de base

Initialiser un repo Git local dans le dossier courant :

```bash
git init
```

Voir l'état du repo (fichiers modifiés, en attente, non suivis) :

```bash
git status
```

Stager tous les changements (prêts à être commités) :

```bash
git add .
```

Créer un commit avec un message :

```bash
git commit -m "feat: description du changement"
```

Envoyer les commits vers GitHub (branche main) :

```bash
git push origin main
```

Récupérer les changements depuis GitHub :

```bash
git pull origin main
```

Cloner un repo GitHub en local :

```bash
git clone https://github.com/JulieCOSSIN/nom-du-repo
```

Voir l'historique des commits (format condensé) :

```bash
git log --oneline
```

---

## HyperFrames - Dev loop complet

Vérifier que l'environnement HyperFrames est opérationnel :

```bash
npx hyperframes doctor
```

Télécharger le Chrome headless bundlé si absent :

```bash
npx hyperframes browser ensure
```

Initialiser un nouveau projet (crée index.html + hyperframes.json + assets/) :

```bash
npx hyperframes init nom-du-projet --non-interactive
```

Lancer le Studio en live reload (prévisualisation frame-accurate) :

```bash
npx hyperframes preview
```

Valider la structure avant le rendu :

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

Rendre en WebM avec canal alpha transparent, vers le dossier _renders/ :

```bash
npx hyperframes render --format webm --output "../_renders/nom-2026-06.webm"
```

Retirer l'arrière-plan d'une vidéo (facecam) :

```bash
npx hyperframes remove-background mafacecam.mp4
```

Installer ou mettre à jour les skills HyperFrames :

```bash
npx skills add heygen-com/hyperframes
```

---

## Node / npm

Installer les dépendances d'un projet (après un git clone) :

```bash
npm install
```

---

## Rappel : terminal VS token

Les commandes terminal (cd, mkdir, git, npx hyperframes init/preview/render) ne consomment aucun token Claude. Seule la session Claude Code ouverte dans le dossier projet consomme des tokens. Séparer les deux mentalement pour raisonner sur les coûts.

---

> Document parent : [[MOC Tech]]
> Dans dossier : [[MOC Tech]] · Dans [[MOC Connaissances]]
> Voir aussi : [[MOC Claude]] · [[Workflow - Video Production]]
