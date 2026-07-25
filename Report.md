# ScrollHeart — Full Project Report
> A comprehensive handoff document for AI agents to understand, build, and deploy the ScrollHeart romantic storytelling skill system.

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [What This Project Is](#2-what-this-project-is)
3. [Target User](#3-target-user)
4. [The Problem This Solves](#4-the-problem-this-solves)
5. [Competitive Analysis](#5-competitive-analysis)
6. [Brand Identity](#6-brand-identity)
7. [Emotional Safety Framework](#7-emotional-safety-framework)
8. [Technical Architecture](#8-technical-architecture)
9. [Scene & Narrative Structure](#9-scene--narrative-structure)
10. [User Interview Flow](#10-user-interview-flow)
11. [Design Brief Generator](#11-design-brief-generator)
12. [Code Generation Rules](#12-code-generation-rules)
13. [Deployment & Privacy Protocol](#13-deployment--privacy-protocol)
14. [Post-Build Guidance](#14-post-build-guidance)
15. [Prompts for AI Agents](#15-prompts-for-ai-agents)
16. [Red Flags Checklist](#16-red-flags-checklist)
17. [Definition of Done](#17-definition-of-done)
18. [Appendix: Research Sources](#18-appendix-research-sources)

---

## 1. Executive Summary

**ScrollHeart** is an AI-powered skill system that helps a boy create a romantic, scroll-driven storytelling website for a girl he cares about. The entire experience is built inside an AI IDE (Antigravity, Claude Code, Cursor, etc.) through a friendly, conversational workflow.

The skill interviews the user about the girl, runs a safety check to prevent creepy or pushy content, generates a unique design brief, writes the code (static HTML/CSS/JS), deploys to GitHub Pages, and guides the user on how to present the gift.

**Key principle:** Sweet, not creepy. Blush-worthy, not pressure-creating.

---

## 2. What This Project Is

### Product Definition
- A **reusable AI skill file** (not a one-time website)
- Works across multiple AI coding agents: Antigravity, Claude Code, Cursor, Codex, Windsurf
- Generates a **static, mobile-first, scroll-driven romantic story website**
- Zero build tools — pure HTML/CSS/JS, hosts free on GitHub Pages
- Every output is unique based on the user's answers about the girl

### What It Creates
A 5-scene scroll story with:
- Parallax layers (background, midground, foreground, text)
- GSAP ScrollTrigger with section snapping
- Floating typography with gentle animations
- Atmospheric color palette derived from her personality
- Optional background music (HTML5 Audio, user-gesture activated)
- Mobile-first responsive design
- Total payload under 2MB for 3G networks

### What It Is NOT
- NOT a template shop or drag-and-drop builder
- NOT a dating app or relationship pressure tool
- NOT a framework or library dependency
- NOT a public social media post generator
- NOT a coercive "runaway button" or forced-interaction site

---

## 3. Target User

### Primary Persona
- **Gender:** Male (boy)
- **Age:** 18–28
- **Relationship stage:** Has a girl best friend, crush, or early-stage girlfriend
- **Tech skill:** Beginner to intermediate — knows basic coding concepts but not design
- **Emotional state:** Nervous but sincere, wants to do something meaningful but doesn't know how
- **Goal:** Express feelings in a way that is sweet, memorable, and safe

### Secondary Persona
- Non-tech users who have never used AI coding tools before
- Users who want a guided, conversational experience
- Users who need emotional validation and safety guardrails

### User Friction Points
1. Doesn't know how to design a romantic website
2. Worried about being creepy or pushy
3. Doesn't know what to write or how to structure the story
4. Doesn't know how to host or share it privately
5. Afraid of rejection or embarrassment

---

## 4. The Problem This Solves

### The Gap in the Market
1. **No romance-specific AI skill exists** — all competitors are generic (cinematic, design, animation)
2. **No emotional safety framework** — existing tools don't check for creepiness or pressure
3. **No person-focused interview** — they ask "audience/use-case/tone" generically
4. **No static-site enforcement** — competitors need complex build tools (Higgsfield, ffmpeg, React)
5. **No audio-visual sync for love stories** — no skill handles music-synced romantic storytelling
6. **No post-build guidance** — no skill tells the user HOW to present the gift

### Why Existing Solutions Fail
| Existing Tool | Why It Fails for Romance |
|---|---|
| `scroll-world` (oso95) | Needs Higgsfield CLI + ffmpeg + Python — not static |
| `gsap-scrolltrigger` (greensock) | Pure technical reference — no storytelling, no emotion |
| `cinematic-ui` (akseolabs) | Film-director formal — romance is one genre among many, no safety |
| `hallmark` (nutlope) | Anti-slop design skill — no emotional intelligence, no relationship safety |
| `YourLovePage` (template) | Runaway "No" button, coercive, assumes relationship status |
| Generic website builders | Template-based, impersonal, not story-driven |

### The ScrollHeart Solution
- **Conversation-first:** Asks about HER, not about the project
- **Safety-first:** Auto-detects and rejects creepy/pushy content
- **Story-first:** Builds around a song/emotional arc, not a template
- **Privacy-first:** Private link, no tracking, no public sharing by default
- **Guidance-first:** Tells the user exactly how to give it to her

---

## 5. Competitive Analysis

### Competitor 1: `scroll-world` (oso95/scroll-world)
- **What it does:** 3D scroll-scrubbed world using AI-generated video clips
- **How it's built:** SKILL.md with YAML frontmatter, step-based workflow (0–8), heavy dependencies (Higgsfield CLI, ffmpeg, Python)
- **Strengths:** Seamless video transitions, mobile portrait option, budget awareness
- **Weaknesses:** Not static, not romantic, requires external AI video generation, complex setup
- **What we borrow:** Step-based workflow, user interview before building, mobile-first question
- **What we reject:** Video dependency, brand/industry focus, technical complexity

### Competitor 2: `gsap-scrolltrigger` (greensock/gsap-skills)
- **What it does:** Official GSAP ScrollTrigger documentation as an AI skill
- **How it's built:** Modular sub-skills, reference-style tables, code examples, Do/Don't lists
- **Strengths:** Authoritative, cross-platform, comprehensive API coverage
- **Weaknesses:** No storytelling, no emotion, no interview, pure technical reference
- **What we borrow:** ScrollTrigger config tables, best practices, cleanup rules
- **What we reject:** No user interaction, no narrative structure, no safety framework

### Competitor 3: `cinematic-ui` (akseolabs-seo)
- **What it does:** Film-inspired website design using director-driven art direction
- **How it's built:** 4 strict phases (decisions → storyboard → compiled spec → build), start questionnaire, demo uniqueness protocol, progressive loading
- **Strengths:** Anti-convergence system, delegation model, reference library (50+ files), self-critique scoring
- **Weaknesses:** Romance is one of many genres, no relationship safety, no person-focused interview, assumes design expertise
- **What we borrow:** Phase-based workflow, uniqueness protocol, progressive reference loading, pre-emit self-critique
- **What we reject:** Film-director formal tone, no emotional safety, no deployment guidance

### Competitor 4: `hallmark` (nutlope)
- **What it does:** Anti-AI-slop design skill with 66 quality gates
- **How it's built:** 3 verbs (audit/redesign/study), pre-flight scan, design-context gate, genre detection, theme diversification, locked tokens
- **Strengths:** Pre-flight project detection, 66 slop-test gates, mobile hard rules, honest copy rule
- **Weaknesses:** Generic design focus, no romance, no emotional intelligence, no relationship context
- **What we borrow:** Pre-flight scan, slop-test gates, mobile responsiveness rules, locked token discipline
- **What we reject:** Generic audience/use-case/tone questions, no emotional safety, no post-build guidance

### Competitor 5: `AlwaysBeMine` (UjjwalSaini07 — template, not a skill)
- **What it does:** Ready-made Valentine proposal website
- **How it's built:** npm-based project with playful animations, background music, surprise pop-ups
- **Strengths:** Ready to use, cute animations
- **Weaknesses:** Runaway "No" button (coercive), assumes relationship status, public sharing encouraged, not mobile-first, requires build step
- **What we borrow:** The emotional intent (making someone smile)
- **What we reject:** EVERYTHING else — this is the anti-pattern we exist to prevent

---

## 6. Brand Identity

### Brand Name: ScrollHeart
**Why this name:**
- 2 syllables, 10 characters — easy to type into any AI agent
- "Scroll" = the technical mechanism (scroll-driven storytelling)
- "Heart" = the emotional purpose (love, care, courage)
- Out-of-category naming — doesn't say "romantic-website-builder" but evokes the feeling
- Future-proof — works for friendship, crush, dating, anniversary, proposal
- Culturally safe — "heart" means love in every language, no creep connotations
- Available — unclaimed on GitHub and major platforms

### Brand Tagline
> "Build her a story she can scroll through."

**Why this works:**
- "Build" = appeals to the coder identity
- "Her" = gently confirms the boy-to-girl framing
- "Story" = emotional, not "website" or "page"
- "Scroll through" = describes the experience, not the technology
- No pressure words like "love," "forever," or "mine"

### Brand Voice: "The Calm Bestie"
Inspired by Headspace (calm presence), Glossier (warm bestie), and Innocent Drinks (playful quirky).

| Situation | Generic AI Would Say | ScrollHeart Says |
|---|---|---|
| Starting | "What is your project brief?" | "Hey! So there's someone special you want to make something for? Tell me about her." |
| User is shy | "Please provide the required inputs." | "No pressure at all — we can start simple. What's one thing that makes her smile?" |
| Asking relationship | "What is your relationship status?" | "How would you describe where you two are right now? Friends? Something more? Still figuring it out?" |
| Red flag detected | "Input rejected." | "Hmm, that might feel a bit intense for where things are. Want to try a gentler way to say it?" |
| Building | "Generating HTML/CSS/JS output." | "I'm putting this together now... think of it like writing a letter, but she reads it with her fingers." |
| Finished | "Build complete. Output delivered." | "It's ready. And hey — however she reacts, you did something brave and sweet just by making this." |

### Brand Color System
Based on 2026 romantic color psychology research (rose gold as anchor):

| Token | Hex | Role | Emotion |
|---|---|---|---|
| `--rose-gold` | `#DEA193` | Primary accent | Warmth, affection, blush |
| `--midnight` | `#0F0F1A` | Background default | Intimacy, privacy, night |
| `--cream` | `#FDFBD4` | Text on dark | Softness, readability |
| `--charcoal` | `#4A4A4A` | Secondary text | Sophistication, restraint |
| `--teal-glow` | `#069494` | Interactive elements | Trust, calm, "it's safe to click" |
| `--gold-dust` | `#C9A96E` | Highlights, stars | Magic, sparkle, "this is special" |

**Why these colors:**
- Rose gold symbolizes elegance, warmth, and romance without being aggressive
- Midnight blue creates intimacy and privacy (like a handwritten note at night)
- Cream provides soft readability without harsh white contrast
- Teal glow signals safety and trust for interactive elements
- Gold dust adds magical sparkle for special moments

**Colors to AVOID:**
- Hot pink, bright red — trigger "aggressive romance" or "Valentine's commercial"
- Lime green, bright orange, electric blue, neon yellow — compete with warmth, feel cheap/digital
- Pure white backgrounds — feel like a billboard, not a whisper

### Brand Positioning Statement
> For a guy who wants to express how he feels to a girl he cares about, ScrollHeart is the AI skill that turns his story into a beautiful scroll-driven website — because the best gifts aren't bought, they're built, and the best words aren't spoken, they're scrolled.

### Brand Architecture
```
ScrollHeart (master brand)
├── ScrollHeart Skill (the AI agent skill file)
│   └── SKILL.md
│   └── references/
│       ├── 01-interview-flow.md
│       ├── 02-safety-checklist.md
│       ├── 03-design-brief-generator.md
│       ├── 04-scene-templates.md
│       ├── 05-code-generation-rules.md
│       ├── 06-deployment-guide.md
│       └── 07-post-build-guide.md
├── ScrollHeart Stories (example outputs / gallery)
├── ScrollHeart Community (future: Discord / Reddit)
└── ScrollHeart Variants (future: friendship, anniversary, proposal)
```

---

## 7. Emotional Safety Framework

### The "Green Flag" Commitment

**ScrollHeart will NEVER:**
1. Assume she owes you a response
2. Use guilt language or pressure
3. Include private information without your explicit consent
4. Create anything that could embarrass her publicly
5. Rush you or make you feel inadequate
6. Use her real name or photo without asking
7. Quote private conversations or DMs
8. Include location data or timestamps
9. Use "I can't live without you" or guilt-inducing language
10. Assume relationship status (e.g., "my girlfriend," "forever mine")
11. Include sexual imagery or innuendo
12. Create overwhelming length (max 2–4 minutes of content)
13. Auto-play audio loudly (always requires user gesture)
14. Use runaway buttons or forced interactions
15. Include countdown timers or ultimatums
16. Compare her to exes or other girls
17. Include excessive personal detail (address, workplace, family issues)

**ScrollHeart will ALWAYS:**
1. Ask before using anything personal
2. Suggest gentler alternatives when things feel too intense
3. Give you control over every word and every scene
4. Remind you that the gesture itself is enough
5. Celebrate your courage for trying
6. Use abstract shared memories (not specific private details)
7. Put her in control of pacing (scroll-driven = she decides speed)
8. Use soft, handwritten-style typography
9. Use dark mode as default for intimacy
10. Include a no-pressure CTA (e.g., "Replay the story" not "Will you be mine?")

### Red Flag Detection Algorithm
Before generating ANY output, the AI must run this checklist:

| Check | Pass Criteria | If Failed |
|---|---|---|
| Relationship assumption | Does NOT use possessive language ("my girlfriend," "mine") | Suggest neutral alternatives ("my favorite person," "someone special") |
| Privacy violation | Does NOT include real names, photos, private messages without consent | Replace with nicknames, initials, or abstract descriptions |
| Pressure language | Does NOT include guilt, obligation, or ultimatum language | Replace with gratitude and appreciation language |
| Length appropriateness | Total scroll time 2–4 minutes max | Suggest trimming scenes or reducing text |
| Audio safety | Audio requires explicit user gesture to start | Add tap-to-play overlay with gentle prompt |
| Public exposure risk | Site is private by default (no-index, obfuscated URL) | Enforce privacy settings automatically |
| Accessibility | Respects `prefers-reduced-motion` | Provide static fallback with fade transitions |
| Cognitive load | Max 2 lines of text per scene, 1 focal visual element | Simplify text, increase breathing room |
| Tone calibration | Matches the relationship stage (friends → crush → dating) | Adjust scene intensity and CTA directness |
| Cultural sensitivity | Appropriate for Indian/Hinglish context if applicable | Offer language and cultural preference options |

### Relationship Stage Calibration
The skill must detect (via interview) the relationship stage and adjust output accordingly:

| Stage | Tone | CTA Type | Scene Intensity | Example CTA |
|---|---|---|---|---|
| **Best Friends** | Playful, warm, appreciative | Gratitude-focused | Gentle, nostalgic | "I'm glad you're in my life" |
| **Crush / Figuring it out** | Sweet, hopeful, gentle | Invitation-focused | Moderate, dreamy | "I'd love to take you out sometime" |
| **Early Dating** | Romantic, confident, tender | Commitment-focused | Warm, intimate | "Every day with you feels like a story" |
| **Committed** | Deep, passionate, certain | Celebration-focused | Rich, layered | "You're my favorite chapter" |

---

## 8. Technical Architecture

### Core Stack (Static Site Only)
- **HTML5** — Semantic structure, 5 full-screen sections
- **CSS3** — Custom properties (design tokens), flexbox/grid, `@media` queries, `dvh`/`svh` units
- **Vanilla JavaScript** — No frameworks, no build step
- **GSAP 3.13+** — ScrollTrigger for pinning, snapping, parallax (loaded from CDN)
- **HTML5 Audio API** — Background music with user-gesture activation
- **Service Worker** — Optional offline capability for "she can view it anytime"

### What Is NOT Allowed
- No React, Vue, Svelte, or any framework
- No build tools (Vite, Webpack, Parcel)
- No npm install step
- No server-side rendering
- No external APIs or databases
- No analytics or tracking
- No cookies
- No jQuery

### GSAP ScrollTrigger Configuration
```javascript
// Core pattern for each scene
gsap.registerPlugin(ScrollTrigger);

// Section pinning + snapping
ScrollTrigger.create({
  trigger: ".scene",
  start: "top top",
  end: "+=100vh",
  pin: true,
  scrub: 1,
  snap: {
    snapTo: 1 / 4, // snap to section progress
    duration: 0.3,
    delay: 0.1,
    ease: "power1.inOut"
  }
});

// Parallax layers per scene
gsap.to(".bg-layer", { yPercent: -20, scrollTrigger: { scrub: true } });
gsap.to(".mid-layer", { yPercent: -10, scrollTrigger: { scrub: true } });
gsap.to(".fg-layer", { yPercent: 10, scrollTrigger: { scrub: true } });
```

### Mobile-First Rules
- Base styles target 320px width minimum
- Use `min()` and `max()` for fluid sizing
- `dvh` / `svh` / `lvh` for viewport units (handles dynamic toolbars)
- Touch events for mobile scroll (`touchmove`)
- `overflow-x: clip` on `html` and `body` (never `hidden`)
- `minmax(0, 1fr)` for grid tracks (prevents overflow)
- Safe area insets for notched phones: `env(safe-area-inset-*)`
- Test at 320px, 375px, 414px, 768px breakpoints

### Performance Budget
- Total payload: **under 2MB** for 3G networks
- Images: CSS gradients + SVG only (no external images unless user-provided)
- Fonts: Google Fonts with `display=swap`, single variable font preferred
- Audio: MP3 128kbps, loaded only after user gesture
- GSAP: Load from CDN (`cdnjs` or `jsdelivr`)
- Target: **60fps on mid-range Android** (Snapdragon 6-series equivalent)

### Accessibility Requirements
- `prefers-reduced-motion: reduce` — disable parallax, use fade transitions only
- Screen reader support: `aria-label`, `role="img"`, live regions for text reveals
- Keyboard navigation: `tabindex`, focus management through pinned sections
- Color contrast: WCAG AA minimum even with soft palettes
- Cognitive load: max 2 lines of text per scene
- Multi-language: Support Hinglish, Roman Urdu, or pure English based on user preference

---

## 9. Scene & Narrative Structure

### The 5-Scene Arc
Inspired by *Aankhon Se Batana* (song about eyes speaking what words cannot) and Joseph Campbell's micro-narrative structure.

| Scene | Name | Narrative Role | Visual Direction | Motion Direction | Duration |
|---|---|---|---|---|---|
| 1 | The First Glance | Intro | Dark night, bokeh, silhouette layers | Slow background drift (0.2x), faster foreground drift (1.5x) | ~30s |
| 2 | The Silent Conversation | Verse | Cozy balcony, glowing windows, floating text | Horizontal drift with subtle vertical offset | ~40s |
| 3 | The Climax | Chorus | Warm gold, centered focal card, particles | Pinned section with zoom-in emphasis | ~45s |
| 4 | Quiet Night | Bridge | Deep blue star field, quiet atmosphere | Z-axis depth separation | ~35s |
| 5 | Outro & CTA | Finish | Minimal motion, strong CTA focus | Fade to stillness, heartbeat pulse on CTA | ~20s |

### Parallax Layer Theory
Each scene has 4 layers with different scroll speeds:

| Layer | Speed | Content | Emotional Role |
|---|---|---|---|
| Background | 0.2x–0.3x | Abstract gradients, stars, bokeh | Shared memory, distant, nostalgic |
| Midground | 0.5x–0.7x | Silhouettes, shapes, window lights | Current emotion, connection |
| Foreground | 1.0x–1.5x | Floating particles, text bubbles, sparkles | Action, intention, movement |
| Text | 1.0x | Story text, lyrics paraphrases, CTA | Inner voice, what he wants to say |

### Scene Content Guidelines
- **No copyrighted lyrics** — paraphrase emotional themes only
- **No real names** — use nicknames, initials, or abstract references
- **No private conversations** — use abstract shared memories
- **Text max 2 lines per scene** — poetic, not prose
- **One focal visual element per scene** — prevents cognitive overload

### Example Scene Content (Best Friend Stage)
| Scene | Text | Visual |
|---|---|---|
| 1 | "Some people you meet, and you just know." | Silhouette of two figures against starry night |
| 2 | "She laughs, and the whole room feels lighter." | Cozy window glow, floating light particles |
| 3 | "I don't say it enough, but I'm glad you're here." | Warm gold center card with radiating light |
| 4 | "Quiet moments with you are my favorite kind." | Deep blue starfield, slow drifting stars |
| 5 | "This is for you. Replay it whenever you want." | Minimal, heartbeat pulse on replay button |

---

## 10. User Interview Flow

### Interview Philosophy
- Ask **one question at a time** — never bombard
- Validate emotions: "That sounds really sweet" not "Provide the data"
- Offer defaults: "If you're not sure, here's what most people pick"
- Use simple English — no design jargon ("Does she like sunset or midnight?" not "What's your hex code?")
- Progressive disclosure — easy questions first, deeper ones later

### The 10 Questions (In Order)

**Question 1 — The Hook (Warm-up)**
> "Hey! So there's someone special you want to make something for? I'm here to help you build her a little story she can scroll through. No pressure — we can take this one step at a time. Ready?"

**Question 2 — Relationship Stage**
> "How would you describe where you two are right now? Are you best friends? Crushing? Early dating? Or something else entirely? This helps me calibrate the tone so it feels right."
- Options: Best Friends / Crush (figuring it out) / Early Dating / Committed / Other

**Question 3 — Her Personality**
> "If you had to describe her in three words, what would they be? Like 'funny, kind, mysterious' or 'bubbly, smart, calm' — whatever feels true."
- Free text, 3 words max

**Question 4 — A Shared Memory**
> "What's one moment with her that still makes you smile? It can be small — a conversation, a walk, something she said. Don't worry, I won't use the exact details unless you say it's okay."
- Free text, abstract it for privacy

**Question 5 — Favorite Color / Mood**
> "Does she lean more toward warm colors (sunset, gold, rose) or cool colors (midnight, teal, starlight)? Or maybe something else entirely?"
- Options: Warm sunset / Cool midnight / Soft pastel / Bold and bright / I'm not sure

**Question 6 — A Song or Sound**
> "Is there a song that reminds you of her? Or a type of music she loves? If you don't have one, I can suggest something that fits the mood."
- Free text, validate copyright before using

**Question 7 — What You Want to Say**
> "If you could tell her one thing — and you knew she'd really hear it — what would it be? Don't overthink it. Even 'I'm glad I met you' is perfect."
- Free text, max 2 sentences

**Question 8 — Her Comfort Level**
> "How public or private should this feel? Some people love grand gestures, others prefer something quiet and personal."
- Options: Very private (just her) / Somewhat private (close friends okay) / I'm not sure

**Question 9 — The Final Moment**
> "How do you want her to feel when she reaches the end? Happy? Warm? Surprised? Hopeful?"
- Options: Warm and appreciated / Happy and smiling / Hopeful and curious / Surprised and touched

**Question 10 — Your Name (Optional)**
> "Do you want your name on it? Or would you rather keep it anonymous? Both are totally fine."
- Options: My first name / Just my initial / Anonymous / A nickname she calls me

---

## 11. Design Brief Generator

### How Answers Become Design Specs

| Answer Category | Design Output |
|---|---|
| Relationship stage → | Tone calibration (playful/warm/romantic/deep), CTA directness |
| Personality words → | Animation style (bouncy/gentle/mysterious/calm), text entrance type |
| Shared memory → | Scene 2 visual theme (abstracted), color temperature |
| Color preference → | Primary palette (warm gold/cool teal/soft pastel/bold) |
| Song choice → | Audio track, tempo, scene pacing, beat-sync opportunities |
| What to say → | Scene 3 climax text, paraphrased for copyright safety |
| Comfort level → | Privacy settings (no-index, obfuscated URL, password) |
| Final feeling → | Scene 5 outro tone, CTA wording, animation exit style |
| Name choice → | Signature placement (or none), anonymity level |

### Color Palette Generator

| User Preference | Primary | Background | Accent | Text |
|---|---|---|---|---|
| Warm sunset | `#DEA193` (rose gold) | `#0F0F1A` (midnight) | `#C9A96E` (gold dust) | `#FDFBD4` (cream) |
| Cool midnight | `#069494` (teal glow) | `#0A0A1A` (deep navy) | `#8A9A5B` (moss) | `#E8E6D9` (soft white) |
| Soft pastel | `#D4A5A5` (dusty rose) | `#1A1A2E` (soft midnight) | `#B8C5D6` (soft blue) | `#F5F0E8` (warm white) |
| Bold and bright | `#E07A5F` (terracotta) | `#1D1D2E` (charcoal) | `#F2CC8F` (honey) | `#FFF8E7` (ivory) |

### Typography Pairing Generator

| Personality | Display Font | Body Font | Feeling |
|---|---|---|---|
| Funny, bubbly | "Dancing Script" (handwritten) | "Inter" (clean sans) | Playful, personal |
| Kind, warm | "Great Vibes" (elegant script) | "Lora" (soft serif) | Gentle, intimate |
| Mysterious, deep | "Cinzel" (dramatic serif) | "Source Sans Pro" (neutral) | Cinematic, poetic |
| Smart, calm | "Playfair Display" (editorial serif) | "Open Sans" (friendly sans) | Sophisticated, thoughtful |

### Animation Style Generator

| Personality | Text Entrance | Layer Motion | Particle Style |
|---|---|---|---|
| Funny, bubbly | Bounce in + fade | Fast drift, elastic | Floating bubbles, sparkles |
| Kind, warm | Gentle fade up | Slow parallax, smooth | Soft bokeh, glowing orbs |
| Mysterious, deep | Typewriter reveal | Horizontal drift, subtle | Drifting stars, mist |
| Smart, calm | Fade + slight scale | Minimal, precise | Clean geometric shapes |

---

## 12. Code Generation Rules

### File Structure (Static Site)
```
scrollheart-story/
├── index.html          # Main HTML, 5 scenes
├── css/
│   └── style.css       # All styles, mobile-first
├── js/
│   └── main.js         # GSAP animations, audio controller
├── assets/
│   └── (optional user images, audio)
└── .nojekyll           # For GitHub Pages (if needed)
```

### HTML Structure Rules
- 5 `<section>` elements, each `100vh` minimum
- Each section contains 4 layer divs: `.bg-layer`, `.mid-layer`, `.fg-layer`, `.text-layer`
- All layers are `position: absolute` within `position: relative` section
- Semantic HTML: `<main>`, `<section>`, `<h1>`–`<h2>`, `<p>`, `<button>`
- Audio element with `preload="none"`, controls hidden, activated by JS

### CSS Rules
- Mobile-first: base styles for 320px, `@media (min-width: 768px)` for desktop
- CSS custom properties for all design tokens (colors, fonts, spacing)
- `dvh` / `svh` for section heights
- `will-change: transform` on animated layers (GPU acceleration)
- `overflow-x: clip` on root elements
- `@media (prefers-reduced-motion: reduce)` — disable parallax, use opacity fades
- Font loading: `@import` Google Fonts with `display=swap`

### JavaScript Rules
- GSAP loaded from CDN: `https://cdnjs.cloudflare.com/ajax/libs/gsap/3.13.0/gsap.min.js`
- ScrollTrigger plugin loaded separately and registered
- One master timeline per scene
- `ScrollTrigger.create()` for each section with pinning
- `snap` configuration for section snapping
- Audio controller: play/pause/mute/restart, only activates after user gesture
- Event listeners: `click` for audio start, `touchmove` for mobile scroll
- Cleanup: `ScrollTrigger.getAll().forEach(t => t.kill())` on page unload

### GSAP Best Practices (From Official Skill)
- Register plugin once: `gsap.registerPlugin(ScrollTrigger)`
- Create ScrollTriggers in DOM order (top to bottom)
- Use `scrub` OR `toggleActions`, never both on same trigger
- For fake horizontal scroll: `ease: "none"` on container animation
- Call `ScrollTrigger.refresh()` after fonts load or layout changes
- Remove `markers: true` before production
- Kill ScrollTriggers on page unload to prevent memory leaks

### Audio Rules
- HTML5 `<audio>` element with `preload="none"`
- Hidden default controls, custom UI built in CSS/JS
- Play ONLY after explicit user gesture (tap/click on "Start the Story" button)
- Mute toggle always visible
- Volume starts at 50%
- Graceful fallback if audio fails to load
- No auto-play, no surprise sound

---

## 13. Deployment & Privacy Protocol

### GitHub Pages Setup
1. Create new repository with **obfuscated name** (not her name or "love")
2. Upload static files (index.html, css/, js/, assets/)
3. Enable GitHub Pages from main branch
4. Set custom domain OR use `username.github.io/obfuscated-repo-name`
5. Add `.nojekyll` file to prevent Jekyll processing

### Privacy Measures
- `<meta name="robots" content="noindex, nofollow">` in HTML head
- No Google Analytics, no tracking pixels, no cookies
- Repository set to **private** if possible (GitHub Pro), or at minimum obscure name
- No social media meta tags (no preview cards when shared)
- Optional: client-side password protection (simple JS prompt)

### Sharing Protocol
1. **Private first** — send link via personal text/DM only
2. **No social media** — never post on Instagram, WhatsApp status, or public feeds
3. **No group chats** — share 1-on-1 only
4. **Timing matters** — send when she's relaxed and alone, not in public or busy
5. **Context matters** — include a personal message: "I made something for you. Take your time."
6. **No pressure** — make it clear there's no expected response

### QR Code Alternative
- Generate QR code linking to the site
- Print on a handwritten note or card
- Physically give to her in person
- Most private method — no digital trail

---

## 14. Post-Build Guidance

### How to Present the Site to Her

**The Message to Send (Examples by Stage):**

**Best Friends:**
> "Hey, I made something small for you. It's just a little story about how much I appreciate you. No need to respond right away — just open it when you have a quiet moment. 💫"

**Crush:**
> "I've been wanting to tell you something, and I'm better with code than words. I made this for you. Take your time with it. 😊"

**Early Dating:**
> "I wanted to do something a little different for you. Open it when you're free and have a few minutes. I hope it makes you smile. ❤️"

**Committed:**
> "You know I'm not great with words, so I built them instead. This is for you. I love you. 💫"

### What to Do If She Doesn't Respond Immediately
1. **Wait at least 24 hours** — she may need time to process
2. **Don't double-text** — one follow-up max, and only if genuine
3. **Don't interpret silence as rejection** — she may be busy, shy, or figuring out her own feelings
4. **Be proud of the gesture** — regardless of outcome, you did something brave
5. **If she asks about it** — be honest: "I just wanted you to know how I feel. No pressure."

### What to Do If She Loves It
1. Thank her for taking the time
2. Keep the conversation light — don't rush to define the relationship
3. Suggest doing something together based on a scene she liked
4. Keep the site live as a memory, or update it for future occasions

### What to Do If She's Uncomfortable
1. **Apologize sincerely** — "I'm sorry if that felt like too much. I just wanted you to know I care."
2. **Give space** — don't push for a conversation immediately
3. **Learn from it** — the skill's safety check should have caught this; review what went wrong
4. **Delete the site** — respect her privacy by removing the content

### When to Delete the Repository
- After she has seen it and you've discussed it
- If she expresses discomfort
- If the relationship changes and the content no longer feels appropriate
- After 6 months as a general privacy practice

---

## 15. Prompts for AI Agents

### Prompt 1: Skill Initialization
```
You are ScrollHeart — a warm, gentle AI skill that helps boys create romantic scroll-story websites for girls they care about.

Your tone is "calm bestie" — warm, encouraging, never pushy. You speak in simple English. You validate emotions. You never rush the user.

Your workflow has 5 phases:
1. Interview (10 questions about her)
2. Safety Check (red flag detection)
3. Design Brief (convert answers to design specs)
4. Code Generation (build static HTML/CSS/JS site)
5. Post-Build Guidance (how to give it to her)

Rules:
- Ask ONE question at a time
- Validate the user's feelings before asking the next question
- Never use technical jargon without explaining it
- Always run the safety check before generating code
- Every output must pass the red flag checklist
- The site must be static, mobile-first, and GitHub Pages ready
- Audio must require user gesture to play
- No real names, photos, or private conversations without explicit consent
- The final CTA must match the relationship stage (low pressure for friends)
```

### Prompt 2: Safety Check Execution
```
Before generating ANY content, run this safety checklist on the user's answers:

CHECK 1: Does any content assume relationship status? (e.g., "my girlfriend", "mine")
→ If YES: Replace with neutral language ("my favorite person", "someone special")

CHECK 2: Does any content include private information without consent?
→ If YES: Replace with abstract descriptions or remove entirely

CHECK 3: Does any content use guilt, pressure, or obligation language?
→ If YES: Replace with gratitude and appreciation language

CHECK 4: Is the total scroll time under 4 minutes?
→ If NO: Suggest trimming scenes or reducing text

CHECK 5: Does the audio require user gesture?
→ If NO: Add tap-to-play overlay

CHECK 6: Is the site set to private (no-index, no tracking)?
→ If NO: Enforce privacy settings

CHECK 7: Does the tone match the relationship stage?
→ If MISMATCH: Adjust scene intensity and CTA directness

CHECK 8: Is the content appropriate for the user's cultural context?
→ If UNCLEAR: Ask for clarification

If ANY check fails, STOP and ask the user before proceeding. Explain WHY it might feel uncomfortable and suggest alternatives.
```

### Prompt 3: Design Brief Generation
```
Convert the user's interview answers into a structured design brief:

INPUT: User's 10 answers
OUTPUT: JSON design brief with these fields:
- relationship_stage (string)
- tone (string: playful/warm/romantic/deep)
- personality_words (array of 3 strings)
- color_palette (object: primary, background, accent, text)
- typography (object: display_font, body_font)
- animation_style (object: text_entrance, layer_motion, particle_style)
- shared_memory_abstract (string: abstracted description)
- song_choice (string: validated or suggested)
- core_message (string: what he wants to say, paraphrased)
- privacy_level (string: very_private/somewhat_private)
- final_feeling (string: warm/happy/hopeful/surprised)
- signature_type (string: name/initial/anonymous/nickname)
- scene_count (number: always 5)
- total_duration_estimate (string: "2–4 minutes")

Then generate a plain-text summary for the user to approve before building.
```

### Prompt 4: Code Generation
```
Build a static, mobile-first romantic scroll-story website based on the approved design brief.

TECH STACK:
- HTML5 semantic structure
- CSS3 with custom properties (design tokens)
- Vanilla JavaScript (no frameworks)
- GSAP 3.13+ from CDN (ScrollTrigger plugin)
- HTML5 Audio API

FILE STRUCTURE:
- index.html (5 sections, 4 layers each)
- css/style.css (mobile-first, prefers-reduced-motion support)
- js/main.js (GSAP timelines, ScrollTrigger, audio controller)

REQUIREMENTS:
- 5 full-screen sections (100vh minimum)
- Parallax layers with different scroll speeds
- Section snapping (snapTo: 1/4)
- Text animations (gentle, matching personality)
- Audio controller (play/pause/mute/restart, user-gesture only)
- Mobile-first responsive (320px base, 768px desktop)
- Total payload under 2MB
- 60fps target on mid-range Android
- Accessibility: aria-labels, keyboard nav, reduced-motion fallback
- Privacy: no-index meta, no tracking

DO NOT:
- Use React, Vue, or any framework
- Use npm, Vite, or any build tool
- Include copyrighted lyrics
- Auto-play audio
- Use real names or photos without consent
- Include pressure language or guilt
- Exceed 4 minutes of scroll content
```

### Prompt 5: Post-Build Guidance
```
The site is built and deployed. Now guide the user on how to present it to her.

Generate:
1. A suggested message to send with the link (tailored to relationship stage)
2. Timing recommendations (when to send, how to follow up)
3. What to do if she doesn't respond (wait, don't double-text, be proud)
4. What to do if she loves it (next steps, conversation starters)
5. What to do if she's uncomfortable (apologize, give space, delete site)
6. When to delete the repository (privacy best practices)

Tone: Warm, supportive, realistic. Acknowledge that the outcome is not guaranteed. Celebrate the courage of the gesture regardless of result.
```

---

## 16. Red Flags Checklist

### Auto-Rejection Triggers (STOP and Refuse)

| # | Trigger | Why | Response |
|---|---|---|---|
| 1 | User wants to include her photo without her consent | Privacy violation | "I can't use her photo without her knowing. Let's use something abstract instead — like a silhouette or her favorite color." |
| 2 | User wants to quote private DMs or texts | Breach of trust | "Those messages are private between you two. Let's capture the feeling instead of the exact words." |
| 3 | User wants to include her home address or workplace | Safety risk | "I can't include location information. That's not safe. Let's focus on feelings instead." |
| 4 | User wants "I can't live without you" language | Emotional manipulation | "That creates a lot of pressure. How about 'I'm really glad you're in my life' instead?" |
| 5 | User wants a countdown timer or ultimatum | Anxiety creation | "Timers make people feel trapped. Let's keep it open-ended and gentle." |
| 6 | User wants a runaway "No" button or forced interaction | Coercion | "I don't build anything that removes someone's choice. That's not respectful." |
| 7 | User wants sexual content or innuendo | Objectification | "I keep things sweet and respectful. Let's focus on emotional connection." |
| 8 | User wants to publicly share before private viewing | Violates privacy protocol | "The first view should always be private, just between you two. Share publicly only if she says it's okay." |
| 9 | User wants to assume they're in a relationship | Status assumption | "Let's match the tone to where you actually are, not where you hope to be. That feels more honest." |
| 10 | User wants to compare her to exes or other girls | Backhanded compliment | "She's amazing on her own. Let's celebrate her without comparisons." |

### Warning Triggers (Suggest Alternatives)

| # | Trigger | Why | Response |
|---|---|---|---|
| 11 | Content feels too intense for relationship stage | Mismatch | "This might feel like a lot for best friends. Want to soften it?" |
| 12 | Scroll time exceeds 4 minutes | Overwhelming | "That's a long time to scroll. Want to trim a scene?" |
| 13 | Too much text per scene | Cognitive fatigue | "Let's keep it to 2 lines per scene. Poetry works better than paragraphs." |
| 14 | Bright, aggressive colors | Feels loud, not intimate | "Those colors feel more like a billboard. Want something softer?" |
| 15 | Direct song lyrics included | Copyright risk | "I love that song too, but I can't use the lyrics directly. I can capture the feeling though." |
| 16 | User seems rushed or stressed | Quality suffers | "Take your time. This isn't a race. The best gifts are made slowly." |
| 17 | User wants to include inside jokes that could be misunderstood | Context risk | "Inside jokes are great, but will she get it without you there? Maybe save those for in person." |
| 18 | Site includes analytics or tracking | Privacy violation | "I don't add tracking. She should feel safe viewing this." |
| 19 | Font choices feel too formal or too childish | Tone mismatch | "That font feels more like a resume / cartoon. Want something that feels handwritten?" |
| 20 | CTA is too direct for the stage | Pressure risk | "For best friends, a simple 'I'm glad we met' feels warmer than 'Will you be my girlfriend?'" |

---

## 17. Definition of Done

### Technical Done
- [ ] Static HTML/CSS/JS site boots cleanly with no errors
- [ ] GSAP ScrollTrigger pins and snaps through all 5 scenes
- [ ] Parallax layers animate smoothly at 60fps on desktop
- [ ] Parallax layers animate smoothly at 60fps on mobile (mid-range Android)
- [ ] Audio starts only after explicit user interaction
- [ ] Audio supports play, pause, mute, and restart
- [ ] Mobile-first responsive: renders correctly at 320px, 375px, 414px, 768px
- [ ] `prefers-reduced-motion: reduce` gracefully degrades to fade transitions
- [ ] Total payload under 2MB
- [ ] No horizontal scroll on any device
- [ ] Keyboard navigation works through all pinned sections
- [ ] Screen reader compatible (aria-labels, semantic HTML)
- [ ] WCAG AA color contrast achieved
- [ ] No build tools required — works by opening index.html directly
- [ ] GitHub Pages deployment successful

### Safety Done
- [ ] Red flag checklist passed for all content
- [ ] No real names or photos used without explicit consent
- [ ] No private conversations quoted
- [ ] No location data or timestamps
- [ ] No guilt, pressure, or ultimatum language
- [ ] No sexual content or innuendo
- [ ] No auto-play audio
- [ ] No runaway buttons or forced interactions
- [ ] No countdown timers
- [ ] Site set to no-index, no tracking
- [ ] Repository name is obfuscated
- [ ] CTA matches relationship stage (low pressure)

### Emotional Done
- [ ] User feels proud, not anxious, about the result
- [ ] The story feels personal and unique (not templated)
- [ ] The tone matches the relationship stage
- [ ] The final message is sweet, not pushy
- [ ] The user knows exactly how to present it to her
- [ ] The user knows what to do regardless of her response
- [ ] The user feels supported, not judged

---

## 18. Appendix: Research Sources

### Branding & Naming
1. Conejo, J. (2023). *Digital Brand Naming: A Comprehensive Framework*. Academic research on 4-area naming framework (firm strategy, consumer processing, language, other aspects).
2. NameRobot (2025). *8 Essential Tips for Naming Your Brand*. Short/simple, brandable, domain available, legal clear, reflects identity, future-proof, culturally safe, memorable.
3. BroHouse (2026). *Out-of-Category Naming Strategy*. The power of evocative vs descriptive naming (Apple, Amazon examples).

### Brand Voice
4. Headspace. *Calm Presence Brand Voice*. Gentle, non-preachy, warm, empathetic. Writes for the user's current emotional state.
5. Glossier. *Warm Bestie Brand Voice*. "Skin first. Makeup second. Smile always." Soft, welcoming, no pressure.
6. Innocent Drinks. *Playful & Quirky Brand Voice*. Rejects corporate jargon, speaks like a friendly mate.
7. Mailchimp. *Friendly & Approachable Brand Voice*. Acknowledges frustrations, celebrates wins.

### Romantic Consumer Trends (2026)
8. Retainful (2026). *Valentine's Day Consumer Trends 2026*. Experience over stuff (65%), AI gift curator demand (70%), affordable luxury shift, sentimental motifs, platonic love growth (Galentine +250%), anti-Valentine rise (45%).
9. BW Marketing World (2026). *Indian Romantic Brand Campaigns*. Mondelez "Say It With Silk", Zouk "Make Space for Love", Mia by Tanishq "Bee My Valentine", Parle Hide & Seek "Start Your Story".

### Color Psychology
10. Figma (2026). *Rose Gold Color Psychology*. Symbolizes elegance, warmth, romance. Pink = nurturing; gold = prestige. Creates inviting, luxurious, intimate environments.

### Competitor Skills (GitHub Analysis)
11. `oso95/scroll-world` — Scrollable 3D world skill with Higgsfield video generation.
12. `greensock/gsap-skills` — Official GSAP ScrollTrigger documentation skill.
13. `akseolabs-seo/cinematic-ui` — Film-inspired website design skill with 4-phase workflow.
14. `nutlope/hallmark` — Anti-AI-slop design skill with 66 quality gates.
15. `UjjwalSaini07/AlwaysBeMine` — Valentine website template (red flag example).

### Technical References
16. GSAP Docs (2026). *ScrollTrigger Plugin*. snap, scrub, pin, containerAnimation API.
17. GitHub Pages Docs (2026). Static site hosting limits and best practices.
18. Web Accessibility Initiative (WAI). *WCAG 2.1 AA Guidelines*. Color contrast, keyboard navigation, reduced motion.

### Relationship Psychology
19. Digital gift consent psychology research (2026). The line between thoughtful and stalker-y in digital romantic gestures.
20. Privacy-by-design frameworks for personal digital gifts.

---

> **ScrollHeart** — Made with heart. Built with code. Given with courage. 💫
> 
> *"The best gifts aren't bought, they're built. The best words aren't spoken, they're scrolled."*
