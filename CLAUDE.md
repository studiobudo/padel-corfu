# CLAUDE.md - Padel Academy Corfu

## Ce que l'IA ne doit PAS faire

- Ne JAMAIS reecrire le fichier entier. Modifier uniquement la section concernee.
- Ne pas inventer de fonctionnalites non demandees.
- Ne pas supprimer de code existant qui fonctionne sans demande explicite.
- Ne pas changer les couleurs, polices ou identite visuelle sans validation.
- Ne pas ajouter de dependances externes ou de CDN sans accord prealable.
- Ne pas hardcoder de donnees (horaires, prix, terrains) - tout doit etre configurable dans l objet CONFIG.
- Ne pas repondre en anglais - toujours communiquer en francais.

## Conventions avant de coder

### Stack et structure
- Single-file HTML : tout le HTML, CSS et JS dans un seul fichier.
- Vanilla JS uniquement - pas de framework, pas de jQuery.
- CSS : variables CSS pour les couleurs et espacements.
- Responsive mobile-first.

### Identite visuelle
- Couleur principale : #1B4332 (vert fonce)
- Couleur accent : #F5C518 (jaune dore)
- Font : system-ui ou sans-serif standard

### Multilingue
- 3 langues : FR / EN / GR
- Toutes les chaines de texte dans un objet TRANSLATIONS en debut de fichier.
- Langue par defaut : FR.

### Qualite de code
- Commenter chaque section avec des balises claires.
- Nommer les fonctions de maniere explicite (handleBookingSubmit, renderCalendar).
- Toujours tester la logique modifiee avant de valider.

### Process
- Avant de coder : expliquer brievement l approche en 2-3 lignes.
- Apres modification : lister les changements effectues.
- En cas de doute sur une spec : demander plutot que deviner.

## Fichiers a lire avant de coder

| Fichier      | Contenu                                    | Quand le lire                                      |
|--------------|--------------------------------------------|----------------------------------------------------|
| index.html   | App complete (single-file)                 | TOUJOURS - lire la section concernee par la tache  |
| SPECS.md     | Specifications fonctionnelles detaillees   | Avant une nouvelle fonctionnalite                  |
| CHANGELOG.md | Historique des modifications               | Avant de reprendre apres un /clear                 |