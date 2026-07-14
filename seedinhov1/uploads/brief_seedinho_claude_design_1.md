# BRIEF CLAUDE DESIGN — SEEDINHO (MVP web app)

> À coller tel quel dans Claude Design. Le contenu football ci-dessous est **dérivé fidèlement de la vraie transcription du coach** (§4.1) : ne rien inventer en plus, ne rien retirer. Construis une **web app mobile-first cliquable**, pas des maquettes statiques.

---

## 0. CE QUE TU CONSTRUIS EN UNE PHRASE

Une web app mobile-first qui transforme le débrief oral d'un coach amateur en rapports individuels de niveau centre de formation — chaque rapport doit donner au joueur l'impression qu'un **staff** l'accompagne personnellement après le match.

**Positionnement fondateur (à respecter partout) :** Seedinho n'est **pas** une app d'IA. C'est un **staff numérique au service du coach**. Le coach reste l'expert ; le produit organise, structure, traduit pédagogiquement et prolonge son travail. Jamais le ton d'un outil techno — le ton d'un staff bienveillant.

---

## 1. RÈGLES NON-NÉGOCIABLES

Priment sur tout le reste.

1. **Jamais un PDF.** Rendu app premium (Apple / Nike / Hudl / Strava). Cartes, espace, rythme vertical, micro-interactions.
2. **Jamais inventer.** Chaque phrase découle des observations du coach (§4). Aucune qualité, aucun défaut, aucune stat inventés.
3. **Jamais « points faibles ».** On dit **« axes prioritaires de progression »**, formulé positivement.
4. **Jamais juger.** Le joueur ne se sent jamais noté. Il se sent accompagné. (Cas sensibles : §4.6.)
5. **Jamais une marketplace.** Spécialistes = **« Le staff Seedinho recommande… »** / **« Pour aller plus loin… »**. Jamais « Acheter », « Débloquer », « Premium », « Panier ».
6. **Une seule main suffit.** Cibles ≥ 44px, actions dans le pouce, navigation minimale.
7. **Lisible en moins d'une minute.** Hiérarchie forte, pas de pavés.

---

## 2. DESIGN SYSTEM

### Fondations
- **Mobile first**, viewport de référence **390 px**. Desktop = même colonne centrée (~430 px) sur fond neutre.
- **Fond blanc dominant.** Beaucoup d'espace blanc — l'air fait partie du luxe.
- Grille d'espacement **8 pt** (4, 8, 12, 16, 24, 32, 48). Gouttières d'écran **20–24 px**.

### Couleurs (tokens) — vert officiel Seedinho
```
--green-700  #02562d   /* vert Seedinho OFFICIEL (extrait du logo) — primaire, profond */
--green-500  #0A6E3B   /* variante plus claire — hover / états interactifs */
--green-50   #E9F3ED   /* tint — badges, surfaces vertes douces, fond de courbe */
--ink        #0E1B14   /* texte principal */
--muted      #6B7280   /* texte secondaire, labels */
--line       #EEF0F2   /* bordures très légères */
--surface    #F7F8FA   /* fond neutre derrière cartes, rare */
--white      #FFFFFF
```
- `#02562d` est un **vert sapin profond** : parfait sur fond blanc, il donne un rendu premium « académie ». Texte posé sur `--green-700` = blanc.
- Vert = accent (boutons primaires, valeurs clés, coches de progression, marqueur de courbe, pastilles « fait »), jamais aplat plein écran sauf une éventuelle zone héro maîtrisée. Aucune autre couleur de marque.

### Typographie
- **Inter** (ou géométrique sobre équivalent) partout.
- Échelle : Display 32/700 · H1 24/700 · H2 18/600 · Body 15–16/400-500 · Caption 13/500 uppercase + letter-spacing pour les labels de section (« TES POINTS FORTS »).
- Gros chiffres (stats, n° de maillot) : poids fort, tracking serré, style sport.

### Formes & profondeur
- Rayons : cartes **20–24 px** · boutons **pilule** ou 16 px · pastilles full.
- Ombres **douces et basses** (`0 8px 24px rgba(2,86,45,.06)`). Éviter les bordures dures — ombre légère + `--line` discret.
- Icônes **fines, monoline** (style Lucide/Feather). Jamais colorées, jamais d'emoji.

### Micro-animations (clé du « premium »)
- Cartes de section : fade + translate-up au scroll (stagger).
- Stats : count-up à l'entrée. Boutons : press-state (scale 0.98).
- Onde sonore animée + transcription qui s'écrit progressivement (écran Démonstration).
- Transitions d'écran fluides. Toujours discret, jamais clownesque.

### Composants réutilisables
`AppHeader` · `PlayerCard` · `SectionCard` · `StatPill` · `ObjectiveCard` (accent vert) · `SpecialistCard` (ton « staff recommande » + badge « Bientôt disponible ») · `SeasonChart` · `Waveform` · `StepChecklist` · `PrimaryButton` / `GhostButton` · nav minimale.

### Logo (deux jeux fournis)
- **Versions vertes** (`full_vert`, `texte_vert`, `vert`/icône) → pour **fond blanc** (le cas dominant). Header sur fond blanc = icône `vert` (+ texte au besoin).
- **Versions blanches** (`full_blanc`, `texte_blanc`, `blanc`) → pour **surfaces vertes/sombres** (zone héro verte, éventuel splash).

---

## 3. LES ÉCRANS

Parcours : **Landing → Démonstration → Liste des joueurs → Rapport individuel → Plan de progression** (+ Progression saison intégrée au rapport).

### 3.1 Landing
- Héro épuré (fond blanc + logo vert, ou bloc vert `#02562d` + logo blanc — sobre).
- **Slogan (exact) :** « Donner à chaque joueur amateur un suivi digne d'un centre de formation. »
- Sous-texte : 1 phrase sur le staff numérique.
- **CTA unique (exact) :** « Découvrir la démonstration ».
- Rien d'autre au-dessus de la ligne de flottaison.

### 3.2 Démonstration (le « aha »)
En 15 s, on comprend que l'IA transforme les **paroles du coach** en **suivi individuel**.
- Lecteur audio du débrief (audio placeholder). Bouton play central + **onde sonore animée**.
- **Transcription qui apparaît progressivement** (texte §4.1), synchronisée.
- **Checklist qui se coche séquentiellement :**
  1. ✓ Transcription
  2. ✓ Identification automatique des joueurs
  3. ✓ Analyse des observations
  4. ✓ Génération des rapports
- Fin : bouton « Voir les rapports de l'équipe » → Liste des joueurs.

### 3.3 Liste des joueurs
- Titre : « Match — AS Charte 0 – 2 Pontois FC · 4-3-3 ».
- Liste de **PlayerCard** : photo (Claude Design gère les photos ; avatar initiales en secours), numéro (style maillot), **prénom**, poste, « Dernier rapport · il y a 2 jours », carte cliquable « Voir le rapport ».
- Roster complet + prénoms au §4.2. Mettre **Lucas — Gardien (#1)** en avant : rapport héros le plus complet.

### 3.4 Rapport individuel — L'ÉCRAN LE PLUS IMPORTANT
Professionnel, motivant, bienveillant, lisible, premium. Impression que le coach a passé 20 min sur ce joueur. Traduire le vocabulaire technique en langage clair pour un 13-19 ans.

Structure verticale, une **SectionCard** par bloc, label caption vert :
1. **En-tête joueur** : photo, prénom, n°, poste, match (« AS Charte 0 – 2 Pontois FC »). 2-3 StatPills sobres dérivées des observations (jamais inventées).
2. **Résumé du match** — fidèle aux observations.
3. **Tes points forts** — uniquement les qualités observées. *(Si aucune n'est citée : voir §4.6, ne pas inventer.)*
4. **Tes axes prioritaires de progression** — formulation positive.
5. **Ton objectif pour le prochain match** — carte accent vert, concret / simple / actionnable.
6. **Ce que Seedinho remarque** — interprétation pédagogique ; prolonge le coach, ne le contredit jamais.
7. **Progression saison** (voir 3.6).
8. En continuité (pas une page vendeuse) : le **Plan de progression** (3.5), amené par « Pour aller plus loin… ».

Le rapport **ne se termine pas** : il **ouvre** le plan de progression.

### 3.5 Plan de progression personnalisé — LE DIFFÉRENCIATEUR
Introduit par « Pour aller plus loin, le staff Seedinho te propose… ». Chaque item est **directement lié à une observation précise**, jamais générique.

**Toujours affichés :** Exercice individuel conseillé · Conseil pour le prochain entraînement (chacun lié à une observation).

**Spécialistes IA — n'apparaissent QUE si l'observation les déclenche** (logique §5). Chacun = SpecialistCard ton « Le staff Seedinho recommande », badge discret « Bientôt disponible », **zéro signal marchand** : Analyse vidéo personnalisée · Gestion de la récupération / sommeil · Préparateur physique IA · Préparateur mental IA · Nutritionniste IA · Plans d'entraînement.

> **⚠️ Fidélité à CETTE transcription :** sur les 11 joueurs, seuls se déclenchent **Analyse vidéo** (Lucas #1 + Malik #6) et **Récupération** (Enzo #3). **Prépa physique, mental et nutrition n'apparaissent chez PERSONNE** — le coach n'en parle jamais. La personnalisation se voit à ce qui **n'apparaît pas**. Ne force aucun spécialiste.

### 3.6 Progression saison (dans le rapport)
- **SeasonChart** : courbe d'un indicateur d'impact sur les derniers matchs (données §4.5, **simulées pour la démo**, cohérentes avec l'axe réel du joueur).
- **Résumé de progression** (1-2 phrases) · **Objectifs atteints** (coches vertes) · **Axes récurrents**.

---

## 4. CONTENU SIMULÉ FOURNI (à utiliser tel quel)

### 4.1 Transcription réelle du débrief coach (source unique de tout le reste)
Contexte : **AS Charte 0 – 2 Pontois FC**, en **4-3-3**, **défaite 2-0**. Deux joueurs **U13** jouent un an au-dessus et débutent dans le 11 (les attaquants Adam #9 et Younes #11) ; Gabriel #5 joue aussi un an au-dessus.

> « Ce week-end, mon numéro 1, le gardien, a fait un bon petit match dans les buts, sa sortie aérienne était intéressante, son jeu au pied aussi. Là où il aurait pu faire mieux, c'est dans l'utilisation de son ballon, dans ses choix : techniquement c'est intéressant, mais au pied il faut être capable de choisir les bonnes solutions. Mon 2 : match référence, techniquement pas de souci, il a déséquilibré le bloc après 2-3 un-contre-un réussis. Mon numéro 3 est sorti très rapidement sur un coup, match compliqué à juger. Mon 4, central, à l'aise, correct au pied, jeu court comme jeu long, il a réussi à sortir du marquage quelques fois ; à lui d'être décisif sur coups de pied arrêtés pour un top match. Mon 5, qui a un an de moins, doit utiliser beaucoup plus son pied gauche, surtout qu'il joue central gauche : pas facile pour lui, à travailler pour performer plus. Mon numéro 6 a couru dans tous les sens, il a perdu de l'utilité en fin de match. Mon numéro 7, côté droit, match intéressant, il touchait beaucoup de ballons mais manque de déséquilibre, son apport offensif n'était pas à la hauteur. Mon 8 : box to box, profondeur, capacité à prendre l'espace, à jouer court et long — super match. Comme mon numéro 10 à côté, puisque je joue en 4-3-3. Mon ailier gauche : match assez terne, offensivement compliqué — ce n'était pas mes trois attaquants de base. On a créé quelques situations, en vain : défaite 2-0. Et mon numéro 9 : peu de ballons touchés, profil plutôt faux 9, il n'a pas assez combiné avec les autres. En passant, ce sont deux joueurs U13 : bon match, bonne première impression dans le 11, à travailler encore. »

### 4.2 Roster (Liste des joueurs)
| N° | Prénom | Poste | Note |
|----|--------|-------|------|
| 1  | Lucas | Gardien | ← héros (rapport complet) |
| 2  | Rayan | Latéral droit | match référence |
| 3  | Enzo | Latéral gauche | sorti sur blessure |
| 4  | Noah | Défenseur central | |
| 5  | Gabriel | Défenseur central gauche | joue un an au-dessus |
| 6  | Malik | Milieu | |
| 7  | Théo | Ailier droit | |
| 8  | Ibrahim | Milieu box-to-box | super match |
| 9  | Adam | Attaquant (faux 9) | U13, 1er match dans le 11 |
| 10 | Mattéo | Milieu | super match |
| 11 | Younes | Ailier gauche | U13, 1er match dans le 11 |

### 4.3 Rapport héros complet — Lucas · Gardien (#1)
- **Résumé du match** : Bon match dans les buts. Ta sortie aérienne a été maîtrisée et ton jeu au pied est propre techniquement. La marge est dans le **choix** de la relance : bien voir la meilleure solution ballon au pied.
- **Tes points forts** : jeu aérien (sortie maîtrisée) · qualité technique au pied.
- **Tes axes prioritaires de progression** : le choix dans la relance. Techniquement tu as les qualités ; le prochain pas, c'est de choisir la solution la plus juste pour l'équipe.
- **Ton objectif pour le prochain match** : sur chaque relance, prends l'info (regarde tes options) avant de recevoir, puis choisis la solution la plus utile.
- **Ce que Seedinho remarque** : ton coach est clair — la technique est là (aérien + pied). Le palier suivant n'est pas technique, il est dans la lecture du jeu : voir vite la bonne option. C'est ce qui fait un gardien moderne, et ça se travaille avec de la répétition et de la vidéo.
- **Plan de progression** :
  - *Exercice individuel* : relances avec options mobiles — un partenaire ouvre 2-3 solutions, tu prends l'info et choisis la meilleure en moins de 2 secondes.
  - *Conseil entraînement* : demande à jouer au pied avec des appuis qui bougent, pour t'habituer à décider vite.
  - *Analyse vidéo personnalisée — Bientôt disponible* (déclenchée par : choix de relance). Revoir tes relances à froid pour repérer les meilleures options.

### 4.4 Les 10 autres rapports (dérivés fidèlement)
Format identique (Résumé · Points forts · Axe · Objectif · Ce que Seedinho remarque · Plan).

**Rayan — #2 Latéral droit.** Résumé : match référence, technique irréprochable, tu as éliminé en un-contre-un (2-3 fois) et déséquilibré leur défense. Points forts : aisance technique · capacité à éliminer en 1v1 · apport offensif qui casse l'organisation adverse. Axe : aucun signalé → faire de ce match ta référence. Objectif : rejouer à ce niveau et transformer un débordement en occasion. Seedinho remarque : « match référence », c'est le mot le plus fort d'un débrief — c'est désormais ton standard. Plan : exercice (répéter 1v1 + centres) · conseil (enchaîner débordement + dernière passe). *Aucun spécialiste.*

**Enzo — #3 Latéral gauche (sorti sur blessure).** Résumé : sorti tôt sur un coup, match écourté, difficile à évaluer — le plus important, c'est ton rétablissement. Points forts : *non renseignés par le coach → ne rien inventer ; centrer sur le retour.* Axe : revenir en forme, sans précipitation. Objectif : soigner, récupérer, revenir à 100 %. Seedinho remarque : un match écourté sur blessure n'efface rien et ne juge rien ; on te retrouve au prochain. Plan : *Gestion de la récupération — Bientôt disponible* (déclenchée par : blessure). Pas d'exercice intense conseillé tant que tu n'es pas remis.

**Noah — #4 Défenseur central.** Résumé : à l'aise, correct au pied en jeu court comme long, tu t'es libéré de ton marquage plusieurs fois. Points forts : aisance technique (court + long) · capacité à se démarquer. Axe : devenir décisif sur les coups de pied arrêtés pour passer au top match. Objectif : peser sur un coup de pied arrêté (bien attaquer le ballon de la tête). Seedinho remarque : ton coach te situe déjà très haut ; le petit plus, c'est l'impact sur les phases arrêtées — un détail qui fait gagner des matchs. Plan : exercice (attaques de tête sur CPA, timing de course) · conseil (déplacements sur corner). *Aucun spécialiste.*

**Gabriel — #5 Central gauche (un an au-dessus).** Résumé : tu joues un an au-dessus de ton âge, à un poste (central gauche) qui exige le pied gauche — un vrai défi que tu relèves. Points forts : jouer au-dessus de ton âge (niveau, maturité) · tu tiens ton poste dans un contexte exigeant. Axe : développer ton pied gauche, essentiel à ton poste. Objectif : utiliser ton pied gauche à chaque relance courte possible. Seedinho remarque : jouer un an au-dessus, à un poste qui demande ton pied le moins fort, c'est difficile — et tu le fais. Le pied gauche, c'est ta prochaine arme. Plan : exercice (répétitions pied gauche : passes, contrôles) · conseil (t'imposer le pied gauche en conservation). *Aucun spécialiste.*

**Malik — #6 Milieu.** Résumé : tu as beaucoup couru et donné de l'énergie ; à trop courir partout, tu as perdu en utilité en fin de match. Points forts : volume de course · générosité dans l'effort. Axe : canaliser cette énergie — être plus juste dans le placement pour rester utile jusqu'au bout (courir mieux, pas seulement plus). Objectif : rester dans ta zone et choisir tes courses, pour peser tout le match. Seedinho remarque : ton énergie est une qualité rare ; le prochain pas, ce n'est pas courir moins mais courir juste — bien te placer pour que chaque effort serve l'équipe. Plan : exercice (jeux de position pour lire les espaces) · conseil (prises de position à l'entraînement) · *Analyse vidéo — Bientôt disponible* (déclenchée par : placement/lecture). *(Pas de prépa physique : la cause décrite est le placement, pas la fatigue.)*

**Théo — #7 Ailier droit.** Résumé : match intéressant, beaucoup de ballons touchés ; il a manqué le déséquilibre — l'action qui fait la différence — pour que ton apport offensif pèse vraiment. Points forts : implication · présence dans le jeu (beaucoup de ballons touchés). Axe : créer du déséquilibre — oser le un-contre-un, provoquer, éliminer. Objectif : tenter le 1v1 dès que tu reçois dans ton couloir. Seedinho remarque : toucher beaucoup de ballons, c'est déjà être bien placé et disponible ; le déclic, c'est d'oser faire la différence balle au pied. Plan : exercice (1v1, feintes, débordements) · conseil (situations de 1v1 face au latéral). *Aucun spécialiste.*

**Ibrahim — #8 Milieu box-to-box.** Résumé : gros match complet — box to box, tu prends la profondeur, tu occupes l'espace, tu joues court et long. Points forts : milieu complet (des deux surfaces) · prise d'espace et de profondeur · palette technique. Axe : aucun signalé → confirmer ce niveau. Objectif : rejouer un match aussi complet et ajouter une action décisive (passe clé ou frappe). Seedinho remarque : ton coach t'a décrit comme un milieu complet — un vrai compliment ; ce match est ta référence. Plan : exercice (arrivées dans la surface pour être décisif) · conseil (finition des courses box-to-box). *Aucun spécialiste.*

**Adam — #9 Faux 9 (U13, 1er match dans le 11).** Résumé : peu de ballons touchés. Sur ton profil de faux 9 — un attaquant qui décroche pour créer le jeu — il a manqué des combinaisons avec tes partenaires ; et c'était ton premier match dans le 11, un an au-dessus. Points forts : profil de faux 9 (intelligence de jeu, tu décroches) · première apparition dans le 11 à un an au-dessus. Axe : te connecter davantage — combiner, jouer en remise, te rendre disponible entre les lignes. Objectif : chercher 3-4 combinaisons avec tes milieux (une-deux, remises). Seedinho remarque : premier match dans le 11, un an au-dessus, dans un rôle qui vit des associations — c'est normal que ça demande de l'adaptation ; ton profil est précieux, la clé c'est de te lier au jeu des partenaires. Plan : exercice (jeu en remise dos au but, une-deux) · conseil (combinaisons entre les lignes). *Aucun spécialiste.*

**Mattéo — #10 Milieu.** Résumé : gros match, à l'image d'un milieu complet dans ce 4-3-3. Points forts : performance de haut niveau au milieu · complémentarité dans l'entrejeu. Axe : aucun signalé → confirmer. Objectif : reproduire ce niveau et ajouter une touche décisive. Seedinho remarque : ton coach t'associe aux meilleurs du match — garde ce standard. Plan : exercice (impact dans le dernier tiers) · conseil (arrivées décisives). *Aucun spécialiste. (Le coach en dit peu : garder le rapport court et honnête.)*

**Younes — #11 Ailier gauche (U13, 1er match dans le 11) — CAS SENSIBLE.** Résumé : match plus discret offensivement, dans une attaque qui n'était pas le trio habituel, pour ta première apparition dans le 11 (un an au-dessus) ; l'équipe a créé quelques situations sans conclure. Points forts : *le coach ne signale aucune qualité individuelle → NE RIEN INVENTER.* Remplacer par un bloc « Le contexte de ton match » : avoir tenu ta place dans le 11 pour un premier match, un an au-dessus, dans un rôle inhabituel. Axe : t'impliquer davantage dans le jeu offensif, prendre tes repères. Objectif : réclamer le ballon et tenter une action offensive dès que possible. Seedinho remarque : un premier match dans le 11, un an au-dessus, avec une attaque remaniée, c'est un contexte difficile — ce match ne te définit pas ; on regarde vers le prochain, chaque ballon touché sera un pas. Plan : exercice (appels et prises de balle côté couloir) · conseil (situations offensives simples pour prendre des repères). *Aucun spécialiste.*

### 4.5 Progression saison — Lucas #1 (données simulées pour la démo)
Indicateur « Décision de relance » (0-100), 5 derniers matchs : `J5 55 · J6 60 · J7 58 · J8 64 · J9 66`.
- Résumé : progression régulière de la qualité de tes relances. Le prochain palier est la vitesse de décision.
- Objectif atteint : ✓ « Gagner en propreté technique au pied ».
- Axe récurrent : « Choix de la relance » (revient sur 3 des 5 derniers matchs).
> Pour les autres joueurs, la courbe est optionnelle ; si affichée, garder l'axe cohérent avec l'observation réelle et libeller « données simulées ».

### 4.6 Traitement des cas sensibles (règle « jamais juger / jamais inventer »)
- **Enzo #3 (blessé)** et **Younes #11 (terne, aucune qualité citée)** : ne jamais inventer un point fort. Protéger le joueur par le **contexte** (blessure / premier match, un an au-dessus, rôle inhabituel) et une **projection positive** dans « Ce que Seedinho remarque » et l'objectif. Le bloc « Points forts » devient « Le contexte de ton match » plutôt que rester vide ou inventer.
- Partout : traduire le vocabulaire technique pour 13-19 ans (« déséquilibre » → faire la différence en un-contre-un ; « faux 9 » → attaquant qui décroche pour créer le jeu ; « box to box » → milieu complet qui joue des deux surfaces ; « sortir du marquage » → se libérer de son adversaire).

---

## 5. LOGIQUE CONDITIONNELLE DES SPÉCIALISTES

Un spécialiste n'apparaît **que** si une observation le justifie. Sinon il n'existe pas dans l'écran.

| Observation générique | Spécialiste | Présent dans CETTE transcription ? |
|---|---|---|
| Choix/décision, placement, lecture du jeu | Analyse vidéo personnalisée | **Oui** — Lucas #1, Malik #6 |
| Blessure, coup, sorti tôt | Gestion de la récupération | **Oui** — Enzo #3 |
| Fatigue physique, « plus de jambes » | Préparateur physique | **Non → n'apparaît pas** |
| Confiance, doute, crispation | Préparateur mental | **Non → n'apparaît pas** |
| Sommeil, alimentation | Récupération / Nutrition | **Non → n'apparaît pas** |

Bilan sur les 11 rapports : **Analyse vidéo ×2, Récupération ×1, rien d'autre.** Preuve visible que le plan est personnalisé, pas un catalogue. Ne force aucun spécialiste absent des observations.

---

## 6. ARCHITECTURE & LIVRABLE

- **Web app** mobile-first, cliquable de bout en bout (parcours §3 navigable).
- **Tout simulé** : pas d'OpenAI, pas de Supabase, audio placeholder, données en dur (§4).
- **Structure prête à brancher plus tard** :
  - Données (roster, rapports, transcription, courbes) isolées dans des objets/JSON dédiés, comme venant d'une API.
  - Logique de déclenchement des spécialistes (§5) dans une fonction pure `getRecommendations(observations)`.
  - UI en composants réutilisables (§2).
- Priorité absolue au rendu du **Rapport individuel** : c'est là que se joue la crédibilité.

---

## 7. LE TEST DE RÉUSSITE

Un coach doit se dire : « Enfin un outil qui transforme mes observations en un véritable accompagnement individuel. »
Un joueur : « J'ai enfin l'impression d'avoir un staff qui m'aide à progresser après chaque match. »
Si un écran ressemble à un PDF, à une IA marketing ou à une boutique → à refaire.

---

### ✅ BRIEF COMPLET
Match : **AS Charte 0 – 2 Pontois FC** · vert officiel `#02562d` · logos (vert sur blanc / blanc sur vert) · 11 prénoms · contenu dérivé de la vraie transcription. Rien à ajouter — prêt à coller dans Claude Design.
