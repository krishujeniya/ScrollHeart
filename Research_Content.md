# Comprehensive Research Document

## Phase 1: Architecture & Technical Foundation

### A. Skill Architecture & Format (Learn from Competitors)

**1. SKILL.md YAML frontmatter standard:**
Modern AI coding agents (like Claude Code, Cursor, Codex, and Antigravity) use a standardized YAML frontmatter in `SKILL.md` files. This must include `name` and `description` (which are used for trigger matching). Other optional but recommended keys include `allowed-tools`, `version`, and `author`. The body (Markdown) should contain instructions loaded *after* the skill triggers and should be kept under 500 lines for optimal context window performance.

**2. Reference file loading pattern:**
To maintain a small active context window, systems like `cinematic-ui` and `hallmark` use progressive loading. The primary `SKILL.md` file points to a `references/` directory. When an agent detects a specific phase (e.g., Phase 2: Animations), it is instructed to explicitly use tools (like `view_file` or `read_file`) to load `references/animations.md`, rather than having everything dumped into the initial prompt.

**3. Multi-platform compatibility files:**
Different agents look for different rule files. For Cursor, rules live in `.cursor/rules/*.mdc` (using glob patterns for triggering). Windsurf uses `.windsurf/rules/`. Claude prefers `CLAUDE.md` in the root, while standard markdown files like `CODEX.md` or `GEMINI.md` are sometimes used. To be fully cross-compatible, a project should establish a unified global configuration (like `AGENTS.md`) and symlink or import it into platform-specific files.

**4. Skill index format (`llms.txt`):**
The `llms.txt` standard acts as a "sitemap for AI". It must be placed at the repository root and formatted in standard Markdown (UTF-8). It typically includes an `<h1>` header, a blockquote summary, and categorized markdown links (`- [Title](URL) - Description`) pointing to key documentation. An optional `llms-full.txt` can consolidate the entire documentation base into one file for single-shot ingestion.

**5. Plugin vs rule vs skill distinction:**
- **Cursor Rule:** Context-injected constraints triggered by glob file matches (e.g., "always use Tailwind when editing `*.tsx`").
- **Claude Plugin / Antigravity Skill:** An active toolset extending agent capabilities. Skills contain instructions (`SKILL.md`) but also include actionable scripts (`scripts/`), templates (`resources/`), and examples (`examples/`).
- **Codex Skill:** Often functions as a declarative instruction set for code generation within IDEs.

**6. Project memory / log.json pattern:**
To avoid repetitive designs (diversification), systems like `hallmark` utilize a `log.json` or `.project-memory` file. Before generating a new design, the agent reads this file to see previous color palettes, animations, and typography choices, actively ensuring the new output differs significantly from historical outputs.

**7. Pre-flight scan methodology:**
Before generating any code, a robust skill instructs the agent to perform a "pre-flight scan." This involves using tools to list directory contents, read `package.json` to identify installed dependencies (e.g., React vs Vanilla, GSAP versions), and checking global CSS tokens to understand the existing design system.

**8. Verb-based invocation:**
Rather than waiting for a conversational prompt, advanced skills support CLI-like verb invocations (e.g., `hallmark audit`, `hallmark redesign`, `hallmark study`). The skill file maps these verbs to specific execution pipelines, standardizing the agent's behavior based on the command intent.

**9. Component-scope vs page-scope detection:**
The skill must instruct the agent to evaluate the user's brief. If the user asks for a "button," the agent restricts context and edits to the component scope. If the request is for a "landing page," it widens the scope to include layout modules, global state, and routing.

**10. Self-critique / slop-test gate pattern:**
A post-emit quality checklist. Before presenting code to the user, the agent is instructed to internally review its work against a rubric (the "slop-test"). Checks include: "Are there hardcoded magical numbers?", "Is the animation relying on JavaScript when CSS suffices?", "Did I include `will-change` for performance?".

### B. GSAP ScrollTrigger 2026 (Technical Foundation)

**11. GSAP 3.13+ ScrollTrigger latest API:**
GSAP 3.13 made all premium plugins, including ScrollTrigger, free to use. Recent APIs focus heavily on performance. Key properties include `snap` (for magnetic scroll sections), `scrub` (linking animation progress directly to scrollbar position), `pin` (locking elements in place while scrolling continues), and `containerAnimation` (triggering animations within a horizontally scrolling pinned container).

**12. ScrollTrigger mobile pinning performance:**
Mobile pinning is notoriously difficult due to dynamic browser UI (URL bars shrinking/expanding) changing the `100vh` calculation.
- **Best Practice:** Use `ScrollTrigger.normalizeScroll(true)` to sync scroll thread with main thread. 
- Use `anticipatePin: 1` to prevent visual jumps during quick scrolls.
- Use `pinType: "transform"` instead of `"fixed"` on mobile when inside nested scrollers, though `"fixed"` is generally better for the main window.

**13. Section snapping best practices:**
When snapping between sections, avoid arbitrary fractional snapping (e.g., `snapTo: 1/4`) unless layout heights are perfectly rigid. Instead, use label-based snapping (`snap: "labels"`) or array-based element snapping. Always configure `snap: { snapTo: "labels", duration: { min: 0.2, max: 0.8 }, ease: "power1.inOut" }` for fluid UX.

**14. Parallax layer architecture:**
For realistic parallax, structure elements into discrete depth layers using speed offsets:
- Background: Very slow (`data-speed="0.2"`).
- Midground: Moderate (`data-speed="0.5"`).
- Foreground/Subject: Natural (`data-speed="1.0"`).
- Overlay elements: Fast (`data-speed="1.5"`).
Map these `data-speed` attributes to GSAP `yPercent` or `y` translations in a `ScrollTrigger.batch()` or loop.

**15. ScrollTrigger + Lenis smooth scroll integration:**
Lenis is the 2026 standard for smooth scrolling. To integrate with GSAP, avoid legacy `scrollerProxy`. Instead, sync Lenis with GSAP's ticker:
```javascript
const lenis = new Lenis()
lenis.on('scroll', ScrollTrigger.update)
gsap.ticker.add((time) => { lenis.raf(time * 1000) })
gsap.ticker.lagSmoothing(0)
```

**16. Horizontal scroll with vertical scroll:**
To create a fake horizontal scroll section while scrolling vertically:
Pin the main container, translate the inner track along the X-axis (`xPercent: -100`), and use `containerAnimation` on child elements to trigger animations based on the horizontal progress, not the vertical scrollbar.

**17. ScrollTrigger cleanup in static sites:**
Without frameworks like React (which handle unmounting), single-page static sites navigating via AJAX or standard links must manually clean up GSAP. Always assign triggers to a variable or context (`let ctx = gsap.context()`) and explicitly call `ctx.revert()` or `ScrollTrigger.getAll().forEach(t => t.kill())` before DOM destruction to prevent memory leaks.

**18. GSAP matchMedia() for responsive breakpoints:**
Do not use CSS `@media` queries to try and override GSAP inline styles; it will cause conflicts. Use `gsap.matchMedia()`:
```javascript
let mm = gsap.matchMedia();
mm.add("(min-width: 800px)", () => {
  // Desktop animations
});
mm.add("(max-width: 799px)", () => {
  // Mobile animations (often simplified or killed)
});
```

**19. GSAP ScrollTrigger.batch():**
Ideal for staggered reveals of multiple identical elements (like a grid of images). `ScrollTrigger.batch(".card", { onEnter: elements => gsap.to(elements, { opacity: 1, stagger: 0.15 }) })` batches DOM queries and animations efficiently based on scroll position, heavily reducing CPU load compared to individual triggers.

**20. GSAP performance on mid-range Android:**
To maintain 60fps on low-to-mid tier devices:
- Never use `scroll-behavior: smooth` in CSS.
- Apply `will-change: transform` to animated elements.
- Animate ONLY `transform` (x, y, scale, rotation) and `opacity`. Never animate `width`, `height`, `top`, `left`, or `box-shadow` with ScrollTrigger, as they trigger expensive layout recalculations.

### C. Mobile-First Static Architecture (GitHub Pages Ready)

**21. GitHub Pages 2026 constraints:**
GitHub Pages remains purely static (no server-side Node.js/PHP). The repository limit is typically 1GB, and bandwidth is soft-capped at 100GB/month. Jekyll processing is enabled by default but should be bypassed with a `.nojekyll` file for modern pure-static builds to avoid ignoring files starting with underscores.

**22. `dvh` / `svh` / `lvh` viewport units:**
Mobile browsers dynamically hide/show URL toolbars. Do not use `vh` as it causes layout shifts. Use `svh` (Small Viewport Height) for fixed elements that must always be visible, `lvh` (Large) when you want it to fill the screen behind transparent UI, and `dvh` (Dynamic) for responsive heights, though `dvh` can trigger expensive repaints on scroll.

**23. Touch event vs wheel event:**
Mobile scrolling relies heavily on `touchmove` and `touchstart`. Relying solely on `wheel` events for custom scroll logic will break on mobile. Always map custom scroll interactions to touch events, or rely on native scroll-linked animations (`@scroll-timeline` or ScrollTrigger) to avoid hijacking native touch momentum.

**24. `prefers-reduced-motion` implementation:**
Romantic designs often use heavy parallax. For accessibility, detect `(prefers-reduced-motion: reduce)`. If true, bypass GSAP ScrollTriggers and fallback to graceful degradation: simple CSS opacity crossfades (≤150ms) instead of spatial translations.

**25. iOS Safari safe area insets:**
To prevent text from hiding under iPhone notches or the home indicator, use CSS environment variables: `padding-top: env(safe-area-inset-top);` and `padding-bottom: env(safe-area-inset-bottom);`. 

**26. Service Worker for offline viewing:**
For a "she can view it anytime" guarantee, implement a Service Worker using Workbox. Use a Cache-First strategy for audio and images. Critical: `blob:` URLs cannot be cached directly. Use `workbox-range-requests` to ensure audio seeking (range requests) functions correctly locally.

**27. No-build static site structure:**
Avoid complex bundlers (Webpack/Vite) for micro-experiences to keep the project portable. Use a flat structure: `index.html`, `/css/style.css`, `/js/main.js`, and `/assets/`. Use native ES Modules (`<script type="module">`) if importing libraries via CDN.

**28. CSS-only animations where possible:**
Leverage CSS `@scroll-timeline` (widely supported in 2026) for simple scroll-linked animations to reduce JS payload. Reserve GSAP specifically for complex, sequenced, or physics-based animations.

**29. Image strategy for static sites:**
Instead of bloated JPEGs, use CSS gradients, SVGs, and WebP/AVIF formats. If using generative AI images, pre-compress them and utilize `picture` tags with `srcset` for resolution switching.

**30. Font loading strategy:**
Custom romantic fonts (like Dancing Script) must use `font-display: swap` to prevent invisible text during loading. Subset Google Fonts to include only the required characters if the text is static (e.g., `&text=Hello`). 

**31. Audio compression for static hosting:**
Keep MP3s under 128kbps, ideally utilizing Opus or AAC if browser support permits. Audio must be lazy-loaded and inherently requires a user gesture (a "play" or "begin" button) to comply with autoplay policies.

**32. Total payload budget:**
Aim for under 2MB total for 3G networks. Inline critical CSS directly into the `<head>` of `index.html` to achieve instant First Contentful Paint (FCP).

### D. Romantic Design Psychology & Color Science

**33. 2026 romantic color psychology:**
Avoid aggressive neons or standard web colors. "Romantic Realism" dictates nature-distilled palettes: warm gold, deep indigo, blush rose, midnight teal, and soft lavender. These evoke calmness, luxury, and intimacy.

**34. Typography that triggers safe intimacy:**
The typography should feel like a personal letter. Handwriting fonts (like Dancing Script) evoke raw emotion, while soft sans-serifs (like Outfit or Inter with loose tracking) feel "safe" and modern. Mix an expressive serif for headings with a clean sans for reading.

**35. Micro-interaction pacing:**
Animations dictate emotional tone:
- Fade = tenderness
- Typewriter = anticipation/thoughtfulness
- Scramble = nervousness
- Scale = a heartbeat
Keep transitions soft and easing functions natural (`power2.inOut`).

**36. Scene duration theory:**
A digital romantic experience should last 2–4 minutes total. Limit each scene to 20–40 seconds of interaction before moving on, preventing emotional fatigue and keeping the narrative moving.

**37. Bokeh, grain, noise textures:**
Pure digital gradients feel cold. Add CSS noise/grain (`mix-blend-mode: multiply` on a noise SVG) to simulate analog film. This tactile depth provides a "human-authored" feel.

**38. Dark mode as intimacy default:**
Light mode feels like a public billboard; dark mode feels like a whisper in a private room. Use midnight blue or deep charcoal (not pure #000000) as the default background.

**39. Text animation psychology:**
Entrance animations affect how the message is received. A slow upward drift implies a dream or memory, while character-by-character typing implies an active, present-tense confession.

**40. "Breathing room" between scenes:**
Negative space acts as emotional punctuation. Allow for blank, slow-scrolling sections between major text blocks so the user can process the emotion before reading the next line.

### E. Relationship Safety & Digital Consent

**41. Digital gift consent psychology:**
Digital gifts act as symbols of emotional connection but can trigger "receiver's anxiety" (feeling indebted or pressured to reciprocate). The UX must focus on the gesture itself, not the transactional value, to prevent the gesture from feeling "stalkery." The behavioral line is crossed when the gift demands immediate interaction or reciprocation rather than simply being an offering.

**42. Privacy-by-design for romantic gestures:**
A private digital gift must remain private. Ensure `no-index, no-follow` meta tags are present to prevent search engine indexing. Use obfuscated repository names (e.g., `project-starlight-88` instead of `for-sarah-love`) and strictly avoid third-party analytics (no Google Analytics, no Meta pixels) to ensure her visits aren't tracked.

**43. Public vs private viewing protocol:**
Provide the user with post-build instructions on how to share the link. It should never be blasted on a public timeline. The protocol should suggest sending it via direct message during a quiet time, emphasizing that she is the only one who has the link (1-on-1 only).

**44. Indian romantic gesture cultural context:**
In South Asian contexts, romance is often deeply tied to music (Bollywood tropes) and cultural timing (festivals, rainy season). Mixing languages (Hinglish/Roman Urdu) makes the digital experience feel authentic and personal, rather than a generic Western greeting card template.

**45. Age-appropriate content boundaries:**
A skill must detect the relationship stage. A "best friend" stage gesture should focus on shared memories, inside jokes, and lighthearted animations. Jumping straight to heavy romantic commitments can be jarring; the UX must calibrate the intensity of the copy and visuals accordingly.

**46. The "pressure gradient":**
The Call to Action (CTA) at the end of the site should scale based on relationship depth.
- Crush: "Hope this made you smile." (No response required).
- Dating: "Let's get coffee this weekend." (Low pressure).
- Committed: A direct, heavy emotional question. (High pressure).

**47. Auto-play audio as consent violation:**
Never surprise a user with sound. Auto-play audio is not just blocked by modern browsers; psychologically, it feels invasive and breaks the safe environment. Always require a clear, voluntary user gesture (e.g., a beautiful "Begin Journey" button) to start music.

**48. "Runaway button" and forced interactions:**
Buttons that dodge the cursor when a user tries to click "No" (a common internet joke) are coercive, manipulative, and explicitly banned in romantic UX. Consent must be freely given, and rejection must be handled gracefully by the UI.

**49. Countdown timers and ultimatums:**
Do not use countdown timers (e.g., "Answer me in 5 minutes"). These create anxiety and simulate e-commerce scarcity tactics. Romantic UX should feel timeless and patient.

**50. Handling "no response" gracefully:**
The AI agent building the site must provide the user with emotional guidance post-deployment. If she doesn't respond immediately (due to differing "media ideologies"), the agent should advise the user to give her space and not double-text, reinforcing healthy relationship boundaries.

### F. Storytelling Structure for 5-Scene Romance Arc

**51. Joseph Campbell's Hero's Journey adapted for micro-narrative:**
Instead of a long epic, the Hero's Journey is condensed into a micro-narrative where the User (the receiver) is the Hero, and the UI is the Guide.
1. Call to Adventure (Intro): "I made something for you."
2. Crossing the Threshold: The user clicks "Begin" and music starts.
3. The Ordeal: A vulnerable confession or deep memory shared mid-scroll.
4. The Reward: A final beautiful realization or personalized message.

**52. Parallax layer theory (Narrative mapping):**
Map visual depth to narrative depth:
- Background (slow): Shared history, the passage of time.
- Midground (moderate): Current emotions, context.
- Foreground (fast): The immediate action, the "now".
- Text (static/fade): The inner voice guiding the hero through the journey.

**53. Audio-visual sync without copyrighted lyrics:**
Instead of relying on copyrighted lyrics, sync scene transitions to instrumental cues: tempo changes, beat drops, or the introduction of a new instrument (like a piano swelling) should trigger the next ScrollTrigger section.

**54. Song emotional arc mapping:**
Structure the 5 scenes to match a standard song structure:
- Scene 1 (Intro): Minimal UI, establishing the mood.
- Scene 2 (Verse 1): Context building, horizontal drift.
- Scene 3 (Chorus): The emotional peak, zoom emphasis, vibrant colors.
- Scene 4 (Bridge): A shift in perspective, depth separation, vulnerability.
- Scene 5 (Outro): Resolution, minimal motion, the final CTA.

**55. Scene transition patterns:**
Avoid jarring transitions like hard wipes or digital glitches. Romantic transitions rely on soft color washes (using `mix-blend-mode`), heavy Gaussian blurs (`backdrop-filter: blur`), and slow crossfades to mimic the feeling of a memory surfacing.

**56. Narrative pacing for scroll:**
Control the user's scroll speed indirectly via GSAP's `scrub` and section heights. Make the intro section very tall (300vh) to enforce a "slow drift," forcing the user to slow down their thumb and enter a calmer state of mind.

**57. Text content generation:**
To avoid copyright strikes on GitHub Pages, the AI should paraphrase the emotional themes of requested songs rather than copying lyrics verbatim, turning them into personalized poetic statements.

**58. Inside joke integration:**
Integrate inside jokes subtly in the background assets or as micro-copy (tooltips, small footer text) rather than making them the main heading. This makes the experience deeply personal without exposing private context out in the open.

### G. Accessibility in Emotional Web Experiences

**59. Screen reader narration for visual scroll stories:**
Since parallax relies heavily on visual storytelling, it is inherently inaccessible to visually impaired users unless correctly labeled. Use `aria-label` on sections, `role="img"` on visual containers, and `aria-live="polite"` regions for text reveals so screen readers narrate the story linearly as the user scrolls.

**60. Color contrast with soft romantic palettes:**
Romantic palettes often use low-contrast pastel tones (like blush pink on white), which fail WCAG AA compliance (requiring a 4.5:1 ratio). To fix this, use deeper accent colors (like dark burgundy or navy) for text, leaving the pastels for large decorative elements or backgrounds.

**61. Keyboard-only navigation through pinned sections:**
GSAP pinned sections can trap keyboard users if not careful. Ensure all interactive elements (like the "Next" button) have `tabindex="0"`. Use "Skip to Content" links, and ensure that pressing Space or Arrow Down smoothly scrubs the ScrollTrigger animation forward without breaking the pin.

**62. Cognitive load per scene:**
To prevent overwhelming users, limit cognitive load. Each scene should contain a maximum of 2 lines of text and 1 focal visual element. Too much text or complex overlapping animations create sensory overload, destroying the calm, intimate mood.

**63. Multi-language support:**
In diverse markets, allow for language mixing. Do not hardcode typography to assume English-only fonts. Use web-safe Unicode fallback fonts to seamlessly render Hinglish, Roman Urdu, or pure English without breaking layout widths.

**64. `prefers-reduced-motion` emotional alternative:**
Do not simply strip out animations and leave a broken layout. When `(prefers-reduced-motion: reduce)` is active, serve a "Static Layered Composition." Rely on subtle fades, high-quality static imagery, and strong typographical hierarchy to convey emotion without moving the layout space.

### H. AI Skill File Prompt Engineering

**65. Chain-of-thought prompting for creative coding:**
Instead of telling the AI "Build a romantic site," use `<thinking>` blocks. Force the agent to output a step-by-step design rationale (color choices, pacing, accessibility) *before* it generates a single line of code. This dramatically improves the emotional intelligence of the output.

**66. Self-correction loops:**
Implement a slop-test gate within the prompt. E.g., "After generating the code, review it. Did you use #000000? If yes, change it to a softer midnight blue. Did you use auto-play audio? If yes, wrap it in a user-gesture handler."

**67. Few-shot examples:**
Show the agent 2–3 examples of "good" vs. "bad" romantic site outputs inside the `references/` folder. Contrast a generic, template-like Valentine's site (bad) with a highly personalized, well-paced GSAP scroll story (good).

**68. Structured output formats:**
Enforce a pipeline: The agent must first output a `JSON design brief`, wait for approval, output a `Markdown plan`, and only then emit the `HTML/CSS/JS code pipeline`.

**69. Context window management:**
For complex skills, respect the 8K-32K token limits by using progressive disclosure. The root `SKILL.md` should only hold the core loop, instructing the agent to dynamically `read_file` on `references/animations.md` only when the user reaches the animation stage of the build.

**70. Multi-turn conversation design:**
Instruct the agent to avoid interrogating the user. It should ask 1 or 2 conversational questions at a time (e.g., "What's a small detail you love about them?") rather than presenting a sterile 10-point intake form.

**71. Emotional validation in prompts:**
When a user shares a vulnerable detail for the site, the agent must validate it. "That's a beautiful memory to include" is better than "Data received. Processing." The agent's tone sets the user at ease.

**72. Progressive disclosure:**
Ask basic questions first (names, relationship duration) to build momentum. Save deep, intimate questions (shared secrets, emotional hurdles overcome) for later in the conversation when the user feels comfortable with the AI's guidance.

**73. Visual preference elicitation without jargon:**
Avoid asking users for "hex codes" or "font pairings." Instead, ask: "Does she prefer the feeling of a bright Sunday morning or a cozy midnight conversation?" The agent then maps "Sunday morning" to warm golds/serifs, and "midnight" to deep teals/sans-serifs.

**74. Handling "I don't know" answers:**
If a user is uncertain ("I don't know what song she likes"), the agent must provide graceful defaults or suggestions ("Many people use 'Yellow' by Coldplay or a soft instrumental jazz track. Should we try instrumental?").

### I. Content Generation & Personalization

**75. Randomization seeds based on user answers:**
To ensure no two outputs look identical, map user answers to generation seeds. E.g., if a user selects "Quiet Evening," the seed biases the GSAP animations toward slower scrubbing and selects a dark-mode-first color palette.

**76. Emotional tone calibration:**
The tone of the generated copy must shift based on intent. "Playful" implies bouncy GSAP `elastic` easing and bright accents. "Serious" implies `power2.inOut` easing, subdued colors, and poetic language.

**77. Song recommendation engine:**
Embed a mini-matrix of song suggestions in the skill's references. If the user wants "nostalgic," suggest acoustic tracks. If they want "epic," suggest cinematic instrumentals. Never leave the user stuck if they lack inspiration.

**78. Unique content every time:**
Utilize the AI's temperature settings to vary HTML structure and CSS class naming. Do not just fill in a static template. Each generation should uniquely structure the DOM based on the length and flow of the generated story.

**79. Nickname/initial generation:**
For privacy, suggest using initials or sweet nicknames ("S" or "Bubs") rather than full legal names. This makes the site feel more intimate and reduces privacy risks if the link is ever leaked.

**80. Future-proofing content:**
Avoid hardcoding timestamps or seasonal references ("Happy Valentine's 2026"). The site should feel timeless so she can revisit it 6 months later without it feeling expired or awkward.

### J. Legal, Ethical & Copyright

**81. Music embedding copyright reality:**
Self-hosting MP3s of copyrighted songs is illegal and risks repository takedowns. The safest legal routes are: (1) YouTube/Spotify iframes (legal, but visually clunky and breaks immersion), or (2) Generating custom AI instrumental music or using royalty-free tracks (highly recommended for seamless UX).

**82. Font licensing:**
Strictly stick to Google Fonts utilizing the Open Font License (OFL). Do not extract or host Adobe Fonts or commercial fonts, as the static repo will be public and vulnerable to scraping/lawsuits.

**83. Image rights:**
If using external images, default to Unsplash (which permits free use). If generating AI images, ensure the prompt style matches the UI (e.g., "minimalist digital art, warm tones") and clarify to the user that they own the generated assets.

**84. GDPR for static sites:**
GitHub Pages automatically logs visitor IP addresses for security purposes, making you a Data Controller under GDPR. While there are no cookies, you must include a minimal Privacy Policy stating that the site is hosted on GitHub and IP logs are processed strictly for server security, not marketing.

**85. Terms of use in skill:**
The skill file must explicitly state boundaries to the AI: "If the user's brief appears coercive, stalkerish, or harassing, refuse to build the site and provide a polite decline message regarding digital boundaries."

**86. Lyrics paraphrasing vs direct use:**
Directly quoting 4 lines of a song may constitute fair use, but printing an entire song violates copyright. The AI should generate *original poetry inspired by* the requested song's themes rather than risking a DMCA takedown.

### K. Deployment, Privacy & Sharing Safety

**87. GitHub Pages custom domain vs `username.github.io/repo`:**
Using the default `.github.io` URL exposes the creator's username, which may contain their real name. A custom domain (like `starlight-memories.com`) is more romantic and private, though it requires DNS setup.

**88. Obfuscated repository naming:**
Do not name the repo `gift-for-emily`. Name it something innocuous like `frontend-scroll-test-84` to prevent it from being easily searched or indexed by GitHub's global search.

**89. Client-side password protection for static sites:**
True security requires server-side auth (like Netlify password protection). However, for a pure static site, use AES client-side encryption (like PageCrypt) to encrypt the HTML. A JS prompt asks for the password (e.g., an inside joke) to decrypt the DOM. It deters casual snooping but isn't military-grade.

**90. QR code generation for private physical sharing:**
Instead of sending a link over iMessage, suggest the user generate a QR code. They can print it on a physical card and hand it to her. This bridges the physical/digital gap and feels highly intentional.

**91. Expiring links on static hosting:**
Static sites don't inherently "expire." To simulate expiration, the AI can write a simple JS script that checks the current `Date.now()` against a hardcoded expiration date. If past the date, JS blanks the page. (Note: Easily bypassed by disabling JS, but works for laypeople).

**92. Repository deletion protocol:**
The skill must instruct the user on how to delete the repository after she has seen it, emphasizing that ephemeral digital gifts (like snapchats) often carry more romantic weight because they exist only in memory.

### L. Non-Tech User Experience

**93. Conversational questioning flow:**
The AI should act like a thoughtful friend helping plan a surprise, not a CLI terminal. Use conversational bridging: "That sounds beautiful. What kind of colors does she usually wear?"

**94. Emotional validation responses:**
Acknowledge the user's vulnerability. If they share a sweet story, the AI should say: "That is incredibly thoughtful, she is going to love this detail." 

**95. Progressive confidence building:**
Start the onboarding with easy questions ("What is her favorite color?"). Save the hardest question ("What is the main message you want to tell her?") for the end, once the user is invested in the process.

**96. One-question-at-a-time vs batch:**
Never ask 5 questions in one prompt. Ask one question, wait for the user's response, validate it, and ask the next. This prevents cognitive overload.

**97. Default suggestions:**
Always provide an "easy out" to reduce decision paralysis. "If you aren't sure about the pacing, I can set it to a slow, dreamy rhythm. Sound good?"

**98. Explanation of technical choices:**
Hide the tech jargon. Instead of "I am using GSAP Scrub," tell the user: "I'm tying the animations to her scrolling, so she controls the pace of the story with her thumb."

**99. Preview before build:**
Before writing code, the AI must summarize the design brief: "Here is what we are building: A 5-scene dark-mode scroll story, paced slowly, ending with your message about the coffee shop. Ready for me to write the code?"

**100. Post-build guidance:**
Once the code is deployed, the agent’s final output should be coaching on how to present it. "Send this to her when you know she is relaxing at home. Tell her to turn her sound on and scroll slowly."
