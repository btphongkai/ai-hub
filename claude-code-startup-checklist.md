# Claude Code Practice Checklist (from "The Claude Code Guide for Startups")

Source: https://claude.com/resources/articles/claude-code-guide-for-startups (Anthropic, Aug 20, 2026)
Level: team already using Claude Code daily, wants to systematize. Generic, not tied to one project.

How to use: go rule by rule. Each item has an action and a "Done when" test. Start with items marked ⭐ (quick wins).

---

## Rule 1: Everyone ships
Goal: whoever understands the problem can build the first version of the fix (0-to-1). Specialists still own review and production quality.

### Connect
- [ ] ⭐ Give every relevant role (PM, QA, support, domain experts) access to Claude Code, not just an expectation to "use AI".
  - Done when: each person has a working install and has run one real task.
- [ ] Connect Claude to your sources of truth (tickets, docs, DB, repo, monitoring) via MCP.
  - Done when: Claude can read from each source without copy-pasting.
- [ ] Prefer mature CLI tools (`gh`, `kubectl`, `bq`, `psql`) over MCP where they exist, as they are more token-efficient.
  - Done when: you have a list of which source uses MCP and which uses CLI.

### Share
- [ ] ⭐ Write skills (reusable instruction files) for team standards: code style, design system, PR template, release steps.
  - Done when: a newcomer can run the skill and get output meeting your standard.
- [ ] Create a shared skills repo or company plugin directory.
  - Done when: skills are versioned, discoverable, and have an owner.
- [ ] Add per-directory `CLAUDE.md` files for local conventions; use skills for on-demand procedures.
  - Done when: each major module has its own conventions file.
- [ ] Accept "slightly outdated but verifiable" context: tell the agent to verify and correct skills as it works.

### Showcase
- [ ] Create a prototype channel (e.g. Slack) where anyone posts what they built.
- [ ] Hold a regular demo/review (quarterly in the article) where prototypes can enter the roadmap.
- [ ] Set a higher review bar for AI-built changes that touch the production product.
- [ ] Have everyone, including senior engineers, talk to customers to shorten the feedback loop.

---

## Rule 2: Automate the tedium
Goal: agents do the mechanical ~80%; humans keep the judgment calls.

### Across the lifecycle
- [ ] ⭐ Onboarding: put dev-environment setup in a markdown file and let Claude run it and fix it when broken.
  - Done when: a new hire is set up by pointing Claude at the file.
- [ ] ⭐ Enable Code Review (research preview) on key repos; configure GitHub Actions so `@Claude` can act on findings.
  - Done when: every PR on key repos gets an automated review.
- [ ] Build a custom review agent that checks a change from several angles (security, compliance, performance) and merges the results.
- [ ] Use parallel subagents for multi-ticket work: one subagent per ticket and per PR.
- [ ] Automate bug triage from first pass to suggested fix.
- [ ] Put Claude Tag (or equivalent) on CI/CD failure first response, with its own service account, observability access, and standing instructions stored as skills in a repo.
- [ ] Build loops, not one-off runs, for recurring jobs (flaky-test fixing, missing-coverage detection).

### Recurring business processes
- [ ] Pick one recurring analysis (self-service analytics, feedback categorization, document summarization, anomaly sweeps) and build an agent for it end to end.
- [ ] For big analysis, ask explicitly: "fan out multiple subagents" or "use a workflow" (higher-end models).

---

## Rule 3: Trust, but verify
Goal: only automate what you can monitor and verify.

### Guardrails
- [ ] ⭐ Put non-negotiables in the root `CLAUDE.md`: architecture rules, security boundaries, constraints.
  - Done when: they load every session and Claude can state them back.
- [ ] Write down architecture invariants, how problems are framed, and what counts as proof.
- [ ] Never let agents merge to main unchecked; require human approval.
- [ ] Use hooks as hard gates where results must be deterministic: block writes that fail lint, require tests before commit, strip secrets.
  - Done when: a bad change is blocked automatically, not by reminder.

### Loops and checks
- [ ] Give every loop a clear stop condition defined in a skill (e.g. tests rerun green).
- [ ] Use `/goal` on long tasks to prevent declaring victory early, drifting, or over-trusting its own review.
- [ ] Use dynamic workflows to run subagents in sequence with separate contexts and focused goals.

### Evals
- [ ] Build a golden set: verified question-answer pairs for each key use case; update regularly.
  - Done when: you can rerun it after any prompt or model change.
- [ ] Back-test every instruction change against the golden set plus random samples; use a judge model to separate real errors from valid alternatives.
- [ ] Move past manual testing and gut feel once agent quality matters.

### Human-in-the-loop improvement (Cainex pattern)
- [ ] Have experts review outputs and reasoning in an app; version everything for audit.
- [ ] Let Claude tag corrections by type, find the instruction that caused each error, and propose revisions.
- [ ] Fix the underlying principle, not the single case; cap how many specifics one change can contain to avoid overfitting.
- [ ] Output a short list: suggested edits, unresolved records, open questions.

---

## Rule 4: Build for rebuilding
Goal: treat scaffolding as disposable; model capabilities keep changing.

- [ ] ⭐ Use plan mode (`--plan` or Shift+Tab) for any non-trivial rewrite; review the plan before code.
- [ ] Use git worktrees to rebuild in isolation, run evals on both versions, merge only if the new one wins.
- [ ] Automate cleanup chores (e.g. a skill that opens PRs removing fully rolled-out feature flags) and have an engineer review.
- [ ] Define "rebuild done" as old path removed; schedule teardown work so it does not lose prioritization fights.
- [ ] Each quarter, review prompts, tools, and scaffolding added for older models and remove what new models no longer need.
- [ ] Keep the learning (evals, data, docs) when you scrap the code.

---

## Rule 5: Prototype, dogfood, productionize (if you build AI products)
- [ ] Build an internal agent with Claude Code.
- [ ] Dogfood it with your own team.
- [ ] If results are strong, productionize it with the Claude API, SDK, or Claude Managed Agents.
- [ ] Use Claude Code to debug your own agent locally to tell model behavior apart from harness problems.
- [ ] Prefer simple designs (e.g. files over embeddings/RAG) where they are enough.

---

## Suggested order for a team already using Claude Code daily
1. Week 1: root `CLAUDE.md` with non-negotiables; plan mode as default for big changes; onboarding markdown file.
2. Week 2-3: shared skills repo; connect MCP/CLI sources; enable Code Review on key repos.
3. Month 1: hooks as hard gates; first loop with a stop condition (flaky tests or triage); prototype channel and demo.
4. Month 2-3: golden sets and evals; parallel subagent workflows; CI/CD on-call agent.
5. Ongoing: quarterly rebuild/teardown review; dogfood to production for AI features.
