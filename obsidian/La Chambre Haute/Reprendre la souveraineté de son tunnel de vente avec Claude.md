---
type: tutoriel
role: retour d'expérience et guide opérationnel
tags:
  - tech
  - claude
  - souveraineté
  - tunnel-de-vente
  - remotion
  - hyperframes
  - cloudflare
up: "[[MOC Claude]]"
related:
  - "[[Comment nous avons conçu le DrillCamp OS]]"
  - "[[Créer des rôles dans ses conversations Claude]]"
  - "[[Rôles Claude - définition et suggestion]]"
  - "[[MOC Tech]]"
created: 2026-06-10
updated: 2026-06-10
---

# Reprendre la souveraineté de son tunnel de vente avec Claude

> Décision de rapatrier l'intégralité du tunnel de vente DrillCamp sous contrôle souverain. Ce tutoriel documente pourquoi on fait ça, comment la stack fonctionne, et le rôle exact de chaque outil. À lire comme un guide de méthode, pas comme une liste de tâches.

---

## Pourquoi sortir des outils SaaS pour son tunnel de vente

La question n'est pas de savoir si Strikingly, ScoreApp ou une plateforme de formation font leur travail. Ils le font. La question est de savoir ce qu'on sacrifie en leur déléguant le tunnel de vente d'une marque premium.

Un site vitrine sur Strikingly est contraint par les templates et les limites de personnalisation de la plateforme. On ne peut pas y intégrer des animations vidéo sur mesure, des compositions interactives, ni des interactions JavaScript complexes. Or le site est le premier contact avec la marque. Si le contenant ne démontre pas le niveau d'exécution que la marque vend, le message perd de sa force avant même d'être lu.

Un quizz sur ScoreApp produit des pages résultat génériques par niveau de score. Tous les prospects avec un score de 65% voient exactement la même page. Il est architecturalement impossible de produire, depuis ScoreApp, une expérience personnalisée à partir des réponses exactes de chaque prospect.

Et une plateforme de formation SaaS type Kajabi ou Teachable coûte entre 150 et 400 euros par mois, impose sa structure de cours, et ne permet aucune intégration brand sur mesure.

Sortir de ces dépendances, c'est aussi une cohérence. Si on accompagne des leaders à matérialiser leurs visions, le tunnel de vente de cet accompagnement doit être lui-même une démonstration de ce niveau d'exécution.

---

## La stack choisie et pourquoi elle fonctionne ensemble

La stack repose sur six outils principaux. Chacun a un rôle précis et ne double pas les autres.

**Claude Design** est l'outil de maquettage visuel. On lui attache le brand system DrillCamp (skill `drillcamp-brandbook`) et on lui décrit les pages voulues. Il produit un rendu HTML temps réel dans son interface. Ce n'est pas du code de production : c'est la conception visuelle. On sort de cette étape avec une référence claire pour Claude Code.

**Claude Code** est l'outil d'exécution. Il reçoit la maquette Claude Design comme référence, les assets vidéo produits par HyperFrames et Remotion, et il écrit le code de production : HTML, CSS, JavaScript, ou React selon le chantier. C'est lui qui déploie sur GitHub et Cloudflare Pages.

**HyperFrames** produit les assets vidéo et d'animation fixes. Intro de marque, hero animé, b-rolls de fond de section, WebM à fond transparent pour les overlays. On écrit une composition HTML avec des animations GSAP, HyperFrames la rend en MP4 ou WebM. Ces fichiers sont ensuite embedés dans le site ou assemblés dans Filmora. HyperFrames fonctionne entièrement en local, sans abonnement supplémentaire, et le rendu est déterministe frame par frame.

**Remotion** produit les vidéos data-driven et personnalisées. C'est la distinction fondamentale avec HyperFrames : dans Remotion, une vidéo est un composant React. Chaque frame est rendue à un timestamp donné à partir de props passées au composant. On peut donc créer une vidéo qui change de contenu selon des données variables : un score de quizz, un nom de personne, une statistique mise à jour, un niveau de progression. HyperFrames ne fait pas ça nativement. Remotion le fait par nature, parce que c'est du React.

**Higgsfield** (via MCP) produit les assets b-roll cinématiques et les images héros premium via Kling 3.0 et Soul 2.0. C'est le seul outil de la stack qui coûte des crédits par génération. Le protocole Higgsfield DrillCamp impose de vérifier le solde avant toute génération et de proposer d'abord les alternatives à 0 crédit.

**Cloudflare Pages + Amen** est l'infrastructure d'hébergement. Cloudflare Pages déploie automatiquement à chaque push GitHub, fournit le HTTPS, et distribue via CDN mondial. Amen est le registrar du domaine `drillcamp.fr`. Pour chaque propriété web, on crée un CNAME dans Amen qui pointe vers l'URL Cloudflare Pages fournie.

---

## Les trois propriétés à construire

### Le site drillcamp.fr

Site vitrine en HTML vanilla. Pas de React : pour un site statique, un framework JavaScript ajoute de la complexité sans bénéfice. Pages à construire : Accueil, Consulting, À propos, Portfolio, Éthique, FAQ, pages de l'offre.

HyperFrames produit le hero animé et les b-rolls de fond de section. Remotion produit les vidéos data-driven : la section "résultats en chiffres" du site contient une vidéo courte qui anime des statistiques lues depuis un fichier JSON. Quand ces chiffres changent, on modifie le JSON et on relance le render. La composition ne change pas.

Pour l'hébergement : dépôt GitHub du site + Cloudflare Pages connecté + CNAME `drillcamp.fr` dans Amen. Strikingly est déconnecté une fois le site en production.

### Le DrillQuizz custom

Interface React. La gestion d'états multiples (progression question par question, calcul du score en temps réel, page résultat conditionnelle) justifie React ici, contrairement au site vitrine.

Le DrillQuizz actuel sur ScoreApp reste opérationnel pendant la construction. Migration en coupure nette une fois la version custom validée.

Le cas d'usage Remotion le plus différenciant de toute la stack se joue ici. À la fin du quizz, le composant React passe le score et les réponses clés à un composant Remotion. `@remotion/player` joue cette vidéo directement dans le navigateur, sans export. La vidéo contient le score du prospect animé, ses 2 ou 3 points de friction identifiés à partir de ses réponses exactes (pas d'un contenu générique pour "score médian"), et un CTA dynamique calibré. Chaque prospect vit une expérience construite à partir de ce qu'il a répondu. C'est architecturalement impossible dans n'importe quel SaaS de quizz existant.

La connexion vers Calendly fonctionne via pre-fill URL : les paramètres nom, email, organisation sont injectés dans l'URL Calendly au clic sur le CTA. Même logique que ScoreApp, reproduite nativement.

### DrillSchool

Plateforme de formation entièrement autonome. URL dédiée `formation.drillcamp.fr`. Aucune synchronisation avec le DrillCamp OS. Le seul pont entre les deux : un bouton dans le Cockpit de l'OS qui ouvre cette URL. Une fois sur la formation, aucun lien vers l'outil. Une fois dans l'outil, aucun lien vers la formation.

Structure v1 : 8 pages HTML, une par pôle. Chaque page contient une introduction, une vidéo embed YouTube (non listé), un PDF téléchargeable, et une barre de progression locale en localStorage.

Remotion a trois usages structurants dans DrillSchool.

Le composant `IntroModule.tsx` est un seul composant React qui reçoit les données du module en props (numéro, titre, sous-titre, couleur d'accent) et génère l'intro vidéo correspondante. 8 renders avec 8 jeux de données différents produisent 8 intros cohérentes depuis un seul fichier de composition. Si le design évolue, on retouche le composant une fois et on relance 8 renders. Sans Remotion, chaque intro est un projet HyperFrames séparé à maintenir individuellement.

La progression visuelle animée est jouée via `@remotion/player` en début de session : "Vous avez complété 3 modules sur 8." La vidéo est générée dynamiquement depuis la progression stockée en localStorage. Aucun export nécessaire.

Les certificats d'achèvement personnalisés : un composant `Certificat.tsx` avec les props `{ nom, date, niveau }` produit une vidéo de 8 secondes jouée dans le navigateur ou exportée en MP4 téléchargeable. Chaque apprenant reçoit un certificat animé à son nom. C'est scalable : un composant, autant de certificats que d'apprenants.

---

## La règle HyperFrames vs Remotion

Ce n'est pas une compétition. Ce sont deux outils complémentaires avec des zones d'excellence différentes.

HyperFrames prend en charge tout ce qui est fixe : une composition dont le contenu ne change pas selon des données variables. Intro de marque, b-roll, kinetic typography, logo animé, WebM à fond transparent pour Filmora. Le pipeline HyperFrames produit des MP4 ou WebM qui entrent dans Filmora ou s'embedent directement dans le HTML.

Remotion prend en charge tout ce qui est conditionnel à des données : une vidéo dont le contenu change selon un score, un nom, une statistique, un niveau de progression. Et tout ce qui doit être joué directement dans une interface React sans export de fichier.

Le skill `remotion-to-hyperframes` installé dans Claude Code sert à migrer des projets Remotion existants vers HyperFrames si on veut un rendu MP4 via le pipeline HyperFrames. C'est le pont entre les deux quand les deux sont dans le projet.

---

## La logique d'hébergement à retenir

Toutes les propriétés web DrillCamp suivent le même schéma.

```
Dépôt GitHub privé
       ↓
Cloudflare Pages (connecté au dépôt)
       ↓
URL de déploiement automatique (ex : projet.pages.dev)
       ↓
CNAME dans Amen
(sous-domaine → URL Cloudflare Pages)
```

On fait cette procédure une fois pour `drillcamp.fr`, une deuxième fois pour `quiz.drillcamp.fr`, une troisième fois pour `formation.drillcamp.fr`. Chaque fois identique, chaque fois 10 minutes.

---

## Ce que cette approche change structurellement

Le niveau d'exécution ne dépend plus des limites des outils SaaS. Une page résultat de quizz avec une vidéo personnalisée par les réponses exactes du prospect : c'est une expérience que personne d'autre dans l'espace conseil indépendant français ne peut proposer sans agence et sans budget conséquent. Avec cette stack, c'est Claude Code + Remotion + une heure de travail.

C'est aussi vrai pour la formation. 8 intros de modules cohérentes depuis un seul composant, des certificats animés à la demande, une progression visuelle dynamique : ce qui serait un projet de développement sur devis devient un deliverable Claude Code d'une session.

Le tunnel de vente devient une démonstration continue de ce que DrillCamp sait faire faire à ses clients.

---

> Document parent : [[MOC Claude]]
> Dans dossier : [[MOC Tech]] · Dans [[MOC Connaissances]]
> Voir aussi : [[Comment nous avons conçu le DrillCamp OS]] · [[Créer des rôles dans ses conversations Claude]]
