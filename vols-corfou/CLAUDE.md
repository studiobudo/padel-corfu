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
