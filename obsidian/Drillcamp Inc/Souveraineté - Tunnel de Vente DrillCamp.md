---
type: note
role: architecture souveraine du tunnel de vente
maison_mere: "[[THE DRILLCAMP]]"
tags:
  - tunnel-de-vente
  - souveraineté
  - drillcamp-fr
  - drillquizz
  - drillschool
  - cloudflare
  - remotion
  - hyperframes
up: "[[COCKPIT]]"
Dans: "[[PROCESS]]"
related:
  - "[[THE DRILLCAMP]]"
  - "[[JC PRODUCTIONS]]"
  - "[[PERSONAL BRAND]]"
  - "[[DrillSchool - Formation]]"
  - "[[Dashboard Opérationnel - DrillCamp]]"
  - "[[DrillCamp OS]]"
  - "[[Workflow - Video Production]]"
  - "[[MOC CLAUDE]]"
created: 2026-06-10
updated: 2026-06-10
---

# Souveraineté - Tunnel de Vente DrillCamp

> Décision stratégique de rapatrier l'intégralité du tunnel de vente DrillCamp sous contrôle souverain. Trois propriétés à construire ou refondre : drillcamp.fr, le DrillQuizz, et DrillSchool. Stack commune : Claude Design + Claude Code + HyperFrames + Remotion + Cloudflare Pages + Amen.

---

## Pourquoi cette décision

Aujourd'hui trois points du tunnel dépendent d'outils tiers dont on ne contrôle ni le design, ni le code, ni la logique : Strikingly pour le site vitrine, ScoreApp pour le quizz, et aucune plateforme de formation encore construite. Ces dépendances ont des conséquences directes.

Strikingly impose ses templates et ses limites de personnalisation. On ne peut pas y intégrer des animations HyperFrames, des compositions vidéo Remotion, ni des interactions JavaScript sur mesure. Le site est le premier contact avec la marque DrillCamp. Si le contenant ne démontre pas ce qu'on vend, le message perd de sa force avant même d'être lu.

ScoreApp est un outil de quizz générique. Il fait ce qu'on lui demande et le DrillQuizz actuel est opérationnel. Mais il ne peut pas produire une page résultat personnalisée selon les réponses exactes du prospect, ni intégrer une vidéo générée dynamiquement à partir du score. Ce niveau de personnalisation est architecturalement impossible dans un SaaS tiers.

DrillSchool n'existe pas encore en tant que plateforme. La décision est de la construire de zéro, souverainement, avec le même stack que le DrillCamp OS.

Reprendre la souveraineté, c'est aussi cohérent avec ce qu'on vend. DrillCamp accompagne des leaders à matérialiser leurs visions. Le tunnel de vente de DrillCamp doit être lui-même une démonstration de ce niveau d'exécution.

---

## Architecture des trois chantiers

### Chantier 1 - Site drillcamp.fr

**Stack : HTML / CSS / JS vanilla + Cloudflare Pages**

Pas de React pour le site vitrine. React introduit un build system, une dépendance NPM, et une complexité de déploiement sans bénéfice concret pour un site statique. HTML vanilla avec Cloudflare Pages couvre tout ce que le site doit faire, avec un déploiement en 5 minutes via push GitHub.

Pages à refondre : Accueil, Consulting, À propos, Portfolio, Éthique, FAQ, et toutes les pages de l'offre par étage (CIBLER, ÉCLAIRER, FORER, RAYONNER).

**Rôle de Claude Design :** maquette interactive des pages, mode visuel par section (Apple Épuré pour les pages de fond, Gospel Hip-Hop pour les pages de conversion, NASA pour les pages de présentation de l'offre). Le skill `drillcamp-brandbook` est attaché à la conversation. Claude Design produit un rendu HTML temps réel dans son iframe. C'est l'outil de conception visuelle, pas de code de production.

**Rôle de HyperFrames :** production des assets vidéo et animations qui s'intègrent dans le site. Hero animé, intro de marque, b-rolls en background de sections, transitions entre blocs de contenu. Le rendu final est un MP4 ou un WebM embedé dans le HTML. HyperFrames n'est pas un builder de site, c'est un moteur de composition vidéo et d'animation qui produit les assets.

**Rôle de Remotion :** production des vidéos data-driven. La section "résultats" ou "l'offre en chiffres" du site peut contenir une vidéo de 10 à 15 secondes qui anime des statistiques (nombre d'accompagnements, taux de transformation, CA clients). Ces données changent. Remotion permet de créer un composant `StatsDrillCamp.tsx` qui lit un fichier JSON de données et génère la vidéo automatiquement. Quand les chiffres évoluent, on modifie le JSON et on relance le render. Même composition, nouveau contenu, zéro retouche d'animation. C'est scalable dans le temps d'une façon que HyperFrames, conçu pour des compositions fixes, ne couvre pas aussi naturellement.

**Rôle de Claude Code :** exécution du site. Reçoit la maquette Claude Design comme référence visuelle, les assets HyperFrames et Remotion à intégrer, et produit le HTML/CSS/JS de production. Responsive, performance, intégration des assets, navigation, formulaires.

**Hébergement :**
- Dépôt GitHub privé pour le site
- Connexion Cloudflare Pages sur ce dépôt (chaque push = déploiement automatique)
- Dans les paramètres Cloudflare Pages : ajout du domaine custom `drillcamp.fr`
- Dans Amen (registrar du domaine) : création d'un enregistrement CNAME `drillcamp.fr` pointant vers l'URL Cloudflare Pages fournie
- Strikingly est déconnecté une fois le site en production

---

### Chantier 2 - DrillQuizz custom

**Stack : React + Cloudflare Pages**

React est justifié ici contrairement au site vitrine. Un quizz est une interface à états multiples : l'utilisateur progresse question par question, son score se calcule en temps réel, la page résultat affiche du contenu conditionnel selon trois niveaux de score. Gérer ça en vanilla JS est possible mais produit du code difficile à maintenir dès qu'on ajoute de la logique de personnalisation. React rend les transitions d'état lisibles.

Le DrillQuizz actuel sur ScoreApp reste opérationnel pendant la construction du nouveau. Migration en coupure nette une fois la version custom validée.

**Rôle de Claude Design :** maquette des écrans. Landing du quizz, page de capture (popup 1 nom/org/email/décisionnaire/opt-in RGPD), interface des 15 questions avec les types existants (choix, sliding scale, texte libre), et les 3 pages résultat (score haut, score médian, score faible). Le ton calibré par niveau est conservé : haut = urgent, médian = curiosité, faible = bienveillant.

**Rôle de HyperFrames :** assets d'animation de l'interface. Transitions entre questions, animation de la barre de progression, reveal du score final. Exportés en WebM fond transparent ou en CSS/JS directement selon l'usage.

**Rôle de Remotion :** c'est le cas d'usage le plus différenciant de la stack. Remotion permet de produire une vidéo de résultat personnalisée jouée directement dans le navigateur via `@remotion/player`. Le composant React du quizz passe le score et les réponses clés au composant Remotion via props. Remotion génère une vidéo de 15 à 20 secondes qui contient le score du prospect animé, ses 2 ou 3 points de friction identifiés selon ses réponses exactes (pas un contenu générique pour "score médian"), et un CTA dynamique calibré. Chaque prospect voit une expérience vidéo construite à partir de ses propres réponses. Aucune plateforme SaaS de quizz ne peut produire ça. C'est la différence qui fait qu'un prospect se souvient du DrillQuizz.

**Connexion Calendly :** le CTA de la page résultat redirige vers l'URL Calendly avec les paramètres pre-fill dans l'URL (nom, email, organisation récupérés depuis le formulaire de capture). C'est la même logique que ScoreApp actuel, reproduite nativement dans Claude Code. En phase 2, quand Supabase est dans la boucle, les résultats du quizz peuvent être loggés automatiquement.

**Hébergement :** `quiz.drillcamp.fr` ou intégré dans `drillcamp.fr/quiz`. Même infrastructure Cloudflare Pages, CNAME dans Amen.

---

### Chantier 3 - DrillSchool

**Stack : HTML vanilla + Cloudflare Pages (v1) / React + Supabase si authentification nécessaire (v2+)**

L'architecture est déjà décidée dans `DRILLCAMP_OS_CONCEPTION_COMPLETE.md`. Aucune synchronisation avec le DrillCamp OS. Produit entièrement autonome. URL dédiée : `formation.drillcamp.fr`. Le seul pont avec l'OS : un bouton dans le Cockpit qui ouvre cette URL.

**Structure v1 :** 8 modules = 8 pôles = 8 pages HTML. Chaque page contient un texte d'introduction du pôle, une vidéo embed (YouTube non listé pour commencer), un bouton de téléchargement PDF guide, et une barre de progression du module gérée en localStorage. Tous les modules sont accessibles dès le départ. La séquence est suggérée, pas imposée.

**Rôle de Claude Design :** maquette du hub des 8 modules et d'une page module type. Univers visuel DrillCamp, NASA/Astronaute ou Apple Épuré selon le registre pédagogique voulu.

**Rôle de HyperFrames :** intro animée de la plateforme, assets visuels par module (titre animé, icone de pôle en motion, transitions).

**Rôle de Remotion :** trois usages structurants pour DrillSchool.

Premier usage : le composant `IntroModule.tsx`. Un seul composant React qui reçoit des props (numéro du module, titre du pôle, sous-titre, couleur d'accent) et génère l'intro vidéo du module. 8 renders avec 8 jeux de données différents produisent 8 intros cohérentes depuis un seul fichier de composition. Si le design évolue, on retouche le composant et on relance 8 renders. Sans Remotion, chaque intro est un projet HyperFrames séparé.

Deuxième usage : la progression visuelle animée. En début de session, DrillSchool peut afficher une vidéo courte "Vous avez complété 3 modules sur 8, soit 37%". Remotion génère cette vidéo dynamiquement depuis la progression stockée en localStorage. La vidéo est jouée via `@remotion/player` sans aucun export.

Troisième usage : les certificats d'achèvement personnalisés. Un composant `Certificat.tsx` avec une prop `{ nom: "Prénom NOM", date: "juin 2026", niveau: "Complété" }` produit une vidéo de 8 secondes jouée dans le navigateur ou exportée en MP4 téléchargeable. Chaque apprenant reçoit son certificat animé à son nom. Impossible à produire manuellement à l'échelle.

**Production de contenu (séquence opérationnelle) :**
- [ ] Script de chaque module : Claude Chat rôle PEDAGOGUE
- [ ] PDF guide illustré : Canva
- [ ] Vidéo courte par module : HyperFrames + Filmora
- [ ] Intro de module : Remotion (`IntroModule.tsx`)
- [ ] Intégration pages formation : embed YouTube + lien PDF
- [ ] Itération selon retours des 10 premiers clients

**Hébergement :** `formation.drillcamp.fr`. Même infrastructure Cloudflare Pages, CNAME dans Amen. Identique à `app.drillcamp.fr` et `drillcamp.fr`, sous-domaine différent.

---

## Stack commune aux trois chantiers

| Outil | Rôle dans la stack |
|---|---|
| Claude Design | Maquette visuelle, design system DrillCamp appliqué en temps réel |
| Claude Code | Exécution : HTML/CSS/JS ou React selon le chantier |
| HyperFrames | Assets vidéo et animation fixes : intro, b-roll, kinetic typo, WebM transparents |
| Remotion | Vidéos data-driven et personnalisées : stats animées, résultat quizz, intros de module, certificats |
| Higgsfield | B-roll cinématique et images héros premium via Kling 3.0 / Soul 2.0 (protocole crédits) |
| Filmora | Assemblage vidéo final avant embed |
| GitHub | Versioning de chaque propriété web (dépôts privés séparés) |
| Cloudflare Pages | Hébergement frontend de toutes les propriétés |
| Amen | Registrar : DNS, CNAME par sous-domaine |
| Supabase Frankfurt | Backend auth et données DrillCamp OS (déjà en place) |

**Règle HyperFrames vs Remotion :** HyperFrames produit des assets MP4/WebM pour Filmora et pour l'intégration web (embed). Remotion prend le dessus quand la vidéo est conditionnelle à des données variables (score, nom, statistiques, progression) ou quand elle doit être jouée directement dans une interface React via `@remotion/player` sans export. Les deux coexistent et ne se font pas concurrence.

---

## Processus de déploiement (commun aux trois propriétés)

```
1. Dépôt GitHub privé créé pour la propriété
2. Cloudflare Pages > Connect to Git > sélectionner le dépôt
3. Cloudflare génère une URL de déploiement (ex : drillcamp-site.pages.dev)
4. Dans les paramètres Cloudflare Pages : Custom domains > ajouter le domaine cible
5. Cloudflare fournit un enregistrement CNAME à créer
6. Amen > Gestion DNS de drillcamp.fr > Ajouter enregistrement CNAME
   Nom : [sous-domaine] ou @ pour l'apex
   Cible : l'URL fournie par Cloudflare
7. Propagation DNS : 5 minutes à 1 heure
8. HTTPS automatique activé par Cloudflare
```

Ce processus est identique pour `drillcamp.fr`, `quiz.drillcamp.fr`, `formation.drillcamp.fr`. Une fois fait pour le premier, les suivants prennent 10 minutes.

---

## État d'avancement

- [ ] Chantier 1 - Site drillcamp.fr : maquette Claude Design
- [ ] Chantier 1 - Assets HyperFrames (hero, b-rolls)
- [ ] Chantier 1 - Composant Remotion stats data-driven
- [ ] Chantier 1 - Exécution Claude Code
- [ ] Chantier 1 - Déploiement Cloudflare + CNAME Amen
- [ ] Chantier 2 - DrillQuizz React : maquette Claude Design
- [ ] Chantier 2 - Composant Remotion vidéo résultat personnalisée
- [ ] Chantier 2 - Exécution Claude Code
- [ ] Chantier 2 - Connexion Calendly pre-fill
- [ ] Chantier 2 - Déploiement
- [ ] Chantier 3 - DrillSchool v1 : maquette + 8 pages HTML
- [ ] Chantier 3 - Composant Remotion `IntroModule.tsx`
- [ ] Chantier 3 - Production contenu 8 modules (scripts, PDFs, vidéos)
- [ ] Chantier 3 - Déploiement `formation.drillcamp.fr`

---

> Tour de contrôle : [[COCKPIT]]
> Dans : [[PROCESS]]
> Entités servies : [[THE DRILLCAMP]] · [[JC PRODUCTIONS]] · [[PERSONAL BRAND]] · [[DrillSchool - Formation]]
