<div align="center">
  <img src="assets/scrollheart-logo.png" alt="ScrollHeart Logo" width="200"/>
  <h1>ScrollHeart</h1>
  <p><em>Build her a story she can scroll through.</em></p>
  <p>A warm, gentle AI skill that helps a boy create a romantic, scroll-driven storytelling website for a girl he cares about.</p>
</div>

---

## 📖 What This Project Is

**ScrollHeart** is an AI-powered skill system that helps you create a personalized, romantic, scroll-driven storytelling website. The entire experience is built inside an AI IDE (Antigravity, Claude Code, Cursor, Windsurf, etc.) through a friendly, conversational workflow.

### Features
- **Conversation-first:** Asks about HER, not about the project.
- **Safety-first:** Auto-detects and rejects creepy/pushy content.
- **Story-first:** Builds around an emotional arc, not a generic template.
- **Privacy-first:** Private link, no tracking, no public sharing by default.
- **Zero Build Tools:** Generates pure HTML/CSS/JS that can be hosted for free on GitHub Pages.
- **Mobile-first:** Responsive design with GSAP ScrollTrigger animations, parallax layers, and optimal performance under 2MB.

---

## 🚀 How to Use ScrollHeart with Different AI Agents

ScrollHeart is compatible with multiple AI coding agents. Follow the instructions for your IDE to get started.

### 🌌 Antigravity IDE
Antigravity automatically discovers skills in the `.agents/skills` directory.
1. Open this project in Antigravity.
2. In the chat, simply mention building a romantic website (e.g., "I want to build a ScrollHeart site for my girlfriend").
3. The skill will trigger and begin the 5-phase workflow automatically.

### 🤖 Claude Code
1. Start Claude Code in the project root.
2. The `CLAUDE.md` file will direct Claude to read the `SKILL.md` entry point.
3. Prompt: "Let's start the ScrollHeart skill to build a website."

### 🖱️ Cursor
Cursor uses the `.cursor/rules/scrollheart.mdc` rule file.
1. Open the workspace in Cursor.
2. Open the Composer or Chat.
3. Type: "I want to make a surprise scroll story for her."
4. Cursor will apply the rule and follow the workflow.

### 🏄‍♂️ Windsurf
1. Open the workspace in Windsurf.
2. The `.windsurf/rules/scrollheart.md` file defines the triggers.
3. Ask the AI: "Help me create a digital love letter with ScrollHeart."

### Other Agents (Codex, etc.)
Any agent that supports `llms.txt` can understand this skill. Just point it to the root directory and ask it to follow the `SKILL.md` instructions.

---

## 🛠️ The 5-Phase Workflow

When you trigger ScrollHeart, the AI acts as "The Calm Bestie" and guides you through:

1. **Interview:** 10 conversational questions about her personality, memories, and preferences.
2. **Safety Check:** Evaluates answers against a "Green Flag" commitment to prevent pushy, creepy, or guilt-inducing language. 
3. **Design Brief:** Generates a custom design spec (colors, fonts, animation style) based on your answers for your approval.
4. **Code Generation:** Builds a static HTML/CSS/JS site with GSAP ScrollTrigger (5 scenes).
5. **Post-Build Guidance:** Coaches you on how to host it on GitHub Pages and how to present the gift gracefully.

---

## 🎨 Scene & Narrative Structure

The generated websites follow a 5-scene emotional arc:
1. **The First Glance (Intro):** Setting the mood with light curiosity.
2. **The Silent Conversation (Verse):** Building context and sharing a memory.
3. **The Climax (Chorus):** The emotional peak and core message.
4. **Quiet Night (Bridge):** A reflective, quiet perspective shift.
5. **Outro & CTA (Finish):** A gentle, no-pressure conclusion.

Each scene uses 4 parallax layers (Background, Midground, Foreground, Text) driven by the user's scroll.

---

## 🛡️ Emotional Safety Framework

We believe the best gifts aren't bought, they're built—and they should always feel safe. ScrollHeart includes a 20-point Red Flag Detection Algorithm. 

**ScrollHeart will NEVER:**
- Assume she owes you a response.
- Use guilt language or pressure.
- Include private information (real names/photos) without explicit consent.
- Create overwhelming length or use countdown timers.
- Auto-play audio loudly.

**ScrollHeart will ALWAYS:**
- Suggest gentler alternatives when things feel too intense.
- Put her in control of the pacing via scroll-driven storytelling.
- Include a no-pressure CTA (e.g., "Replay the story").
- Respect privacy by disabling search indexing and analytics.

---

## 📁 Repository Structure

- `SKILL.md` — The core AI skill instruction file.
- `AGENTS.md` — Universal rules for AI agents.
- `references/` — Progressive loading files for the 5-phase workflow (Interview, Safety, Design, Code, Deployment).
- `resources/` — Curated JSON data for color palettes, font pairings, and song suggestions.
- `examples/` — A complete reference implementation of a ScrollHeart story.

---

<div align="center">
  <p><em>Made with heart. Built with code. Given with courage. 💫</em></p>
</div>
