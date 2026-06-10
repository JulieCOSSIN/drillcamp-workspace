---
type: note
role: récapitulatif hebdomadaire
maison_mere: "[[COCKPIT]]"
tags:
  - recap
  - hebdo
  - claude
  - semaine
up: "[[COCKPIT]]"
related:
  - "[[MOC CLAUDE]]"
  - "[[DrillCamp OS]]"
  - "[[OFFRE GLOBALE DRILLCAMP]]"
  - "[[KPIS]]"
  - "[[Workflow - Video Production]]"
created: 2026-06-06
---

# Ce qu'on a fait cette semaine

> Récapitulatif complet de tout ce qui a été construit, conçu et documenté avec Claude du 31 mai au 6 juin 2026.
> Une semaine fondatrice : infrastructure, offre, méthode, et documentation de toute la structure.

---

## 31 mai — Workflow de production vidéo

Construction du workflow de production vidéo complet pour DrillCamp.

- [[Workflow - Video Production]] : note Obsidian documentant toute la chaîne de production, de l'idée au fichier publié, couvrant Claude, HyperFrames, Canva et CapCut
- Version visuelle [[Workflow - Video Production (Excalidraw)]] : schéma graphique interactif dans Obsidian
- Positionnement de CapCut clarifié : deux positions distinctes validées (pré-processing sur un clip avant Canva, ou post-processing sur le montage final après export Canva)
- Claude.ai positionné comme point de départ de toute production, y compris pour générer les prompts Claude Code et Claude Design

---

## 1er juin — KPIs, offre, campagne YouTube

### KPIs DrillCamp
- Analyse et enrichissement des KPIs existants : quatre couches manquantes identifiées (Conversion, Rétention, Email/Nurturing, Performance contenu)
- Production de [[KPIS]] : référentiel complet, 5 couches, benchmarks, cadence de suivi recommandée
- Top 3 KPIs prioritaires établis : taux Quizz vers RDV, taux RDV vers client, taux rétention vidéo

### MOC Cabinet Conseil
- Création de la MOC [[Drillcamp - Cabinet Conseil & Incubateur]] avec Dataview dynamique + Index Manuel
- Conventions découvertes : champs `entité` et `connected` propres aux MOC d'entité, `up` vers Tour de Contrôle

### Campagne YouTube publicitaire
- Script vidéo 45 secondes (étendu à 48s avec B-roll) : 5 scènes, 4 modes visuels DrillCamp
- Concept B-roll : entrepreneur au bureau, zoom arrière révèle le bureau isolé dans un champ de blé (invisibilité sur le marché)
- Deux prompts Gemini Veo écrits (version cinématique réaliste et version surréaliste)
- Décision funnel : CTA vers drillcamp.fr et non directement vers Calendly, pour tester le funnel complet
- Kling AI testé et évalué (résultats visiblement IA, Standard plan ~6,99$/mois, ~11 générations/mois)

---

## 5 juin — DC Finance + STRATEGIST OS

### DC Finance v1 à v4
- Application HTML standalone de suivi financier construite de zéro : 5 vues (Dashboard, Mois en cours, Récap annuel, Plan dettes, Référentiel)
- Charts SVG natifs (offline et compatibles Obsidian), persistance localStorage
- Données réelles migrées depuis le fichier Excel existant
- V3 : mécanismes de sauvegarde (export HTML autonome, JSON daté, import JSON)
- V4 : polish visuel Claude Design, calcul dîme repositionné
- Stack de déploiement arrêté : Cloudflare Pages + Indy pour la facturation maintenant, API Abby/Pennylane dans 6 mois

### STRATEGIST — Fusion Dashboard + DC Finance → DrillCamp OS
- Session de conception pure : aucun code, toutes les décisions architecturales tranchées
- Architecture de l'interface définie : Cockpit (instruments de bord) + 4 portes (Terrain, Chiffres, Vue rapide, Formation)
- Arbitrages clés : Supabase Frankfurt, Cloudflare Pages, app.drillcamp.fr, CRM dans les Chiffres (pas le Terrain), CA potentiel et effectif toujours séparés, pas de score global
- Deux versions de l'outil : interne (Julie) et template client (données à zéro, RLS isolé)
- Formation = produit séparé [[DrillSchool - Formation]], aucune synchronisation de données avec l'OS
- Livrable : `DRILLCAMP_OS_CONCEPTION_COMPLETE.md`, 15 sections, autoportant

---

## 6 juin matin — EXECUTOR + Offre Globale

### EXECUTOR — Backend Supabase
- Schéma SQL complet généré table par table, dans l'ordre logique des dépendances
- Compte Supabase créé (region Frankfurt, thedrillcamp@gmail.com)
- SQL exécuté : 16 tables, contraintes, fonctions, triggers, seeds, pg_cron
- RLS activé sur toutes les tables, helper `is_internal()`
- Authentification configurée, premier compte créé
- Promotion du compte en rôle `internal` effectuée
- Re-seed des 28 missions internes : 89 missions totales en base (28 internes + 61 client)
- Automatismes vérifiés en conditions réelles : `handle_new_user` a généré le profil automatiquement, seed a créé les 61 missions client
- Discordance résolue : le chiffre de référence est 89 missions (pas 92 annoncé initialement)
- Deux points ouverts déterminés : `is_pole_operational` mis à jour avec condition OR pour les récurrentes, contrainte UNIQUE sur `projects`

### Offre Globale DrillCamp
- Gamme complète à 4 étages structurée et documentée dans [[OFFRE GLOBALE DRILLCAMP]]
- CIBLER : diagnostic 75 min, 150€, synthèse PDF personnalisée sous 24-48h
- ÉCLAIRER : conseil par angle sur les 8 pôles (Async 120€, Flash 180€, Pack 480€)
- FORER : services exécutifs (Branding 2-2,5k€, Audiovisuel 800-1,5k€, Accompagnement 600-900€/mois)
- RAYONNER : Formation 850€ + 1 an OS offert, OS 19€/mois ou 205€/an
- Fondation interne : Habacuc 2:2-3
- Accroche OS : "Votre vision et votre cible, à portée de main et des yeux."

---

## 6 juin après-midi — Infrastructure Obsidian complète

Une session entière dédiée à documenter et structurer tout ce qui avait été construit.

### Notes créées pour le vault La Chambre Haute (Tech/Claude)
- [[Comment nous avons conçu le DrillCamp OS]] : tutoriel narratif, méthode STRATEGIST/EXECUTOR
- [[Comment nous avons structuré nos notes Obsidian avec Claude]] : retour d'expérience sur cette session
- [[Créer des rôles dans ses conversations Claude]] : concept des rôles comme AI agents
- [[Rôles Claude - définition et suggestion]] : référence injectable, 9 rôles définis, taxonomie, protocole de suggestion
- GUIDE - Structure des notes Obsidian [La Chambre Haute] : note racine avec conventions complètes

### Notes créées pour le vault Drillcamp Inc (dossier Claude)
- [[DrillCamp OS]] : note fusionnée, historique + état opérationnel + usage par entité
- [[MOC CLAUDE]] : cartographie complète de tout ce qui a été fait avec Claude
- [[Rôles Claude - Attribution DrillCamp]] : attribution des rôles par type de mission DrillCamp
- [[Comment nous avons conçu le DrillCamp OS]] : copie adaptée depuis La Chambre Haute, version narrative
- GUIDE - Structure des notes Obsidian [Drillcamp Inc] : note racine avec conventions complètes

### Documents de contexte Claude (hors vault, en mémoire projet)
- METHODE_NOTES_OBSIDIAN_DRILLCAMP.md v2 : référence rapide distinguant les deux vaults, frontmatters types, types de notes, règles de formatage
- CARTOGRAPHIE_VAULT_DRILLCAMP_INC.md : structure complète du vault Drillcamp Inc avec hubs, clusters, isolés intentionnels
- CARTOGRAPHIE_VAULT_LA_CHAMBRE_HAUTE.md : structure complète du vault La Chambre Haute

---

## Ce qui reste ouvert

### DrillCamp OS
- [ ] Test du reste des automatismes Supabase
- [ ] Réécriture du frontend (localStorage → Supabase)
- [ ] Dépôt GitHub + déploiement Cloudflare Pages
- [ ] Configuration domaine app.drillcamp.fr (CNAME dans Amen)
- [ ] Polish visuel avec Claude Design dans l'univers DrillCamp
- [ ] Construction de formation.drillcamp.fr

### Contenu
- [ ] Stratégie TikTok (conversation dédiée à planifier)
- [ ] Montage et production vidéo YouTube SONCAS-E (script produit, montage à faire)
- [ ] Bilan de clôture à formaliser

---

> Tour de contrôle : [[COCKPIT]]
> Méthode de travail : [[MOC CLAUDE]]
