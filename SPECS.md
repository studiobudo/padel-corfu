# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Projet : 

Build a complete padel court booking web application for "Padel Academy Corfu" 
as a single self-contained HTML file (index.html) with all CSS and JavaScript inline.

---

## BRAND IDENTITY

- Primary color: #1B4332 (deep forest green, from logo background)
- Accent color: #F5C518 (golden yellow, from logo text)
- Secondary accent: #2D6A4F (mid green)
- Text light: #FFFFFF
- Text dark: #0A1F14
- Background: #0D2B1A (very dark green)
- Card bg: #1B4332
- Border/subtle: #2D6A4F

Fonts (load from Google Fonts):
- Display: "Oswald" (bold headings, sport energy)
- Body: "DM Sans" (clean, modern readability)

Logo text style: "PADEL" in white bold, "ACADEMY" in #F5C518 bold, "CORFU" in white bold
Aesthetic: Premium Mediterranean sports resort — dark green dominance, gold accents, 
clean sport energy. Think luxury hotel meets padel club.

---

## APP STRUCTURE (single-page, tab navigation)

### 1. HEADER (fixed top)
- Logo circle icon (padel rackets) + "PADEL ACADEMY CORFU" text
- Navigation tabs: Réserver | Mes Réservations | Terrains | Tarifs
- Language toggle: FR / EN / GR
- Mobile hamburger menu

---

### 2. PAGE: RÉSERVER (default view)

**Step 1 — Choose date & time**
- Calendar widget (full month view, current month)
  - Highlight: today, selected day, unavailable slots (grayed)
  - Available days have a subtle gold dot indicator
- Time slot grid (06:00 → 22:00, every 90 minutes):
  - Slots displayed as cards: time range, availability badge (Disponible / Complet / Dernières places)
  - Color: available = green, last slots = gold, full = dark gray strikethrough

**Step 2 — Choose court**
- 4 courts to choose from:
  - Court 1 — Panoramic (sea view) — Premium
  - Court 2 — Garden (olive trees) — Standard  
  - Court 3 — Indoor (covered) — Standard
  - Court 4 — Night (floodlit) — Standard
- Each court card shows: name, photo placeholder (gradient with icon), features chips, price/slot

**Step 3 — Player details**
- Number of players: 2 or 4 (toggle)
- Player 1 (booker): First name, Last name, Email, Phone
- Players 2-4 (optional): First name, Email
- Racket rental toggle per player (+5€/player)
- Ball set option (+3€)
- Special requests (textarea)

**Step 4 — Summary & Payment**
- Recap card: date, time, court, players, extras
- Total price calculation (live update)
- Payment method: Credit card (Stripe placeholder form), Cash on arrival
- Terms checkbox
- CTA button: "Confirmer la réservation" (gold, full width)
- On confirm: animated success screen with booking reference number

---

### 3. PAGE: MES RÉSERVATIONS

- Filter tabs: À venir | Passées | Annulées
- Booking cards showing:
  - Date, time, court name, players, total paid
  - Status badge (Confirmé / En attente / Annulé)
  - Actions: Modifier (up to 24h before) | Annuler | Télécharger reçu
- Empty state with CTA to book

Use localStorage to persist bookings across sessions.

---

### 4. PAGE: TERRAINS

Grid of 4 court cards (2x2 on desktop, 1 col mobile):
- Large image placeholder (gradient + SVG court diagram)
- Court name + type badge
- Features list: lighting, surface type, dimensions (10x20m), covered/outdoor
- Availability mini-calendar (next 7 days, dot indicators)
- "Réserver ce terrain" button

---

### 5. PAGE: TARIFS

Clean pricing table:

| Formule | Durée | Prix | Inclus |
|---|---|---|---|
| Match | 90 min | 24€ | Court + 1 set balles |
| Training | 90 min | 20€ | Court seul |
| Académie Jeunes | 60 min | 12€ | Encadrement inclus |
| Cours Collectifs | 90 min | 15€/pers | Max 4 joueurs |
| Location raquette | — | 5€ | Par raquette |

Season pricing note: High season (June-September) +20%

Membership cards:
- Pass 10h — 180€ (save 15%)
- Pass Mensuel illimité — 280€/mois
- Pass Famille — 320€/mois (up to 4 people)

---

## TECHNICAL SPECIFICATIONS

### Architecture
- Single file: index.html
- All CSS in <style> tag (no external stylesheets except Google Fonts CDN)
- All JS in <script> tag (vanilla JS only, no frameworks)
- No backend required — all state in memory + localStorage

### Responsive Design
- Mobile-first approach
- Breakpoints: 480px, 768px, 1024px, 1280px
- Touch-friendly: min tap target 44px
- Smooth scroll, no horizontal overflow

### CSS Architecture
- CSS custom properties (variables) for all colors, spacing, border-radius
- BEM-inspired naming
- Smooth transitions: 0.2s ease on all interactive elements
- Glassmorphism cards: background rgba(27,67,50,0.8), backdrop-filter blur(12px), border 1px solid rgba(245,197,24,0.15)

### Animations & Micro-interactions
- Page transitions: fade + slight translateY(8px) on tab switch
- Calendar days: scale(1.05) + gold glow on hover
- Booking steps: horizontal progress bar with gold fill
- Success screen: checkmark SVG stroke animation + confetti burst (CSS only)
- Court cards: subtle lift (translateY -4px) + gold border glow on hover
- Loading spinner: rotating padel racket icon (SVG)

### Calendar Logic (JS)
- Generate current month + 2 next months
- Mark past days as unavailable
- Mock availability: randomly mark 30% of slots as full, 15% as "last slots"
- Date selection updates time slot grid dynamically

### Booking Form Validation
- Real-time validation with inline error messages
- Email format, phone (international), required fields
- Step navigation only advances when current step is valid
- Booking reference format: PAC-[YEAR]-[6 random alphanumeric]

### LocalStorage Schema
```json
{
  "bookings": [
    {
      "id": "PAC-2026-A3X9KL",
      "date": "2026-03-15",
      "timeSlot": "10:00-11:30",
      "court": "Court 1 — Panoramic",
      "players": 4,
      "bookerName": "Michaël Boudot",
      "bookerEmail": "contact@kerkyra.fr",
      "bookerPhone": "+33600000000",
      "extras": { "rackets": 2, "balls": true },
      "totalPrice": 42,
      "paymentMethod": "card",
      "status": "confirmed",
      "createdAt": "2026-03-02T10:00:00Z"
    }
  ]
}
```

### Multilingual (FR/EN/GR)
- JS object with translation keys for all UI strings
- Language toggle updates entire UI instantly (no reload)
- Default: FR
- Store preference in localStorage

### Icons
- Use inline SVG icons only (no external icon libraries)
- Key icons needed: calendar, clock, user, location-pin, padel-racket, check, arrow-right, star, download

---

## UX DETAILS

- Sticky header with blur backdrop
- Active tab has gold underline + slightly brighter text
- Form inputs: dark bg (#0D2B1A), gold focus border, white text, placeholder in muted green
- All primary CTAs: gold (#F5C518) bg, dark text, rounded-full pill shape, font-weight 700
- Secondary CTAs: transparent with gold border
- Error states: red (#FF4757) border + small error message below
- Success toast notifications (top-right, auto-dismiss 3s)
- Skeleton loading states for court cards

---

## FOOTER

- Logo + tagline: "L'académie de padel premium de Corfou"
- Links: Mentions légales | CGV | Contact | Instagram
- Address: Corfu, Greece | contact@padelacademycorfu.com
- Copyright 2026 Padel Academy Corfu

---

Deliver a single, complete, production-ready index.html file.
The app must work entirely offline (except Google Fonts).
All placeholder images should be CSS gradient + SVG compositions, no <img> with src URLs.