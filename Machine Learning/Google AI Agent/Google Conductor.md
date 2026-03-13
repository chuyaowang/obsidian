# Google Conductor

#agent 
[link](https://developers.googleblog.com/conductor-introducing-context-driven-development-for-gemini-cli/)

Based on the article **"Conductor: Introducing context-driven development for Gemini CLI"** (published Dec 17, 2025), here is an explanation of what Google Conductor is and how to use it in a code development workflow.

## What is Google Conductor?

**Google Conductor** is an extension for the Gemini CLI that shifts AI development from simple chat logs to a structured methodology called **Context-Driven Development**.

Instead of relying on a temporary chat window where context is lost when the session ends, Conductor helps you create formal specifications ("specs") and plans that live directly in your codebase as persistent Markdown files.

**Key Philosophy:** "Control your code." It treats project context (requirements, tech stack, guidelines) as a managed artifact, ensuring the AI agent has a deep, persistent understanding of what it is building and why.

**Core Benefits:**

* **Persistent Context:** Uses Markdown files in your repo as the "single source of truth."
* **Plan Before Build:** Forces a "measure twice, code once" approach by creating specs and plans before generating code.
* **Team Consistency:** Allows teams to define shared project settings (tech stack, testing strategies) so AI contributions feel cohesive regardless of which developer runs the tool.
* **Brownfield Support:** Designed to work well with existing ("brownfield") codebases by analyzing current architecture to inform new features.

---

## How to Use Conductor in a Workflow

Conductor organizes development into "Tracks"—high-level units of work. Here is the standard workflow described in the article:

### 1. Installation

First, install the extension using the Gemini CLI:

```bash
gemini extensions install https://github.com/gemini-cli-extensions/conductor

```

### 2. Establish Context (Setup)

Run this command to initialize Conductor in your project. It creates a foundational set of documents defining your project's "DNA":

* **Command:** `/conductor:setup`
* **What you define:**
* **Product:** Users, goals, and high-level features.
* **Tech Stack:** Languages, databases, and frameworks.
* **Workflow:** Team preferences (e.g., Test-Driven Development).

### 3. Specify and Plan (New Track)

When you start a new feature or bug fix, you initialize a "Track." Conductor will interview you to generate two critical Markdown artifacts:

* **Command:** `/conductor:newTrack`
* **Artifacts Generated:**
* **Specs:** Detailed requirements (What are we building and why?).
* **Plan:** An actionable checklist of Phases, Tasks, and Sub-tasks.

### 4. Implement

Once you review and approve the plan, the coding agent begins execution. It works through the `plan.md` file, checking off tasks as it completes them.

* **Command:** `/conductor:implement`
* **Features:**
* **State Persistence:** You can stop work and resume later without losing context.
* **Checkpoints:** Ability to revert to previous versions if the agent makes a mistake.
* **Mid-flight Edits:** You can edit the plan while the agent is working if requirements change.