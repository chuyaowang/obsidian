Below is a ready-to-paste PartyRock prompt that implements your full app concept. It’s written to be used as the _system/prompt description_ for PartyRock widgets and model chains, and includes precise instructions for each module (purpose, rules, audience, input widgets, output format, UX constraints). You can copy this into PartyRock and wire each widget to the corresponding LLM step.

---

# PartyRock App Prompt — **Counter-Procrastination Starter**

**Brief:** A low-effort, persona-driven micro-intervention app for people currently procrastinating. The app minimizes typing, uses dropdowns/checks/uploads, and produces (1) a brief reframe of negative thoughts, (2) a tiny starter plan + automatic task breakdown, (3) a time-boxed starter session, (4) a micro-reward image, and (5) a short personalized starter script / message. Include a “relapse” nudge option up front.

---

## Global Purpose

Help someone who is actively procrastinating to (a) recognize the feeling/thought pattern, (b) receive concise cognitive reappraisals, (c) get a concrete, tiny action plan they can immediately start, and (d) feel reinforced via a small reward cue — all with minimal typing.

## Global Rules (must be enforced by each widget / model call)

1. Keep all user-visible text **very short** by default (1–3 sentences) with optional “more info” toggle for clinical explanation.

2. Avoid medical/diagnostic language. Use supportive CBT-informed language (reframes, behavioral activation).

3. Prioritize actionability over theory. Every output must include a single next action the user can do in ≤10 minutes.

4. Respect persona tone setting. Provide tone variations for every output.

5. If user selects “I don’t want to type,” provide defaults and sample suggestions automatically.

6. Protect privacy: do not include persistent identifiers in generated messages. (Implementation note: store data encrypted on backend / follow your data policy.)

## Audience

- Primary: users who are actively procrastinating and want a quick intervention (low friction, short attention).

- Not for emergency/crisis situations; show a brief safety message if user enters crisis keywords (suicide, self-harm, severe distress).

---

# Modules (for each: Purpose • Rules • Audience • Inputs • Outputs • Prompt template)

---

## 0) Persona Selector (global)

**Purpose:** Choose style/tone for all subsequent messages.  
**Inputs:** Dropdown (Warm Therapist, Neutral Coach, Tsundere, Tough-Love, Playful Friend). Default = Neutral Coach.  
**Rule:** Every generated message must be stylistically adapted per persona but must remain kind and non-shaming. Tsundere may be playful/teasing but not insulting.  
**Output:** Short one-line persona confirmation.  
**Example output:** `Persona: Tsundere — "Ugh, finally? Fine, one tiny step then."`

---

## 1) Relapse Nudge (shown at app open)

**Purpose:** Normalize relapse and encourage use of the app quickly. This can be tapped before anything else.  
**Inputs:** Button: “I relapsed / I gave up earlier” (one tap).  
**Outputs:** One-sentence validation + one 60-second micro-starter (e.g., “Let’s do 60s reset — breathe & open project”), plus a gentle prompt to pick your persona or continue.  
**Prompt template to model:**

> If user taps relapse button, output 2 lines: (1) validation statement (e.g., “That happens — you’re not failing”), (2) one short 60-second starter action the user can do now. Tone = persona. Keep ≤30 words.

---

## 2) Task + Context Input

**Purpose:** Capture the concrete task and optional context without long typing.  
**Inputs:**

- Short text field (single line, optional): **Task title** (max 60 chars). Provide examples as chips (e.g., “Write function X”, “Draft Methods section”). If user leaves blank, offer 3 smart suggestions based on last used tasks or a generic list.

- File upload: optional context file (code snippet, doc, PDF, screenshot). Accept drag/drop. If provided, model may extract small context snippets. (RAG/short summary only.)  
    **Output:** Echo of the task name plus a short extracted context line (if file provided) or a chosen default context from suggestions.  
    **Rule:** No more than one short sentence returned; do not ask user to write long descriptions.

---

## 3) Feelings Dropdown

**Purpose:** Let user select current emotions they feel _while avoiding the task_ (not when thinking about it). Multiple select allowed.  
**Inputs:** Multi-select dropdown with icons. Options (common): Guilt, Shame, Anxiety, Overwhelm, Frustration, Restlessness, Hopelessness, Boredom, Tiredness, Embarrassment. Also “Other” → presets (choose one). Default none.  
**Output:** Short confirmation of chosen feelings. If user selects none, offer a “Not sure” quick pick.

---

## 4) Negative Thoughts — Category Dropdowns (low effort)

**Purpose:** Identify the thinking errors behind avoidance.  
**Inputs:** Multi-select from categorized lists (one tap per item). Categories mirror your earlier list: Perfectionism, Overwhelm/Size, Catastrophizing, Low self-belief, Devaluing task, Avoidance of discomfort, Fear of judgement, Comparative thinking, All-or-nothing time thinking, Disregarding prior evidence, Emotional reasoning, Mental filtering, Mind reading, Fortune telling, Should statements, Labeling, Personalization, Discounting the positive. Provide common short examples as chips under each category for 1-tap selection (e.g., under Perfectionism: “If it’s not perfect I shouldn’t start”).  
**Rule:** Limit to 6 selections max to keep output concise. If user selects >6, show a subtle tooltip: “Pick up to 6 — we’ll focus on the most important ones.”  
**Output:** Short list of the categories chosen.

---

## (UI Insert) Excuse Buster Quick Buttons (placed after feelings)

**Purpose:** Give immediate evidence-based counterphrases for common excuses.  
**Inputs:** 4–6 prewritten excuse buttons (e.g., “I need motivation first”, “It’s too late to start”, “It’ll take forever”, “It’s not that important”). User taps those that apply (optional).  
**Outputs:** For each tapped excuse, present one 1-sentence counter-reframe + a suggested micro-action. (E.g., “It’s too late” → “A 10-minute start still moves things forward — open project and write one TODO.”) Tone = persona.  
**Rule:** Keep each counter-reframe ≤20 words.

---

## 5) Aggregation & Reframe Module (core LLM step)

**Purpose:** Combine task title + uploaded context + selected feelings + selected negative thought categories + tapped excuses → produce a short, prioritized output: (A) 1–2 CBT reframes, (B) single next action (≤10 minutes), (C) brief personalized starter message.  
**Inputs:** Structured JSON from Modules 2–4 + persona.  
**Outputs (strict format):**

- **Reframe (1–2 lines):** Concise corrective thought(s) that directly map to selected thinking errors.

- **Next Action (one line):** Concrete micro-task (5–10 minutes). Use an implementation intention when possible (If [time], then [action]).

- **Starter Script (1 sentence):** Read-aloud friendly one-liner user can say to themselves before starting. (Integrated into your Personal Message module.)

- **Confidence tag:** `low/medium/high` (model confidence in appropriateness).  
    **Prompt template to model:**

> Aggregate the following inputs and produce JSON with keys: `reframe`, `next_action`, `starter_script`, `confidence`. Each value must be concise. Tone = persona. Reframe(s) should counter selected distortions directly. Next_action must be a specific physical action that can be completed in ≤10 minutes. Starter_script is a single sentence the user can repeat.

**Example output JSON:**

```json
{
  "reframe": "Small, messy progress counts; you can always revise later.",
  "next_action": "Open project folder and write one function header (10 minutes).",
  "starter_script": "Okay — 10 minutes. I’ll just get one thing started.",
  "confidence":"high"
}
```

---

## 6) Automatic Task Breakdown Generator (action plan integration)

**Purpose:** Create a short 3-step micro-breakdown of the frog, prioritized smallest → next. Each step should be self-contained and independently completable in ≤20 minutes (preferably 5–15 minutes).  
**Inputs:** Task title + optional file context + chosen time_box preference.  
**Output:** 3 suggested steps with estimated durations (e.g., Step 1: open and run tests — 5 min; Step 2: write function stub — 10 min; Step 3: write one unit test — 15 min). Also mark which is the “first bite” (should match the `next_action` from aggregation).  
**Rule:** Steps must be concrete and sequential; avoid vague verbs like “work” or “improve.” If file indicates code/docs, include code-related starter steps.

---

## 7) Time-Box Selector (Quick Timer Module)

**Purpose:** Let user pick an immediate duration and start a timer.  
**Inputs:** Quick picks: 3, 5, 10, 15, 25 min (Pomodoro). Default recommended = `next_action` duration or 10 min. Button: “Start now.”  
**Outputs:** Timer UI + one sentence reminder (starter script) shown while timer runs. When timer completes, show completion prompt with quick checkboxes: “Continue / Stop / Log.”  
**Rule:** When timer starts, disable distracting notifications optionally and show existentially small instructions (e.g., “No editing, just one small step — open file”).

---

## 8) Micro-Reward Selector + Image Generator

**Purpose:** Strengthen approach behavior by pairing the start with a chosen micro-reward and an image representation.  
**Inputs:** Micro-reward dropdown (Tea, Snack, 2-min walk, 1 song, Stretch break, Funny GIF). After selection, option to “Generate image of reward” (one tap).  
**Outputs:** Short reward description + generated image (one PNG) sized for display. Image must be stylized, non-photorealistic (to avoid copyrighted or personal depiction issues). Provide alt text.  
**Prompt template for image generator:**

> Create a simple, uplifting illustration of [reward] in a minimal style, suitable as a phone banner (aspect ratio 16:9). Include a small caption overlay: “Reward after starter.” Do not use real person likenesses.

---

## 9) Personalized Starter Scripts & Personal Message Module

**Purpose:** Produce a short personal message that combines the reframe, persona tone, and a micro-action invitation. This is the message the app will display right before the timer starts.  
**Inputs:** Output from Aggregation + Persona. Option: choose message length (short = 1 sentence, medium = 2–3 lines).  
**Output:** Final display message and optional copyable text for the user to paste as alarm/phone reminder or read aloud. Also offer “Send to self” (email/DM) button.  
**Example:** `Tsundere: “Hmph — fine. Do 10 minutes. But don’t expect me to babysit you forever.”`

---

## 10) Post-Session Quick Log & Relapse Recovery

**Purpose:** After timer ends, let user log outcome with minimal taps: “Worked / Started but stopped / Didn’t start.” If “Didn’t start,” show relapse support: 1) validation line, 2) one modified micro-action (smaller), 3) offer to schedule next short session.  
**Inputs:** Tap one of 3 buttons. Optional quick slider for mood (emoji).  
**Outputs:** Brief coaching line + adaptive next step.

---

## 11) Two-Tap Pattern Tracker (privacy-friendly)

**Purpose:** Collect lightweight usage data to generate trends and suggestions after a few sessions. No long journaling.  
**Inputs (each session):** Time of day (auto), session result (3 choices), main feeling category (1 tap).  
**Output:** After 7 uses, provide one insight sentence: e.g., “You tend to stall in the evening; try scheduling frogs before 3pm.” Keep outputs concise. Allow user to opt out.

---

# UX & Low-Effort Design Rules

- Default suggestions must always be present so users don't have to type.

- Use chips, 1-tap buttons, and short dropdowns; no multi-paragraph forms.

- Make “Start now” visually prominent; minimize friction to begin timer.

- Provide “skip to timer” for users who just want a push.

- Keep all messages ≤2 sentences by default; include “Explain more” toggles for users who want clinical background.

- Offer an “Undo” or “Back” at each step.

---

# Safety, Privacy & Edge Cases

- If user types or selects crisis keywords (self-harm, suicidal intent), output immediate safety text and provide local crisis resources — do not run normal intervention.

- Avoid producing prescriptive medical advice. Use language like “If you’re struggling severely, consider contacting a mental health professional.”

- For uploaded files, strip/extract only the first relevant paragraph or small code snippet to minimize data retention; provide opt-out.

---

# Implementation Notes (for wiring PartyRock widgets)

- **Widget types:** Persona (dropdown), Relapse (button), Task (short text + file upload), Feelings (multi-select), Thoughts (multi-select chips), Excuses (buttons), Aggregator (LLM call), Breaker (LLM call), Timer (UI widget), Image generator (image widget), Post-session log (buttons).

- **Chaining:** After persona, show relapse nudge. Then Task→Feelings→Thoughts→Excuse buttons→Aggregator → Breaker + TimeBox + Reward → Start timer.

- **Model instructions:** Use a strong Bedrock text model for cognitive tasks; use a lightweight image model for reward images. Keep repetition low by including `temperature=0.2` for deterministic outputs for action plans and a slightly higher temperature (0.6) for persona phrasing variation.

- **Max token guidance:** Keep `reframe` and `next_action` outputs to ~30 tokens each. Starter_script ~15 tokens.

---

# Example End-to-End Flow (test case)

**User selections:** Persona=Neutral Coach; Task="Write analysis.py"; File uploaded (short code); Feelings=[Anxiety, Overwhelm]; Thoughts=[Perfectionism, All-or-nothing time thinking]; Excuse tapped: “I need motivation first”; Reward=Tea; TimeBox=10 min.

**Aggregator JSON output (example):**

```json
{
 "reframe":"A short, messy version is progress; you can improve it later.",
 "next_action":"Open analysis.py and add one function header (10 min).",
 "starter_script":"Just ten minutes — one function header, then stop.",
 "confidence":"high"
}
```

**Automatic breakdown:**

1. Open project and run tests (5 min)

2. Add function header and docstring (10 min) ← first bite

3. Implement simple return or placeholder test (15 min)

**Reward image:** small illustration of a steaming cup with caption “Tea after 10 min”.

---

# Testing / QA Checklist (before deployment)

- Validate that each persona produces appropriately toned variations for the same inputs.

- Test maximum 6 thought selections. Confirm model references chosen categories in the reframe.

- Timer must always show starter_script while running.

- Ensure image generation returns within acceptable size limits and alt text.

---

If you want, I can now:

- Produce the **exact LLM prompt strings** for the Aggregation, Breakdown, and Persona phrasing calls (ready to copy into PartyRock model widgets).

- Generate sample micro-copy for each persona for the app UI (button labels, tiny helper text).

Which of those would you like next?