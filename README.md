# Ask · Connect · Delegate

**Architecture for AI work**

Asking, connecting, and delegating answer different questions. A model can perform a task well and still be the wrong thing to hand authority to. This presentation develops that argument through a single running scenario — a recurring campaign workload — and closes on a practical rule: delegate where the loop can close, and constrain authority where it can't.

**View the live presentation:** <https://rtmandreyev.github.io/ask-connect-delegate/>

**Repository:** <https://github.com/rtmandreyev/ask-connect-delegate>

**Companion presentation:** Predict · Explain · Intervene — <https://rtmandreyev.github.io/predict-explain-intervene/>

![The title slide: ASK · CONNECT · DELEGATE — Architecture for AI work](assets/readme/title-slide.png)

---

## Overview

A sixteen-slide Reveal.js deck built with Quarto, with a custom SCSS theme — a title slide, fourteen content slides, and a reference slide. It stays on one running scenario from the first slide to the last.

It opens with a single number: 93% of Claude Code permission prompts were approved. The question that follows is whether that is oversight or habit — and if approval stops being a decision, what is actually controlling the machine.

From there the talk separates three questions that are often conflated:

| Business question | Architectural dimension |
| --- | --- |
| What judgment does this need? | **Ask** — what cognition or judgment is actually required |
| What can it reach? | **Connect** — what information, systems, and tools it can touch |
| Who chooses what happens next? | **Delegate** — where the authority sits and how far it extends |

The deck then works through each in turn. Ask is settled first with the running scenario: 200 campaigns a week, a four-step process, and one question — how? Separating a workflow from an agent is the answer, because their control flows differ: a workflow runs a predefined path with AI inside it, an agent decides the path and loops. Connect comes next, and the deck is emphatic that it is not delegation — MCP standardises how a model reaches tools and context without choosing the goal, the plan, or the action, so access and autonomy are not the same permission. Delegate is where the deck slows down, and it arrives there through evidence rather than principle: a company that automated 55% of claims start to finish and moved the remaining boundary rather than removing it, a meta-analysis of 106 experiments showing that human + AI combinations did not outperform the better solo performer on average, and a running agent that hands control to a human at a login gate and resumes afterwards. It closes on the variables that actually decide the answer — authority, reversibility, and blast radius — rather than on how capable the model is.

The discussion is then grounded in what the cited sources actually report rather than in the deck's own authority: a vendor engineering report on containing an agent in production, a public company's FY2025 Form 10-K, and a peer-reviewed meta-analysis in *Nature Human Behaviour*. The deck's framework follows: it names the dimensions, composes one system from the components that occupy them, and reduces the delegation decision to four questions. Its conclusion is that the architecture around a model decides whether delegating to it is safe, and that the question worth asking is not "which model is best?" but "best for what?"

## The rule: delegate where the loop can close

The deck's payoff is a four-question test to run before handing anything over: **can we verify it, can we reverse it, can we bound it, and who handles the exception?** Where those answers hold, the deck's argument is that delegation can go wide — a recurring, high-volume workload is exactly where an agent earns its keep. Where they don't, the correct move is not a better model but a narrower authority.

That is the sense in which the talk is about architecture rather than intelligence. The deck makes the same distinction concrete twice: drafting an email and sending money may be the same capability at a different authority, and a model that returns three typed outcomes — `PILOT .61`, `DEPLOY .22`, `ABSTAIN .17` — is more useful for a bounded decision than one that answers in open-ended prose. It also treats discovery as part of the architecture: trying models through OpenRouter, including free and stealth endpoints, is how you find what a task actually needs, with the boundary that free inference is not free data.

None of this is claimed as a published framework. The closing slide labels the four questions the presentation's own synthesis, drawn from the prediction/decision framing in the cited literature, and the architecture slide labels its composition as one possible arrangement rather than a recommended stack. Product names — Paperclip, Buzz, Hermes, MCP, n8n, Jev, OpenRouter, Inkling — appear because they occupy different architectural roles, not because they belong together.

## Design and implementation

The deck is a dark 1600×900 layout with fixed colour semantics carried across every slide: acid green for machine execution and delegation, cyan for connection and interfaces, electric yellow for human judgment and uncertainty, and signal red for boundary, privacy, and constraint. Slides are authored as hand-written HTML blocks inside the Quarto source rather than plain Markdown, so each slide's layout can be controlled individually, with fragment-based reveals and hash-addressable slides.

- **Quarto** (1.10.18) with the `revealjs` format
- **Reveal.js** 5.1.0, bundled by Quarto's `revealjs` format
- **Custom SCSS theme** — `theme.scss`, providing the palette, typography, and all per-slide layout rules
- **Product marks** — a small number of official logos in `assets/logos/`, palette-adapted and each used once
- No JavaScript frameworks and no external runtime dependencies

## Running it locally

Requires [Quarto](https://quarto.org). This output was rendered with Quarto 1.10.18.

```bash
git clone https://github.com/rtmandreyev/ask-connect-delegate.git
cd ask-connect-delegate

quarto preview presentation.qmd   # live preview while editing
quarto render presentation.qmd    # writes presentation.html
```

`presentation_files/` is Quarto's generated asset directory and is gitignored, so a fresh clone must be rendered before `presentation.html` will display correctly on its own. To view an already-rendered copy without Quarto, serve the directory over a local server (for example `python3 -m http.server`) and open the HTML — the deck loads its assets relatively.

GitHub Pages publishes the presentation itself at <https://rtmandreyev.github.io/ask-connect-delegate/>. The site is built by a GitHub Actions workflow (`.github/workflows/publish.yml`), which renders `presentation.qmd` with Quarto, checks that the deck, Reveal.js, and the deck's own assets are all present, and deploys the result as the site root; the `presentation_files/` assets are generated during the build and are not committed.

## Sources

Every substantive slide carries an inline citation to the specific source supporting the claim, and vendor-reported figures stay attributed on the slide rather than in the deck's own voice. The deck's closing slide holds the full bibliography and is the authoritative reference — 24 entries covering Anthropic's engineering report on containing Claude across products; Agrawal, Gans & Goldfarb, *Prediction Machines* (2018); Anthropic's "Building effective agents"; the Model Context Protocol specification; Lemonade's FY2025 Form 10-K; Vaccaro, Almaatouq & Malone, *Nature Human Behaviour* (2024); the Hermes Agent, Paperclip, Buzz, n8n and MCP documentation; TypeSafe AI's System One material; Thinking Machines Lab's Inkling and Tinker; Fulcrum Research's Echo; OpenRouter's stealth and free-model records; and the official pages for the models named on the landscape slide.

Two figures on the deck are labelled on the slide as illustrative rather than empirical — the recurring-campaign scenario and the example Jev output — and the deck fits no models and evaluates none. The permission statistic is Anthropic-reported telemetry, the claims-automation figure is a company-reported metric, and the collaboration result comes from a published meta-analysis; each is marked as such where it appears.

## Main files

| File | Role |
| --- | --- |
| `presentation.qmd` | Presentation source — front matter, slide content, inline citations |
| `theme.scss` | Custom SCSS theme: palette, typography, per-slide layout |
| `presentation.html` | Rendered deck (generated by `quarto render`) |

## Series

This is the second of two CIS 565 presentations, built as a pair rather than a one-off:

- **[Predict · Explain · Intervene](https://github.com/rtmandreyev/predict-explain-intervene)** — on what AI contributes to a decision. Prediction, explanation, and causal intervention answer different questions, and the talk closes on matching the model to the decision.
- **Ask · Connect · Delegate** — this deck — moves outward from the decision to the architecture around it: connectivity, control, authority, and delegation.

## Context

This is coursework — built for CIS 565 and kept here as a standalone presentation artifact. It presents no original research and fits no models; the arguments are drawn from the cited sources, and the product names identify architectural roles rather than endorsing a stack.
