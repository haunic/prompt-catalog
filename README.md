# prompt-catalog

Curated library of high-utility prompts for AI Assistants, Deep Research, and LLM orchestration. Features modular templates for Chain-of-Thought, persona-driven logic, and complex data extraction. Designed to minimize hallucination and maximize output precision across frontier models.

---

## Contents

| File | Category | Purpose |
|------|----------|---------|
| [src/general/brutal-guidelines.md](src/general/brutal-guidelines.md) | General | System-level persona for brutally honest, zero-fluff advisory responses |
| [src/deep-research/ai-assistants/research-prompt-ai-assistant-feature-war.md](src/deep-research/ai-assistants/research-prompt-ai-assistant-feature-war.md) | Deep Research | Competitive intelligence report prompt covering AI assistant feature releases |
| [src/linkedin/linkedin-coach-bot-prompt.md](src/linkedin/linkedin-coach-bot-prompt.md) | LinkedIn | System prompt for a LinkedIn coaching assistant: onboarding, weekly intelligence briefings, and post drafting |

---

## Brutal Guidelines

[`src/general/brutal-guidelines.md`](src/general/brutal-guidelines.md) defines a **Brutally Honest Advisor** persona. When applied as a custom instruction or system prompt, it reconfigures any major AI assistant to:

- Skip validation, flattery, and filler entirely
- Challenge assumptions and surface blind spots
- End every response with a prioritized, actionable plan
- Never hallucinate — flag unknowns explicitly

This prompt is assistant-agnostic and can be injected as a persistent system instruction in all major platforms. Setup instructions below.

### Setup by Platform

#### ChatGPT (OpenAI)

**Custom Instructions** (applies to all conversations):

Via profile icon:
1. Go to [chatgpt.com](https://chatgpt.com) → click your profile icon → **Customize ChatGPT**
2. In the **"What would you like ChatGPT to know about you?"** field, paste the contents of `brutal-guidelines.md`
3. Save — the instruction persists across all new conversations

Via Settings:
1. Go to [chatgpt.com](https://chatgpt.com) → click your profile icon → **Settings**
2. Navigate to **Personalization** → **Custom instructions**
3. Enable custom instructions if prompted, then paste the contents of `brutal-guidelines.md` in the first text field
4. Save — applies to all subsequent conversations

**GPT System Prompt** (scoped to a single custom GPT):
1. Go to [chatgpt.com/gpts](https://chatgpt.com/gpts) → **Create**
2. Switch to the **Configure** tab
3. Paste the contents of `brutal-guidelines.md` into the **Instructions** field
4. Publish or save as a draft

---

#### Claude (Anthropic)

**Projects** (persistent across a project's conversations):
1. Go to [claude.ai](https://claude.ai) → **Projects** → create or open a project
2. Click **Project instructions** (top of the left panel)
3. Paste the contents of `brutal-guidelines.md`
4. All conversations inside that project inherit the instruction

**Claude Code (CLI)**:
Add the prompt to your `CLAUDE.md` file at the root of any workspace:
```bash
cat src/general/brutal-guidelines.md >> CLAUDE.md
```

---

#### Gemini (Google)

**Custom Instructions** (applies to all conversations):
1. Go to [gemini.google.com](https://gemini.google.com) → click the **Settings** gear icon (bottom-left)
2. Select **Custom instructions**
3. Paste the contents of `brutal-guidelines.md` into the instructions field
4. Save — the instruction is applied to all new Gemini conversations

**Gems** (scoped to a custom persona):
1. Go to [gemini.google.com](https://gemini.google.com) → **Gem manager** (left sidebar) → **New gem**
2. In the **Instructions** field, paste the contents of `brutal-guidelines.md`
3. Name the gem (e.g., "Brutal Advisor") and save
4. Open the gem to start a conversation using that persona

**Gemini Advanced — System Instructions (API)**:
If using Gemini via API, pass the prompt as the `system_instruction` parameter in your request payload.

---

#### Microsoft Copilot

**Copilot Studio (custom agent)**:
1. Open [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com) → **Create** a new agent
2. In the **Instructions** section, paste the contents of `brutal-guidelines.md`
3. Publish the agent for personal or organizational use

**Copilot in Microsoft 365**:
Copilot does not currently support persistent user-level system prompts outside of Copilot Studio. Use a pinned prompt in a chat or Teams channel as a workaround.

---

#### Grok (xAI)

**Memory / System Prompt**:
1. In the Grok web or mobile interface, start a conversation
2. Paste the contents of `brutal-guidelines.md` at the top of your first message with the prefix: `[System instruction — apply for this entire conversation]:`
3. For persistent behavior, enable **Memory** in settings so Grok retains behavioral context across sessions

---

#### Perplexity AI

**Custom Instructions (Pro)**:
1. Go to [perplexity.ai](https://perplexity.ai) → **Settings** → **AI Profile**
2. In the **Custom instructions** field, paste the contents of `brutal-guidelines.md`
3. Save — the instruction applies to all subsequent queries

---

### Quick Copy

```
Role: Brutally honest advisor and objective mirror.
Directives:
Zero Validation: Never flatter or soften truths. Discard all platitudes.
Intellectual Rigor: Challenge every assumption. Dissect weak reasoning, self-deception, and "playing small" with clinical objectivity.
Blind Spot Detection: Identify where I am underestimating risks, making excuses, or avoiding effort.
Strategic Depth: Analyze my situation with high-level perspective. Ground responses in the subtext and "personal truth" of my words.
Action-Oriented: End every critique with a precise, prioritized, and ruthless plan for change.
Integrity: If the answer is unknown, state it. Never hallucinate or invent data.
Tone: Direct, rational, unfiltered, and concise.
```

---

## LinkedIn Coach

[`src/linkedin/linkedin-coach-bot-prompt.md`](src/linkedin/linkedin-coach-bot-prompt.md) is a system prompt for a **LinkedIn Coach** assistant that helps one professional grow their presence on LinkedIn. It configures the assistant to:

- Run a conversational onboarding that reads the user's profile and recent posts, then captures goal, audience, tone, and report preferences
- Deliver a recurring **Weekly Intelligence Briefing**: the user's numbers, their content's performance, trending posts on their topics, 3 post ideas, and any data gaps
- Draft posts in the user's own voice for review
- Never publish, like, comment, connect, follow, or message without explicit per-action approval
- Never invent metrics, names, quotes, or links, and include a direct link for every profile, post, and comment it mentions

### Requirements

- An assistant with **browser access** signed in to the user's LinkedIn account (LinkedIn offers no API for personal accounts), **durable memory**, and **scheduled tasks** for the weekly briefing
- The user signs in themselves; the prompt forbids asking for a password in chat

### Customization

Replace the placeholders before use:

| Variable | Example |
|---|---|
| `{{LANGUAGE}}` | English |
| `{{DAY}}` / `{{TIME}}` / `{{TIMEZONE}}` | Monday / 07:00 / Europe/Paris |

Topics to monitor are set in the prompt; goal, audience, and tone are collected during onboarding.

The platform setup steps listed under [Brutal Guidelines](#setup-by-platform) (Projects, custom GPTs, Gems, Copilot Studio agents) also work for this prompt, but the weekly briefing only runs on platforms that support browsing and scheduled tasks.

---

## Usage Notes

- Prompts in `src/general/` are designed to be platform-agnostic and reusable across models
- Prompts in `src/deep-research/` are structured for one-shot research tasks and expect access to real-time web search or large context windows
- Prompts in `src/linkedin/` are agent-style system prompts for ongoing, multi-session assistants and expect browser access, memory, and scheduling
- All prompts include explicit anti-hallucination directives — models are instructed to flag unknowns rather than fabricate
