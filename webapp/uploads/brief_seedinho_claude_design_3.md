# BRIEF CLAUDE DESIGN — SEEDINHO (MVP web app) — v3

> À coller dans Claude Design **avec les fichiers joints** (audio, photos joueurs, planche d'écussons, logos SVG). Web app **mobile-first cliquable**. Contenu football dérivé fidèlement de la vraie transcription (§4.1).

---

## 0. PITCH & AUDIENCE
Une web app qui transforme le débrief oral d'un coach amateur en **suivi individuel de niveau centre de formation**. Seedinho n'est pas « une IA » : c'est le **staff numérique du coach**.
**La démo sert à convaincre un COACH d'adopter l'appli.** Donc :
- **Écrans démo (Landing, Démonstration) → s'adressent au COACH** (« tu / ton équipe », angle gain de temps + meilleur suivi).
- **Rapports & Mon évolution → s'adressent au JOUEUR** (« tu », ton jeune et motivant).

---

## 1. RÈGLES NON-NÉGOCIABLES
1. **Jamais un PDF** → app premium (Apple / Nike / Hudl / Strava).
2. **Jamais inventer.** Tout vient des mots du coach (§4).
3. **« Tes points forts » n'apparaît QUE si le coach a cité du positif** (audit §4.4 : 5 joueurs n'en ont pas). Ne jamais fabriquer une qualité.
4. **Jamais « points faibles »** → « axe de progression », positif.
5. **Jamais juger.** Cas sensibles protégés par « Le contexte de ton match » (§4.7).
6. **Ton adapté à l'audience** (§0) : coach sur la démo, joueur (jeune, parlant) sur les rapports.
7. **Peu de rubriques.** Rapport lu en < 1 min (structure §3.4).
8. **Objectif toujours suivi de « À valider avec ton coach ».**
9. **Écussons des 2 équipes visibles** partout où un match est cité.
10. **Jamais une marketplace** : « Le staff Seedinho recommande… » / « Pour aller plus loin… ». Jamais « Acheter / Débloquer ».
11. **Une seule main suffit** (cibles ≥ 44px).

---

## 2. DESIGN SYSTEM

### Couleurs (vert officiel Seedinho)
```
--green-700 #02562d (primaire) · --green-500 #0A6E3B (hover) · --green-50 #E9F3ED (tint)
--ink #0E1B14 · --muted #6B7280 · --line #EEF0F2 · --surface #F7F8FA · --white #FFFFFF
```
Texte sur vert = blanc. Vert = accent uniquement.

### Fondations & typo
Mobile first 390 px, fond blanc, air, grille 8 pt, gouttières 20-24 px. **Inter** : Display 32/700 · H1 24/700 · H2 18/600 · Body 15-16 · Caption 13/500 uppercase. Gros chiffres tracking serré.

### Formes & anim
Cartes 20-24 px · boutons pilule · ombres douces `0 8px 24px rgba(2,86,45,.06)` · icônes monoline (Lucide), pas d'emoji. Micro-anims : fade+translate-up au scroll, count-up sur les chiffres, onde audio animée, transitions fluides.

### Assets (fournis, §6)
Photos joueurs (portrait rond) · écussons clubs (pastille ronde) · logo Seedinho **vert** sur blanc / **blanc** sur vert · audio `.m4a` (2 min 21).

### Composants
`AppHeader` · `TeamHero` · `PlayerCard` · `MatchTag` (2 écussons + score) · `ReportSection` · `ObjectiveCard` (+ badge « À valider ») · `SpecialistCard` (badge « Bientôt disponible ») · `EvolutionMatchRow` (écusson + résumé + bouton « Voir le rapport détaillé ») · `AudioPlayer` + `Waveform` · `StepChecklist` · `AdvantageStrip` (mini-anim de stats).

---

## 3. LES ÉCRANS
Parcours : Landing → Démonstration (finit par une mini-anim d'avantages) → Liste joueurs → Rapport individuel → Mon évolution → Rejoindre Seedinho (CTA coach).

### 3.1 Landing
- Logo Seedinho (vert) en haut.
- **Visuel d'équipe** : grille des portraits + **écusson du club au centre**. ⚠️ **Griser / désaturer et assombrir légèrement les portraits**, et mettre **l'écusson en couleur, au premier plan avec une ombre**, pour qu'il ressorte nettement (actuellement il se noie dans les photos).
- **Slogan (exact)** : « Donner à chaque joueur amateur un suivi digne d'un centre de formation. »
- Une ligne de sous-texte : « Le staff numérique qui transforme le débrief du coach en suivi pour chaque joueur. »
- CTA : « Découvrir la démonstration ».
- Footer **MatchTag** : [écusson] AS Montreuil FC 0 – 2 AC Rivière [écusson].

### 3.2 Démonstration (parle AU COACH)
- **Titre (change)** : « Après le match, une note vocale de 2 minutes. »
- **Sous-titre** : « Fais ton débrief à voix haute, joueur par joueur — Seedinho écrit un rapport pour chacun. »
- **MatchTag** (2 écussons) sous le titre.
- **AudioPlayer** : lit le vrai `.m4a` (2 min 21), play central + **onde animée**. Libellé « Note vocale · Coach ». ⚠️ **BUG à corriger : à la fin de la lecture, remettre le curseur à 0:00** (écouter l'event `ended`), réinitialiser le bouton play et la progression de l'onde, pour que le coach puisse relancer.
- **Transcription** : ⚠️ **revenir à l'ancien affichage en UN SEUL BLOC** (une carte grise « Transcription », texte continu, scrollable) — **PAS de bulles de messages séparées avec avatars** (format actuel à retirer). Le texte complet (§4.1) s'affiche en une fois dans le bloc.
- **StepChecklist** qui se coche : ✓ Transcription de la note vocale · ✓ Identification des joueurs · ✓ Analyse des observations · ✓ Génération des rapports.
- **Mini-animation d'avantages (remplace l'ancienne page stats)** — `AdvantageStrip`, apparaît en count-up juste après la checklist :
  - « **30 min à la main → 2 min** avec Seedinho »
  - « **28 min gagnées** par match »
  - « **≈ 2 h 20 gagnées** sur tes 5 derniers matchs »
  - « **9 joueurs sur 11** ont déjà bossé leur axe de progression » (mention « données simulées »)
- ⚠️ **Icône du bloc stats** : utiliser une icône qui évoque les statistiques (graphique en barres / courbe montante, ex. Lucide `bar-chart-2` ou `trending-up`), **PAS l'icône caméra/vidéo** (à retirer).
- **CTA final (change)** : bouton direct « **Voir les rapports** » → Liste joueurs.

### 3.3 Liste des joueurs
- Titre = **MatchTag** : AS Montreuil FC 0 – 2 AC Rivière · 4-3-3.
- **PlayerCard** : photo réelle (ronde), n° (style maillot), prénom, poste, « Rapport prêt ». **Lucas (#1, gardien)** en tête (rapport héros).

### 3.4 Rapport individuel — s'adresse au JOUEUR (structure allégée)
Ordre :
0. **Bandeau repère (fin, discret)** tout en haut : **« Ce que reçoivent vos joueurs »** — signale au coach qu'il prévisualise l'expérience côté joueur (le tutoiement qui suit s'adresse au joueur).
1. **En-tête** (bandeau vert) : **photo** + prénom + n° + poste + **MatchTag (2 écussons + score + 4-3-3)**.
2. **Résumé du match** — 2-3 phrases, ton jeune.
3. **Tes points forts** — *seulement si le coach a cité du positif* (sinon supprimer la carte, cf. §4.7).
4. **Ton axe de progression** — positif, souvent un seul.
5. **Ton objectif — prochain match** (carte verte) + badge **« À valider avec ton coach »**.
6. **Pour aller plus loin** — *uniquement* la/les **SpecialistCard** conditionnelle(s) (§5). ⚠️ **La carte « Ton exercice conseillé » est SUPPRIMÉE.** Du coup cette section n'apparaît que pour Lucas, Enzo et Malik ; pour les 8 autres, le rapport s'arrête à l'objectif.
7. Boutons : « **Voir mon évolution** » (renommé, ex « Voir ma saison ») · « Voir un autre joueur ».
8. **CTA coach (discret, en pied)** : « **Essayer avec mon équipe** » → écran Rejoindre Seedinho (§3.6).

### 3.5 Mon évolution (ex « Ma saison ») — s'adresse au JOUEUR
- Titre : **« Mon évolution »**.
- En-tête joueur (photo, prénom) + « données simulées ».
- ⚠️ **Supprimer la carte « Progression saison » (la courbe).**
- **Liste des matchs** (`EvolutionMatchRow`) : chaque ligne = **écusson adversaire** + nom + journée + résultat + **résumé 1 ligne** + bouton **« Voir le rapport détaillé »** (ramène au rapport du match — peut être non fonctionnel en démo). 5 matchs (§4.6).
- **Bilan** : 2 phrases sur la progression constatée + **Objectifs atteints** (coches) + **Axe récurrent**.
- **CTA coach en pied** : « **Essayer avec mon équipe** » → §3.6.

### 3.6 Rejoindre Seedinho (CTA / captation coach) — s'adresse au COACH
Écran final de conversion, atteint depuis les CTA « Essayer avec mon équipe » (rapport & évolution).
- Titre : « Envie de suivre ton équipe comme ça ? »
- Sous-texte : « Laisse-nous tes infos, on te recontacte pour démarrer avec ton club. »
- **Formulaire** (3 champs) : **Nom du club** · **Catégorie** (ex. U13, U15, U17…) · **Division** (ex. Départemental 2, Régional 1…).
- **Email affiché** : « Vos infos arrivent directement à **seedinho.contact@gmail.com** ».
- **Envoi réel des soumissions (remplace `mailto:`, qui ne marchait pas)** : le formulaire POST vers un service **formulaire → email** de type **Web3Forms** (`https://api.web3forms.com/submit`) avec un champ caché `access_key` (à obtenir gratuitement sur web3forms.com avec l'adresse seedinho.contact@gmail.com). Chaque soumission (club / catégorie / division) arrive alors par email dans la boîte Seedinho. Champs `name` : `club`, `categorie`, `division` + `subject` = « Nouveau club — {club} ». *(Formspree/Getform équivalents.)*
  - ⚠️ Mettre la clé en placeholder `[ACCESS_KEY_WEB3FORMS]` dans le code (le porteur du projet la colle après inscription).
  - ⚠️ Fonctionne sur la version **déployée/exportée** ; dans l'aperçu Claude Design (iframe), l'appel réseau peut être bloqué — tester sur la version publiée.
- **Bouton « Envoyer mes infos »** → soumet le formulaire (POST). Après succès : message de confirmation (« Merci, on revient vers vous vite ! »). Gérer un état d'erreur simple si l'appel échoue.

---

## 4. CONTENU FOURNI (tel quel)

### 4.1 Match & transcription
**AS Montreuil FC 0 – 2 AC Rivière · 4-3-3 · défaite.** U13 débutant dans le 11 : Adam #9, Younes #11 ; Gabriel #5 joue un an au-dessus.
> « Mon numéro 1, le gardien, a fait un bon match : sortie aérienne intéressante, jeu au pied aussi. Là où il aurait pu faire mieux : le choix, l'utilisation du ballon au pied. Mon 2 : match référence, techniquement pas de souci, il a déséquilibré le bloc après 2-3 un-contre-un. Mon 3 est sorti très vite sur un coup, match compliqué à juger. Mon 4, central, à l'aise, correct au pied court et long, il s'est sorti du marquage plusieurs fois ; à lui d'être décisif sur coups de pied arrêtés. Mon 5, un an de moins, doit beaucoup plus utiliser son pied gauche, surtout à central gauche. Mon 6 a couru dans tous les sens, il a perdu de l'utilité en fin de match. Mon 7, côté droit, match intéressant, beaucoup de ballons touchés mais manque de déséquilibre. Mon 8 : box to box, profondeur, prend l'espace, joue court et long — super match. Comme mon 10 à côté, en 4-3-3. Mon ailier gauche : match assez terne offensivement — ce n'était pas mes trois attaquants de base. Défaite 2-0. Et mon 9 : peu de ballons, profil faux 9, pas assez combiné. En passant, deux joueurs U13 : bonne première impression dans le 11. »

### 4.2 Roster + photos
Associer les photos **par PRÉNOM** (ignorer les numéros imprimés sur la planche, décalés). **Portrait à générer : Enzo (#3).**
| N° | Prénom | Poste | Photo |
|----|--------|-------|-------|
| 1 | **Lucas** | Gardien (**héros**) | oui |
| 2 | Rayan | Latéral droit | oui |
| 3 | Enzo | Latéral gauche (blessé) | oui |
| 4 | Noah | Défenseur central | oui |
| 5 | Gabriel | DC gauche (un an au-dessus) | oui |
| 6 | Malik | Milieu | oui |
| 7 | Théo | Ailier droit | oui |
| 8 | Ibrahim | Milieu box-to-box | oui |
| 9 | Adam | Attaquant faux 9 (U13) | oui |
| 10 | Mattéo | Milieu | oui |
| 11 | Younes | Ailier gauche (U13) | oui |

### 4.3 Rapport héros — Lucas · Gardien #1
- **Résumé** : Bon match dans les cages. Ta sortie dans les airs était bien gérée et t'es propre au pied. Le truc à bosser : le choix quand tu as le ballon — bien voir la meilleure solution avant de la jouer.
- **Tes points forts** : Ton jeu aérien — sortie bien maîtrisée. · Ta technique au pied — c'est propre.
- **Ton axe** : Le choix de la relance. Techniquement t'as tout ; maintenant, choisir la bonne option, celle qui aide vraiment l'équipe.
- **Objectif — prochain match** : Sur chaque relance, regarde tes options avant de recevoir, puis joue la solution la plus sûre. *(À valider avec ton coach.)*
- **Pour aller plus loin** : **Analyse vidéo perso (Bientôt)** — revoir tes relances au calme pour repérer, action par action, les meilleures options.

### 4.4 Les 10 autres rapports (audit des points forts + spécialistes)
*(Plus d'« exercice conseillé ». « Pour aller plus loin » = spécialiste seulement, s'il est déclenché.)*

**Rayan #2 (Latéral droit).** Résumé : Gros match, sûrement le meilleur du groupe. Techniquement nickel, et t'as fait mal avec tes un-contre-un : 2-3 fois t'as cassé leur défense. Points forts ✅ : ta technique · tes un-contre-un qui déséquilibrent. Axe : — (match référence). Objectif : Rejoue à ce niveau et transforme un débordement en occasion. *(À valider avec ton coach.)* — *Pas de « Pour aller plus loin ».*

**Enzo #3 (Latéral gauche, blessé).** ❌ pas de points forts. **« Le contexte de ton match »** : Sorti tôt sur un coup, ton match a été trop court pour être jugé — le plus important, c'est que tu reviennes bien. Objectif : Soigne-toi, récupère, reviens à 100 %. *(À valider avec ton coach.)* **Pour aller plus loin : Récupération (Bientôt)** — on t'accompagne pour un retour en douceur.

**Noah #4 (Défenseur central).** Résumé : Match solide derrière. À l'aise, propre au pied (court comme long), et tu t'es libéré de ton marquage plusieurs fois. Points forts ✅ : ton aisance technique court et long · tu sais te démarquer. Axe : Être décisif sur les coups de pied arrêtés — ce qui te ferait passer au-dessus. Objectif : Sur le prochain corner, va chercher le ballon de la tête. *(À valider avec ton coach.)* — *Pas de « Pour aller plus loin ».*

**Gabriel #5 (DC gauche, un an au-dessus).** ❌ pas de points forts. **« Le contexte de ton match »** : Tu joues un an au-dessus de ton âge, à un poste qui demande le pied gauche — pas simple, et tu tiens le coup. Axe : Ton pied gauche. À ton poste c'est essentiel : plus tu l'utilises, plus tu montes. Objectif : À chaque relance courte possible, joue du gauche. *(À valider avec ton coach.)* — *Pas de « Pour aller plus loin ».*

**Malik #6 (Milieu).** ❌ pas de points forts. Résumé : T'as mis beaucoup d'énergie et beaucoup couru. Le souci : à courir partout, t'as perdu en impact sur la fin. Axe : Cours juste, pas juste beaucoup — place-toi bien pour que chaque course serve à quelque chose. Objectif : Reste dans ta zone et choisis tes courses pour peser tout le match. *(À valider avec ton coach.)* **Pour aller plus loin : Analyse vidéo (Bientôt)** — repère tes courses inutiles.

**Théo #7 (Ailier droit).** Résumé : Bon match, t'as beaucoup touché le ballon. Ce qu'il a manqué : le petit truc qui fait la diff' devant — provoquer, éliminer ton défenseur. Points forts ✅ (un seul, réellement cité) : t'étais bien dans le jeu, beaucoup de ballons touchés. Axe : Créer du déséquilibre — ose le un-contre-un, provoque, élimine. Objectif : Dès que tu reçois dans ton couloir, tente le un-contre-un. *(À valider avec ton coach.)* — *Pas de « Pour aller plus loin ».*

**Ibrahim #8 (Milieu box-to-box).** Résumé : Gros match du début à la fin. Box to box, t'as pris la profondeur, occupé les espaces, joué court et long — un vrai milieu complet. Points forts ✅ : milieu complet des deux surfaces · tu prends l'espace et la profondeur · ta palette technique. Axe : — . Objectif : Rejoue un match aussi complet et ajoute une action décisive. *(À valider avec ton coach.)* — *Pas de « Pour aller plus loin ».*

**Adam #9 (Faux 9, U13, 1er match).** **« Le contexte de ton match »** : Premier match dans le 11, un an au-dessus, en faux 9 (l'attaquant qui décroche pour créer le jeu). Peu de ballons, pas encore assez de combinaisons — normal, c'est un rôle qui demande de l'adaptation. Point fort ✅ (cité par le coach) : bonne première impression pour un premier match dans le 11. Axe : Connecte-toi plus au jeu — combine, joue en remise, rends-toi dispo entre les lignes. Objectif : Cherche 3-4 combinaisons avec tes milieux. *(À valider avec ton coach.)* — *Pas de « Pour aller plus loin ».*

**Mattéo #10 (Milieu).** Résumé : Gros match aussi pour toi au milieu, dans la lignée de l'équipe dans ce 4-3-3. Points forts ✅ : une perf de haut niveau au milieu (« super match » dixit le coach). Axe : — . Objectif : Reproduis ce niveau et ajoute une touche décisive. *(À valider avec ton coach.)* — *Pas de « Pour aller plus loin ».* (Rapport court.)

**Younes #11 (Ailier gauche, U13, 1er match).** **« Le contexte de ton match »** : Match plus discret devant, dans une attaque qui n'était pas le trio habituel, pour ton premier match dans le 11 (un an au-dessus). Contexte difficile — ce match ne te définit pas. Point fort ✅ (cité par le coach) : bonne première impression pour un premier match dans le 11. Axe : Implique-toi plus dans le jeu offensif, prends tes repères. Objectif : Réclame le ballon et tente une action offensive dès que tu peux. *(À valider avec ton coach.)* — *Pas de « Pour aller plus loin ».*

### 4.5 Chiffres des avantages (mini-anim §3.2) — CORRIGÉS
- Rédiger à la main les rapports de tous les joueurs d'un match ≈ **30 min**. Avec Seedinho ≈ **2 min** (la note vocale).
- Gain = **28 min par match**. Sur **5 matchs** : 5 × 28 = **140 min ≈ 2 h 20** cumulées.
- Stat d'impact (simulée) : **9 joueurs sur 11 ont travaillé leur axe de progression** avant le prochain entraînement (variantes possibles : « 11 rapports, 0 joueur oublié » ; « chaque joueur suivi, pas seulement les meilleurs »).
*(Tous chiffres simulés, cohérents.)*

### 4.6 Évolution simulée (écran « Mon évolution ») — clubs de la planche
Club du coach : **AS Montreuil FC**. Matchs (avec écussons), exemple Lucas :
| Journée | Adversaire | Résultat | Résumé 1 ligne | 
|--------|------------|----------|----------------|
| J5 | FC Vallières | V 3-1 | Match propre, relances maîtrisées. |
| J6 | US Lorient | N 2-2 | Bon jeu au pied, un choix à revoir. |
| J7 | Étoile Sportive | V 1-0 | Ta meilleure sortie de la saison. |
| J8 | FC Horizon | D 0-1 | Peu sollicité, propre sur tes appuis. |
| J9 | AC Rivière | D 0-2 | Bon match, à travailler le choix de relance. |
Chaque ligne a un bouton **« Voir le rapport détaillé »**.
Bilan Lucas : Tu progresses sur la propreté de tes relances ; le prochain palier, c'est décider plus vite. Objectif atteint ✓ « gagner en propreté au pied ». Axe récurrent : le choix de la relance.
> Autres joueurs : même structure, résumés cohérents avec leur axe réel. Clubs dispo pour varier : Sporting des Bois, FC Saint-Martin, USP de la Plaine, Entente du Val.

### 4.7 Ton & cas sensibles
- **Ton joueur (rapports)** : tutoiement, phrases courtes, mots vivants (« la diff' », « le déclic », « t'as tout pour »). Bannir le soutenu (« néanmoins », « apport offensif »). Pro et bienveillant, jamais moqueur.
- **Ton coach (démo)** : direct, valorisant, orienté gain de temps + meilleur suivi.
- **Traductions** : déséquilibre → faire la diff' en 1v1 ; faux 9 → attaquant qui décroche ; box to box → milieu complet des deux surfaces ; sortir du marquage → se libérer de son défenseur.
- **Jamais inventer un point fort** : Enzo, Gabriel, Malik → pas de carte points forts. Adam & Younes → uniquement « bonne première impression » (réellement dit).

---

## 5. LOGIQUE CONDITIONNELLE DES SPÉCIALISTES
| Observation présente | Spécialiste | Joueurs |
|---|---|---|
| Choix / placement / lecture du jeu | Analyse vidéo | **Lucas #1, Malik #6** |
| Blessure / sorti sur un coup | Récupération | **Enzo #3** |
| Fatigue physique · confiance · sommeil · nutrition | Physique / Mental / Nutrition | **Aucun → n'apparaissent pas** |
Bilan : Analyse vidéo ×2, Récupération ×1. Ne force aucun spécialiste absent des mots du coach.

---

## 6. ASSETS & USAGE
- `AUDIO-...m4a` (2 min 21) → Démonstration (lecture réelle ; transcription en **bloc unique** ; **reset à 0:00 en fin de lecture**).
- `Photos_joueurs.png` → portraits, **associer par prénom** (ignorer les numéros imprimés, décalés). Enzo est désormais fourni.
- `logo_clubs.png` → écussons : **AS Montreuil FC** vs **AC Rivière** (ce match) + FC Vallières, US Lorient, Étoile Sportive, FC Horizon (saison).
- Logo Seedinho : `vert`/`full_vert` sur blanc, `blanc` sur vert.

---

## 7. ARCHITECTURE & LIVRABLE
Web app mobile-first cliquable de bout en bout. Tout simulé (données en dur). Isoler données + `getRecommendations(observations)` (§5) pour brancher plus tard. Priorité de rendu : **Rapport individuel** puis **Mon évolution**.

---

## 8. TEST DE RÉUSSITE
Coach : « Enfin un outil qui transforme mes observations en accompagnement individuel. » — Joueur : « J'ai un staff qui m'aide à progresser après chaque match. » Un écran qui fait PDF / IA-marketing / boutique → à refaire.

---

## 9. SUGGESTION OPTIONNELLE (à activer ou ignorer)
- **Bouton mock « Envoyer à mon joueur »** sur le rapport : montre au coach comment il diffuse les rapports et rappelle que **c'est lui qui envoie** (le coach reste l'expert). *(Distinct de l'écran §3.6 qui, lui, sert à capter le coach.)*
*(Les anciens points « CTA de conversion » et « bandeau ce que reçoivent vos joueurs » sont désormais intégrés au brief : §3.6 et §3.4.)*
