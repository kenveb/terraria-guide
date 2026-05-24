# PRD: Terraria Guide Site

## 1. Product Overview

### 1.1 Positioning
A clean, beginner-friendly English-language guide website for **Terraria** players. Focused on practical, actionable guides rather than exhaustive wiki-style documentation.

### 1.2 Target Audience
- New Terraria players (0-100 hours) who need guidance on progression
- English-speaking players worldwide
- Players looking for specific boss strategies, crafting guides, and building tips

### 1.3 Competitive Differentiation

| Competitor | Weakness | Our Advantage |
|------------|----------|---------------|
| Official Terraria Wiki | Too detailed, overwhelming for beginners, cluttered UI | Simpler content, focused on "what to do next" |
| Steam Guides | Inconsistent quality, no unified navigation | Curated content, consistent design |
| YouTube guides | Hard to reference mid-game | Text-based, searchable, skimmable |

### 1.4 Site Name (TBD)
Options: `terrariaguide.pro` / `terrariacraft.xyz` / `guide-to-terraria.com`
→ Final decision after availability check.

---

## 2. Content Plan

### 2.1 Content Sections

| Section | Description | Priority |
|---------|-------------|----------|
| Getting Started | New player guide, first steps, basic survival | P0 |
| Boss Progression | Boss strategies in order (King Slime → Moon Lord) | P0 |
| Class Builds | Melee, Ranged, Mage, Summoner, and hybrid builds | P0 |
| Crafting Guide | Key items, workstations, progression gates | P1 |
| Biome Guide | Exploration tips per biome | P1 |
| Building Tips | Base design, arenas, NPC housing | P1 |
| Potions & Buffs | Useful buffs and how to brew them | P2 |
| Achievements | Guide to hardest achievements | P2 |

### 2.2 MVP Page List (15 pages)

**Phase 1 — Core Content:**
1. `index.html` — Homepage / hub
2. `getting-started.html` — First hour guide
3. `boss-order.html` — Boss progression order
4. `king-slime.html` — King Slime guide
5. `eye-of-cthulhu.html` — Eye of Cthulhu guide
6. `skeletron.html` — Skeletron guide
7. `wall-of-flesh.html` — Wall of Flesh / Hardmode entry
8. `melee-build.html` — Melee class build guide
9. `ranged-build.html` — Ranged class build guide
10. `mage-build.html` — Mage class build guide
11. `summoner-build.html` — Summoner class build guide
12. `best-weapons.html` — Best weapons by stage
13. `best-armor.html` — Best armor sets by stage
14. `npcs-housing.html` — NPC housing & happiness
15. `arenas.html` — Boss arena designs

**Phase 2 — Expansion (post-MVP):**
- Hardmode bosses (Destroyer, Twins, Skeletron Prime, Plantera, Golem, Lunatic Cultist, Moon Lord)
- Potions guide
- Biome guides (Jungle, Dungeon, Underworld, Corruption/Crimson, Hallow)
- Fishing guide
- Building tips & inspiration

### 2.3 Content Production
- Use AI (Claude) to generate initial draft per page
- Human review for accuracy (critical: game mechanics must be correct)
- Consistent template: overview → preparation → step-by-step → rewards
- Internal linking between related pages

---

## 3. Tech Architecture

### 3.1 Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Static HTML5 + CSS3 + Vanilla JS |
| Styling | Custom CSS (no framework, keep it lightweight) |
| Icons | Font Awesome (free tier) |
| Hosting | Cloudflare Pages |
| CDN | Cloudflare (built-in) |
| Domain | Cloudflare Registrar or Namesilo |
| Version Control | GitHub |

### 3.2 Structure

```
terraria-guide/site/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── main.js
├── pages/
│   ├── getting-started.html
│   ├── boss-order.html
│   ├── king-slime.html
│   └── ... (more pages)
└── assets/
    └── (images/icons)
```

### 3.3 SEO Strategy
- Each page has unique `<title>` and `<meta name="description">`
- Semantic HTML5 tags (`<header>`, `<nav>`, `<main>`, `<article>`, `<footer>`)
- Structured data (FAQ schema for guide pages)
- XML sitemap (`sitemap.xml`)
- `robots.txt`
- Clean URL structure (`/pages/boss-order.html`)
- Mobile-first responsive design

### 3.4 Deployment Flow

```
Edit HTML locally → git push → Cloudflare Pages auto-deploys → Live
```

---

## 4. Monetization Plan

### 4.1 Ad Strategy

| Phase | Platform | Condition | Expected RPM |
|-------|----------|-----------|-------------|
| Launch | Buuuo / PropellerAds | No traffic threshold | ~$0.5-1 |
| Growth | Google AdSense | 20+ pages, some traffic | ~$1-3 |
| Scale | Ezoic | 10k+ monthly visitors | ~$3-8 |

### 4.2 Ad Placement (planned)
- Below article title (one native ad)
- Sidebar (if desktop layout)
- Between content sections (one in-article ad)
- Footer banner

> **Rule:** No intrusive ads. Keep user experience first.

### 4.3 Traffic Targets

| Milestone | Timeframe | Daily UV | Monthly Revenue (est.) |
|-----------|-----------|----------|----------------------|
| MVP launch | Week 1 | 0-10 | $0 |
| Initial content | Month 1 | 10-50 | $0-5 |
| Growth | Month 3 | 50-300 | $5-30 |
| Scale | Month 6 | 300-1000 | $30-150 |

---

## 5. Milestones

| # | Milestone | Deliverable | Timeline |
|---|-----------|-------------|----------|
| M1 | PRD + Content | PRD done, all MVP pages drafted | Day 1-2 |
| M2 | Site Build | All HTML pages created, styled, linked | Day 3-5 |
| M3 | Deploy | GitHub repo → Cloudflare Pages → custom domain live | Day 6 |
| M4 | AdSense | Submit application | Day 7+ |
| M5 | Iterate | Monitor analytics, expand content, optimize SEO | Ongoing |

---

## 6. Success Metrics

- **Technical:** Pages load under 2s (Cloudflare CDN)
- **SEO:** Pages indexed by Google within 2 weeks
- **Traffic:** 100+ daily unique visitors by month 3
- **Revenue:** $5+/month by month 3 (validation of model)

---

## 7. Risks & Mitigation

| Risk | Impact | Mitigation |
|------|--------|------------|
| Google not indexing AI content | SEO failure | Manual editorial pass, unique value-add |
| AdSense rejection | No revenue | Start with low-tier ad network |
| Terraria updates (1.4.5+) | Content outdated | Track patch notes, update key pages |
| Domain/parking costs | Small financial loss | Total cost < $15 — acceptable loss |
