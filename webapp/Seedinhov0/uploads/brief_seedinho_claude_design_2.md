# BRIEF CLAUDE DESIGN — SEEDINHO (MVP web app) — v2

> À coller dans Claude Design, **avec les fichiers joints** (audio, photos joueurs, planche d'écussons, logos SVG). Contenu football dérivé fidèlement de la vraie transcription (§4.1). Web app **mobile-first cliquable**.

---

## 0. PITCH
Une web app qui transforme le débrief oral d'un coach amateur en **suivi individuel de niveau centre de formation**. Seedinho n'est pas « une IA » : c'est le **staff numérique du coach**. Le coach reste l'expert ; le produit organise, traduit et prolonge son travail.

---

## 1. RÈGLES NON-NÉGOCIABLES
1. **Jamais un PDF** → app premium (Apple / Nike / Hudl / Strava).
2. **Jamais inventer.** Tout vient des mots du coach (§4).
3. **« Tes points forts » n'apparaît QUE si le coach a clairement cité du positif.** Sinon, pas de section (voir l'audit §4.4 : 5 joueurs n'ont pas de points forts). Ne jamais fabriquer une qualité pour « équilibrer ».
4. **Jamais « points faibles »** → « axes de progression », positif.
5. **Jamais juger.** Cas sensibles (blessé, match terne) protégés par le contexte (§4.7).
6. **Ton jeune et parlant**, pas soutenu (§4.7). On tutoie, phrases courtes, énergie, bienveillance.
7. **Peu de rubriques.** Un rapport se lit en < 1 min. Structure allégée imposée (§3.5).
8. **Objectif toujours suivi de « À valider avec ton coach ».**
9. **Écussons des 2 équipes visibles** partout où un match est cité (landing, démo, rapport, saison) → prouve qu'on parle du bon match.
10. **Jamais une marketplace** : « Le staff Seedinho recommande… » / « Pour aller plus loin… ». Jamais « Acheter / Débloquer / Premium ».
11. **Une seule main suffit** (cibles ≥ 44px, actions dans le pouce).

---

## 2. DESIGN SYSTEM

### Fondations
Mobile first, viewport 390 px. Fond blanc dominant, beaucoup d'air. Grille 8 pt. Gouttières 20-24 px.

### Couleurs (vert officiel Seedinho)
```
--green-700  #02562d   /* vert Seedinho OFFICIEL (logo) — primaire */
--green-500  #0A6E3B   /* hover / états */
--green-50   #E9F3ED   /* tint : badges, fonds doux, fond de courbe */
--ink #0E1B14 · --muted #6B7280 · --line #EEF0F2 · --surface #F7F8FA · --white #FFFFFF
```
Texte sur `--green-700` = blanc. Vert = accent uniquement (boutons, valeurs clés, coches, courbe). Aucune autre couleur de marque.

### Typo
**Inter**. Display 32/700 · H1 24/700 · H2 18/600 · Body 15-16 · Caption 13/500 uppercase (labels de section). Gros chiffres tracking serré (stats, n°).

### Formes
Cartes 20-24 px · boutons pilule · ombres douces `0 8px 24px rgba(2,86,45,.06)` · icônes monoline (Lucide). Pas d'emoji.

### Micro-animations
Cartes en fade+translate-up au scroll · count-up sur les stats · onde audio animée · transcription qui s'écrit en synchro audio · transitions d'écran fluides. Discret.

### Médias & assets (fournis, voir §6)
- **Photos joueurs** : portrait rond dans PlayerCard et en-tête de rapport.
- **Écussons clubs** : petite pastille ronde/écusson à côté du nom d'équipe.
- **Logo Seedinho** : version **verte** (`vert`, `full_vert`) sur fond blanc ; version **blanche** (`blanc`) sur surface verte.
- **Audio** : fichier `.m4a` (2 min 21) lu dans l'écran Démonstration.

### Composants
`AppHeader` · `TeamHero` (photo équipe + écusson) · `PlayerCard` · `MatchTag` (2 écussons + score) · `StatTile` · `ReportSection` · `ObjectiveCard` (+ badge « À valider ») · `SpecialistCard` (badge « Bientôt disponible ») · `SeasonMatchRow` (écusson + résumé) · `SeasonChart` · `AudioPlayer` + `Waveform` · `StepChecklist`.

---

## 3. LES ÉCRANS
Parcours : Landing → Démonstration → **Valeur coach (stats)** → Liste joueurs → Rapport individuel → **Ma saison**.

### 3.1 Landing — ALLÉGÉE (moins de texte, plus d'air)
Refonte demandée : le pavé de texte actuel est trop lourd.
- Logo Seedinho (vert) en haut, discret.
- **Visuel d'équipe** au centre : la photo de groupe des 11 joueurs (ou une grille de leurs portraits), avec **l'écusson du club posé au centre/dessus**. C'est l'élément dominant, pas le texte.
- **Slogan (garder, exact)** : « Donner à chaque joueur amateur un suivi digne d'un centre de formation. »
- **Une seule ligne** de sous-texte (supprimer le paragraphe) : « Le staff numérique qui transforme le débrief du coach en suivi pour chaque joueur. »
- CTA : « Découvrir la démonstration ».
- Footer = **MatchTag** : [écusson] **AS Montreuil FC** 0 – 2 **AC Rivière** [écusson].

### 3.2 Démonstration — avec le vrai audio
- **AudioPlayer** lisant le fichier `.m4a` réel (2 min 21). Play central + **onde animée**.
- **MatchTag** (les 2 écussons) affiché près du titre pour situer le match.
- **Transcription synchronisée** : le texte (§4.1) défile/apparaît au fil de la lecture. Si un transcript horodaté est fourni, caler dessus ; sinon, dérouler proportionnellement à `currentTime`/`timeupdate` de l'audio.
- **StepChecklist** qui se coche au fil de la lecture : ✓ Transcription · ✓ Identification des joueurs · ✓ Analyse des observations · ✓ Génération des rapports.
- CTA fin : « Voir ce que ça change pour toi » → écran Valeur coach.

### 3.3 Valeur coach (NOUVEL écran intermédiaire)
Objectif : montrer le gain concret pour le coach, juste après la démo.
- Titre : « En 2 min 21, Seedinho a fait le travail d'un staff. »
- **StatTiles** (count-up), données §4.5 :
  - **13** rapports générés (11 titulaires + 2 remplaçants)
  - **~12 min** économisées par rapport (vs rédaction à la main)
  - **≈ 2 h 36** de rédaction évitée sur ce seul match
  - **1** note vocale → **13** suivis individuels
- Ligne saison (discrète) : « Cette saison : 60+ rapports, ~13 h gagnées. »
- Ton : fierté sobre, pas commercial. CTA : « Voir les rapports de l'équipe ».

### 3.4 Liste des joueurs
- Titre = **MatchTag** : AS Montreuil FC 0 – 2 AC Rivière · 4-3-3.
- **PlayerCard** : **photo réelle** du joueur (ronde), n° (style maillot), prénom, poste, « Rapport prêt ». Mettre **Lucas (#1, gardien)** en tête → rapport héros.

### 3.5 Rapport individuel — STRUCTURE ALLÉGÉE
Ordre imposé (moins de rubriques qu'avant) :
1. **En-tête** (bandeau vert) : **photo** du joueur + prénom + n° + poste + **MatchTag (2 écussons + score + 4-3-3)**. 1-2 StatPills max, dérivées des mots du coach.
2. **Résumé du match** — 2-3 phrases, ton jeune, fidèle.
3. **Tes points forts** — *seulement si le coach a clairement cité du positif* (sinon supprimer la carte).
4. **Ton axe de progression** — positif, souvent un seul axe.
5. **Ton objectif — prochain match** (carte verte) + **badge « À valider avec ton coach »**.
6. **Pour aller plus loin** : **1 exercice** conseillé + spécialiste(s) conditionnel(s) (§5). *(On a SUPPRIMÉ les cartes « Ce que Seedinho remarque » et « Conseil pour le prochain entraînement ».)*
7. Liens : « Voir ma saison » · « Voir un autre joueur ».

> Pour les joueurs sans points forts (blessé / match discret / U13 débutant), remplacer la carte « Tes points forts » par une carte **« Le contexte de ton match »** (§4.7). Jamais de vide, jamais d'invention.

### 3.6 Ma saison (NOUVEL écran / demandé)
Rapport global simulé, par joueur.
- En-tête joueur (photo, prénom).
- **SeasonChart** : courbe de l'indicateur du joueur (données simulées, §4.6).
- **Liste des matchs** (SeasonMatchRow) : chaque ligne = **écusson adversaire** + nom + journée + résultat + **résumé 1 ligne**. (5 matchs, §4.6.)
- **Résumé de saison** : 2 phrases sur la progression constatée + **Objectifs atteints** (coches) + **Axe récurrent**.
- Tout est libellé « données simulées ».

---

## 4. CONTENU FOURNI (à utiliser tel quel)

### 4.1 Match & transcription
**Match : AS Montreuil FC 0 – 2 AC Rivière · 4-3-3 · défaite.** Deux joueurs **U13** débutent dans le 11 (Adam #9, Younes #11) ; Gabriel #5 joue un an au-dessus.
Transcription (texte affiché, synchronisé à l'audio) :
> « Mon numéro 1, le gardien, a fait un bon match : sortie aérienne intéressante, jeu au pied aussi. Là où il aurait pu faire mieux : le choix, l'utilisation du ballon au pied. Mon 2 : match référence, techniquement pas de souci, il a déséquilibré le bloc après 2-3 un-contre-un. Mon 3 est sorti très vite sur un coup, match compliqué à juger. Mon 4, central, à l'aise, correct au pied court et long, il s'est sorti du marquage plusieurs fois ; à lui d'être décisif sur coups de pied arrêtés. Mon 5, un an de moins, doit beaucoup plus utiliser son pied gauche, surtout à central gauche. Mon 6 a couru dans tous les sens, il a perdu de l'utilité en fin de match. Mon 7, côté droit, match intéressant, beaucoup de ballons touchés mais manque de déséquilibre. Mon 8 : box to box, profondeur, prend l'espace, joue court et long — super match. Comme mon 10 à côté, en 4-3-3. Mon ailier gauche : match assez terne offensivement — ce n'était pas mes trois attaquants de base. Défaite 2-0. Et mon 9 : peu de ballons, profil faux 9, pas assez combiné. En passant, deux joueurs U13 : bonne première impression dans le 11. »

### 4.2 Roster + association des photos
Roster canonique (fait autorité). **Associer les photos par PRÉNOM, en ignorant les numéros/postes imprimés sur la planche** (ils sont décalés). **Portrait manquant à générer : Enzo (#3).**
| N° | Prénom | Poste | Photo fournie ? |
|----|--------|-------|-----------------|
| 1 | **Lucas** | Gardien (**héros**) | oui |
| 2 | Rayan | Latéral droit | oui |
| 3 | Enzo | Latéral gauche (blessé) | **non → à générer** |
| 4 | Noah | Défenseur central | oui |
| 5 | Gabriel | Défenseur central gauche (un an au-dessus) | oui |
| 6 | Malik | Milieu | oui |
| 7 | Théo | Ailier droit | oui |
| 8 | Ibrahim | Milieu box-to-box | oui |
| 9 | Adam | Attaquant faux 9 (U13) | oui |
| 10 | Mattéo | Milieu | oui |
| 11 | Younes | Ailier gauche (U13) | oui |

### 4.3 Rapport héros — Lucas · Gardien #1 (ton jeune, structure allégée)
- **Résumé** : Bon match dans les cages. Ta sortie dans les airs était bien gérée et t'es propre au pied. Le truc à bosser, c'est le choix quand tu as le ballon : bien voir la meilleure solution avant de la jouer.
- **Tes points forts** : Ton jeu aérien — une sortie bien maîtrisée. · Ta technique au pied — c'est propre.
- **Ton axe** : Le choix de la relance. Techniquement t'as tout ; maintenant c'est de choisir la bonne option, celle qui aide vraiment l'équipe.
- **Objectif — prochain match** : Sur chaque relance, regarde tes options avant de recevoir, puis joue la solution la plus sûre. *(À valider avec ton coach.)*
- **Pour aller plus loin** : Exercice — relances avec un partenaire qui t'ouvre 2-3 solutions : prends l'info et choisis la meilleure en moins de 2 secondes. · **Analyse vidéo perso (Bientôt)** — revoir tes relances au calme pour repérer les meilleures options.

### 4.4 Les 10 autres rapports (audit des points forts inclus)
Rappel règle 3 : « Tes points forts » **seulement si le coach a cité du positif**.

**Rayan #2 (Latéral droit).** Résumé : Gros match, sûrement le meilleur du groupe. Techniquement nickel, et t'as fait mal avec tes un-contre-un : 2-3 fois t'as cassé leur défense. Points forts ✅ : ta technique, rien à dire · tes un-contre-un qui déséquilibrent. Axe : — (match référence). Objectif : Rejoue à ce niveau et transforme un débordement en occasion. *(À valider avec ton coach.)* Plan : Exercice — enchaîne débordement + dernière passe/centre. *Aucun spécialiste.*

**Enzo #3 (Latéral gauche, blessé).** ❌ pas de points forts. Carte **« Le contexte de ton match »** : Sorti tôt sur un coup, ton match a été trop court pour être jugé — le plus important, c'est que tu reviennes bien. Objectif : Soigne-toi, récupère, reviens à 100 %. *(À valider avec ton coach.)* Plan : **Récupération (Bientôt)** — on t'accompagne pour un retour en douceur. Pas d'exo intense.

**Noah #4 (Défenseur central).** Résumé : Match solide derrière. T'es à l'aise, propre au pied (court comme long), et tu t'es libéré de ton marquage plusieurs fois. Points forts ✅ : ton aisance technique, court et long · tu sais te démarquer. Axe : Être décisif sur les coups de pied arrêtés — c'est ce qui te ferait passer au-dessus. Objectif : Sur le prochain corner, va chercher le ballon de la tête. *(À valider avec ton coach.)* Plan : Exercice — attaque de tête sur CPA, bosse ton timing de course. *Aucun spécialiste.*

**Gabriel #5 (Central gauche, un an au-dessus).** ❌ pas de points forts (le coach n'a pas cité de qualité). Carte **« Le contexte de ton match »** : Tu joues un an au-dessus de ton âge, à un poste qui demande le pied gauche — pas simple, et tu tiens le coup. Axe : Ton pied gauche. À ton poste c'est essentiel : plus tu l'utilises, plus tu montes. Objectif : À chaque relance courte possible, joue du gauche. *(À valider avec ton coach.)* Plan : Exercice — répète passes et contrôles du pied gauche. *Aucun spécialiste.*

**Malik #6 (Milieu).** ❌ pas de points forts (le coach a décrit sans praiser). Résumé : T'as mis beaucoup d'énergie et beaucoup couru. Le souci : à courir partout, t'as perdu en impact sur la fin. Axe : Cours juste, pas juste beaucoup — place-toi bien pour que chaque course serve à quelque chose. Objectif : Reste dans ta zone et choisis tes courses pour peser tout le match. *(À valider avec ton coach.)* Plan : Exercice — jeux de position pour lire les espaces. · **Analyse vidéo (Bientôt)** — repère tes courses inutiles. 

**Théo #7 (Ailier droit).** Résumé : Bon match, t'as beaucoup touché le ballon. Ce qu'il a manqué, c'est le petit truc qui fait la diff' devant : provoquer, éliminer ton défenseur. Points forts ✅ (un seul, réellement cité) : t'étais bien dans le jeu, beaucoup de ballons touchés. Axe : Créer du déséquilibre — ose le un-contre-un, provoque, élimine. Objectif : Dès que tu reçois dans ton couloir, tente le un-contre-un. *(À valider avec ton coach.)* Plan : Exercice — des un-contre-un face à un défenseur, feintes et débordements. *Aucun spécialiste.*

**Ibrahim #8 (Milieu box-to-box).** Résumé : Gros match du début à la fin. Box to box, t'as pris la profondeur, occupé les espaces, joué court et long — un vrai milieu complet. Points forts ✅ : milieu complet, des deux surfaces · tu prends l'espace et la profondeur · ta palette technique. Axe : — . Objectif : Rejoue un match aussi complet et ajoute une action décisive (passe clé ou frappe). *(À valider avec ton coach.)* Plan : Exercice — travaille tes arrivées dans la surface. *Aucun spécialiste.*

**Adam #9 (Faux 9, U13, 1er match).** Carte **« Le contexte de ton match »** : Premier match dans le 11, un an au-dessus, en faux 9 (l'attaquant qui décroche pour créer le jeu). Peu de ballons et pas encore assez de combinaisons — normal, c'est un rôle qui demande de l'adaptation. Point fort ✅ (cité par le coach) : bonne première impression pour un premier match dans le 11. Axe : Connecte-toi plus au jeu — combine, joue en remise, rends-toi dispo entre les lignes. Objectif : Cherche 3-4 combinaisons avec tes milieux (une-deux, remises). *(À valider avec ton coach.)* Plan : Exercice — jeu en remise dos au but, une-deux. *Aucun spécialiste.*

**Mattéo #10 (Milieu).** Résumé : Gros match aussi pour toi au milieu, dans la lignée de l'équipe dans ce 4-3-3. Points forts ✅ : une perf de haut niveau au milieu (« super match » dixit le coach). Axe : — . Objectif : Reproduis ce niveau et ajoute une touche décisive. *(À valider avec ton coach.)* Plan : Exercice — tes arrivées décisives dans le dernier tiers. *Aucun spécialiste.* (Rapport court : le coach en a peu dit.)

**Younes #11 (Ailier gauche, U13, 1er match).** Carte **« Le contexte de ton match »** : Match plus discret devant, dans une attaque qui n'était pas le trio habituel, et pour ton premier match dans le 11 (un an au-dessus). Contexte difficile — ce match ne te définit pas. Point fort ✅ (cité par le coach) : bonne première impression pour un premier match dans le 11. Axe : Implique-toi plus dans le jeu offensif, prends tes repères. Objectif : Réclame le ballon et tente une action offensive dès que tu peux. *(À valider avec ton coach.)* Plan : Exercice — appels et prises de balle dans ton couloir. *Aucun spécialiste.*

### 4.5 Stats écran « Valeur coach »
13 rapports (11 titulaires + 2 remplaçants) · ~12 min économisées / rapport · ≈ 2 h 36 évitées sur ce match · 1 note vocale (2 min 21) → 13 suivis · Saison : 60+ rapports, ~13 h gagnées. *(Chiffres simulés, cohérents.)*

### 4.6 Saison simulée (écran « Ma saison ») — clubs de la planche d'écussons
Club du coach : **AS Montreuil FC**. Adversaires de la saison (avec écussons) :
| Journée | Adversaire (écusson) | Résultat | Résumé 1 ligne (ex. Lucas) |
|--------|----------------------|----------|-----------------------------|
| J5 | FC Vallières | V 3-1 | Match propre, relances maîtrisées. |
| J6 | US Lorient | N 2-2 | Bon jeu au pied, un choix à revoir. |
| J7 | Étoile Sportive | V 1-0 | Ta meilleure sortie de la saison. |
| J8 | FC Horizon | D 0-1 | Peu sollicité, propre sur tes appuis. |
| J9 | AC Rivière | D 0-2 | Bon match, à travailler le choix de relance. |
Courbe Lucas « Décision de relance » (0-100) : J5 55 · J6 60 · J7 58 · J8 64 · J9 66.
Résumé saison : Tu progresses sur la propreté de tes relances ; le prochain palier, c'est décider plus vite. Objectif atteint ✓ « gagner en propreté au pied ». Axe récurrent : le choix de la relance.
> Pour les autres joueurs : même structure, résumés cohérents avec leur axe réel, écussons des mêmes adversaires. Clubs restants dispo pour varier : Sporting des Bois, FC Saint-Martin, USP de la Plaine, Entente du Val, FC Vallières.

### 4.7 Ton & cas sensibles
- **Ton jeune** : tutoiement, phrases courtes, mots simples et vivants (« la diff' », « le déclic », « t'as tout pour », « continue comme ça »). Bannir le soutenu (« néanmoins », « apport offensif », « de surcroît »). Rester pro et bienveillant, jamais gamin ni moqueur.
- **Traductions** : déséquilibre → faire la diff' en un-contre-un ; faux 9 → attaquant qui décroche pour créer le jeu ; box to box → milieu complet qui joue des deux surfaces ; sortir du marquage → se libérer de son défenseur.
- **Jamais inventer un point fort.** Enzo, Gabriel, Malik : aucune carte points forts. Adam & Younes : uniquement le positif réellement dit par le coach (« bonne première impression »). Protéger par « Le contexte de ton match ».

---

## 5. LOGIQUE CONDITIONNELLE DES SPÉCIALISTES
N'apparaît que si l'observation le justifie.
| Observation présente | Spécialiste | Joueurs concernés |
|---|---|---|
| Choix / placement / lecture du jeu | Analyse vidéo | **Lucas #1, Malik #6** |
| Blessure / sorti sur un coup | Récupération | **Enzo #3** |
| Fatigue physique · confiance · sommeil · nutrition | Physique / Mental / Nutrition | **Aucun → n'apparaissent pas** |
Bilan : Analyse vidéo ×2, Récupération ×1. Rien d'autre. Ne force aucun spécialiste absent des mots du coach.

---

## 6. ASSETS FOURNIS & USAGE
- `AUDIO-...m4a` (2 min 21) → écran Démonstration (lecture réelle + synchro transcription).
- `Photos_joueurs.png` → portraits ; **associer par prénom** (ignorer numéros imprimés) ; **générer le portrait d'Enzo**.
- `logo_clubs.png` → écussons : **AS Montreuil FC** (coach) vs **AC Rivière** (ce match) ; + FC Vallières, US Lorient, Étoile Sportive, FC Horizon pour la saison.
- Logo Seedinho : `vert`/`full_vert` sur blanc, `blanc` sur vert.

---

## 7. ARCHITECTURE & LIVRABLE
Web app mobile-first cliquable de bout en bout. Tout simulé (données en dur, pas d'OpenAI/Supabase). Isoler données (roster, rapports, saison, stats) et la fonction `getRecommendations(observations)` (§5) pour brancher une vraie analyse plus tard. Priorité de rendu : **Rapport individuel** puis **Ma saison**.

---

## 8. TEST DE RÉUSSITE
Coach : « Enfin un outil qui transforme mes observations en accompagnement individuel. » — Joueur : « J'ai un staff qui m'aide à progresser après chaque match. » Si un écran fait PDF, IA-marketing ou boutique → à refaire.
