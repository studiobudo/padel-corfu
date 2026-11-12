# CLAUDE.md — Projet « Vols directs vers Corfou 2026 » (Kerkyra Work & Play)

Contexte de travail pour toute session Claude/Cowork intervenant sur ce dossier.
Langue de travail : **français**. Owner : Michaël BOUDOT (Kerkyra Work & Play, DMC/agence réceptive à Corfou).

## Objet du projet
Guide des **vols directs vers Corfou (aéroport CFU, Ioannis Kapodistrias)** pour la **saison 2026**, au départ de **France, Belgique, Luxembourg et Suisse**. Deux livrables : un document Word (guide par ville) et un mini-site web (outil de recherche de vol + capture email + CTA devis).

## Livrables (dans ce dossier `Communication/`)
- **`Vols_Corfou_2026_par_ville.docx`** — couverture + sommaire par pays, puis 1 page par ville (15 villes). Chaque page : tableau Aller/Retour (jours + créneau), estimation de prix, saison. Logo Kerkyra en couverture.
- **`Corfou-Vols-2026.html`** — page web autonome (1 seul fichier). Ouvrable en local ou hébergeable.

## Charte graphique (À RESPECTER)
- **Teal / bleu** : `#028a95` (primaire), `#045a63` (foncé), `#033f47` (très foncé).
- **Doré** : `#e0b128` (primaire), `#c2971a` (foncé).
- **Crème / fond** : `#F6F1E7`.
- **Logo** : `logo.svg` / `logo.png` (source : `KERKYRA_logo_bleu_dore.svg`, teal `#028a95` + doré `#e0b128`). Inline dans le site (en-tête + pop-up), en image sur la couverture du .docx.
- **E-mail de contact unique** : `hello@kerkyra.fr` (pop-up, formulaire devis, footer).

## Fonctionnalités du site `Corfou-Vols-2026.html`
- **3 langues** : Français / English / Ελληνικά (sélecteur FR/EN/ΕΛ en haut à droite). Tout est piloté par le dictionnaire `T` + attributs `data-i18n` ; les données (jours, créneaux, saison) sont générées par langue.
- **Outil de recherche** : filtre **par ville** (avec option « Paris (CDG + Orly) » combinée) et **par jour**. Chaque résultat affiche 2 blocs : « Ville → Corfou » (Aller) puis « Corfou → Ville » (Retour).
- **Carte géographique réelle** (SVG) : contours France métropolitaine / Belgique / Luxembourg / Suisse (issus de GeoJSON `johan/world.geo.json`, projection équirectangulaire corrigée en longitude), + **encart contour de Corfou** en bas à droite. Points de ville cliquables = filtrent l'outil.
- **Pop-up email** (gate) : mailto vers `hello@kerkyra.fr`. **Astuce interne** : une croix « × » blanche sur fond blanc en haut à droite du pop-up (invisible au public, visible au survol) permet de fermer/passer le pop-up sans saisir d'email — pour usage interne équipe.
- **CTA + formulaire devis** : « Recevoir mon devis Corfou » → formulaire (nom, email, période, nb personnes, projet) → mailto `hello@kerkyra.fr` (devis hébergement + activités).

## Données vols (IMPORTANTES — statut)
- **Indicatives, saison 2026.** Compagnies couvertes : Transavia, easyJet, Ryanair, Volotea (+ Aegean sur Nantes, Brussels Airlines/TUI fly, Luxair, SWISS, Edelweiss).
- 15 villes : Paris-Orly, Paris-CDG, Marseille, Lyon, Nantes, Bordeaux, Toulouse, Bâle-Mulhouse, Strasbourg, Lille (France) ; Bruxelles-Charleroi, Bruxelles-Zaventem (Belgique) ; Luxembourg ; Genève, Zurich (Suisse).
- **Fiabilité** : compagnies, fréquences hebdo et fins de saison = solides (source aviability.com / sites compagnies / flightsfrom / cfu-airport.gr). **Jours nommés et horaires exacts = partiellement estimés** (les sources agrégées n'exposent pas le détail jour par jour) → toujours étiqueter « indicatif », à confirmer sur les moteurs des compagnies. Prix = fourchettes « à partir de », très volatiles.
- Contour de Corfou : transcription fidèle (30 points) de la ligne de côte réelle (la source Grèce libre n'incluait pas Corfou).

## Comment régénérer / éditer (environnement Cowork)
- Scripts dans le dossier de travail temporaire (outputs) : `build_villes.js` (docx, via `npm i docx`), `build_site.js`/heredoc + `patch_map.py` (site + carte), `map_assets.json` (géométrie carte).
- Word : Node + lib `docx`, validé via le skill `docx` (`scripts/office/validate.py`). Couleurs = constantes `NAVY/TEAL/GOLD` en haut de `build_villes.js`.
- Site : données dans les tableaux JS `FLIGHTS` (out/ret = slots + horaire), `MAP` (marqueurs), dictionnaire `T` (i18n). Carte = `map_assets.json` injecté par `patch_map.py`.
- Rendu/preview local : `cairosvg` (SVG→PNG). Pas de navigateur headless dispo dans le VM → vérifier le visuel via captures utilisateur si besoin.

## Canva (source du guide historique)
- Design « Vols 2026 » : ID `DAHOmERQOvs` — shortlink `https://canva.link/vilif1dbgyzeol5`. Site publié 2025 : `https://pro.kerkyra.fr/vols-corfou-2025`.
- Couverture déjà passée en 2026 + menu limité aux villes. **Les tableaux d'horaires par ville sont des IMAGES dans Canva** (non éditables via le connecteur) → à refaire manuellement. Les pages villes étrangères 2025 (Bruxelles Charleroi, Bruxelles, Genève, Zurich) restent dans le design : suppression de page **non supportée** par le connecteur → à faire à la main.

## En attente / à faire
- **Design System Kerkyra (Claude Design)** : projet `https://claude.ai/design/p/019e2e91-0c01-7cfa-87be-28adc3586a0f`. Le connecteur `claude_design` (`https://api.anthropic.com/v1/design/mcp`, auth `/design-login`) **n'est pas connecté** dans Cowork → impossible d'importer les tokens exacts. Charte actuelle = approximée depuis les couleurs du logo. À autoriser côté réglages connecteurs claude.ai, puis rouvrir une session et demander l'import.
- Option : version photo-réaliste de la couverture (avion + église de Corfou) à la place de l'illustration SVG.
- Option : reporter la vraie carte dans le .docx (page d'intro).

## Règles de style avec l'owner
Direct, créatif, efficace. Aller droit au but, proposer des options concrètes. Toujours signaler honnêtement le statut « indicatif » des données et les limites techniques (connecteurs, images Canva, etc.).

## Mise à jour saison 2027 (relevé du 12/11/2026)
- Le site affiche désormais la **saison 2027**. Chaque entrée de `FLIGHTS` porte un statut `st` : `ok` (programme 2027 publié), `part` (partiel ou une seule source), `np` (non publié). `ref26:true` signale que les jours/horaires affichés sont ceux de 2026, faute de mieux.
- Champs de saison : `deb` (premier vol 2027) et `fin` (dernier vol, absent si non publié). Notes par liaison dans `note` (FR/EN/EL).
- **Sources du relevé** : flightconnections.com, partir.com, aeroroutes.com (France, pages lues) ; extraits de moteur de recherche pour Belgique, Luxembourg et Suisse. **Aucun site de compagnie n'a été lu** : tout reste à confirmer.
- Points ouverts : fins de saison CDG, Lyon, Bâle, Marseille, Toulouse ; jours 2027 de Charleroi, Bruxelles, Luxembourg, Genève ; maintien de TUI fly Bruxelles–Corfou. Nouveauté : Condor Zurich–Corfou dès le 2 juillet 2027.
- Le pop-up d'entrée ne collecte plus d'e-mail (CTA Instagram @kerkyra_workplay). Le Hero est une scène SVG/CSS animée (classes `hs-*`).
- Bloc devis : carrousel d'activités (`#car`, fonction `initActivityCarousel`), 4 photos `img/act-*.jpg` reprises du blog kerkyra.fr (CDN Webflow), recadrées en 16:10 et optimisées. La mention « programme 2027 incomplet » est la clé i18n `updateNote`, affichée sous le texte d'intro (classe `.notice`) : mettre sa date à jour à chaque relevé.
- Carte : affichée sans cadre sur le fond (`viewBox="88 8 708 552"`). La Corse est visible et étiquetée ; Corfou est un encart à droite (hors échelle) dont le contour vient de Natural Earth 10m (paquet npm `world-atlas`, 98 points, projection équirectangulaire corrigée à 39,6° N), avec le point de l'aéroport CFU.

## Page « Destination Corfou 2027 » (`destination-2027.html`, ajout du 12/11/2026)
- **Rôle** : page de présentation commerciale, montrée en rendez-vous sur téléphone. Non indexée (`noindex`). URL une fois en ligne : `vols.kerkyra.fr/destination-2027` (ajouter `?lang=en` ou `?lang=gr` pour forcer la langue).
- **Fichier unique** HTML/CSS/JS, vanilla, aucun CDN. Ressources dans `destination/img/` (WebP) et `destination/fonts/` (The Seasons, Mistrully, Playfair Display, Poppins, en local).
- **Données** dans l'objet `CONFIG` (durée de vol, températures, villes, activités, formats de groupe, chiffres DMC, contact) ; **textes** dans `TRANSLATIONS` (`fr` / `en` / `gr`), appliqués par `applyLanguage()` via `data-i18n`. Variables de texte : `{flight}`, `{price}`, `{year}`.
- **Sections** : hero animé → manifeste (mots qui s'allument au scroll) → infographies (2 h 45, météo, 13 villes, repères) → carrousel incontournables → carrousel extras → formats de groupe (cartes empilées) + cas réel → DMC → FAQ → contact.
- **Effets** : `initReveals` (apparitions), `updateScrollEffects` (hero, arc de vol, soleil, parallaxe, ligne du déroulé), `initActivityCarousel` (scroll-snap). Tout est neutralisé avec `prefers-reduced-motion`.
- **Police The Seasons = version démo** : pas d'accents, et les glyphes `4 - + / & ! ( )` affichent un tampon « DEMO ». Un `unicode-range` limite donc la police aux glyphes sûrs (le reste bascule sur Playfair Display) et les chiffres d'infographie utilisent `--font-num` (Playfair). Avec la version complète de la police : retirer le `unicode-range` et pointer `--font-num` sur `--font-display`.
- **Sources des contenus** : kerkyra.fr (pages séminaires, incentive, activités, FAQ, équipe) et blog (formats de séminaire, team building, vol Paris-Corfou, Corfou en octobre), lus le 12/11/2026. Photos : CDN Webflow de kerkyra.fr et photothèque du design system.
- **À confirmer par l'owner** : températures mensuelles (`CONFIG.weather`, maximales moyennes indicatives, non issues du site) ; durée de vol (le site affiche 2 h 30, 2 h 40 ou 2 h 45 selon les pages, 2 h 45 retenu) ; prix incentive « à partir de 1 500 € » (repris du site) ; photos de faible définition (`extra-rando`, `extra-moto`) à remplacer si des originaux existent.
