# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

- **The author and his research.** A doctoral researcher at KIT (AIFB) uses the tool for his dissertation. The tool
  carries the method of the domain view (a Petri net animated in the language of its domain). He runs experiments with
  language models through the evaluation script, writes papers with its exports (TikZ, PNG, SVG) and gives
  demonstrations.
- **The AIFB research group.** Colleagues model, simulate and analyze their own processes. They use the shared server in
  the KIT network: projects with versions and share links, and a language model without a personal key.
- **Industry partners in demonstrations.** People without Petri net knowledge see their own process as a picture of
  their domain, such as a hall, a workshop or an office, and judge whether it is right.

Students in teaching were not named as a primary audience.

## Product Purpose

The tool models, simulates and analyzes Petri nets, from place/transition nets to JSON nets whose tokens are JSON values.
It replays real event logs on a net and shows the net and its behavior twice: as the net itself and as a domain view.
Success means:

- simulation and analysis results are exact and reproducible (same seed, same stream, same export);
- a domain view is recognizable to someone who does not read Petri nets;
- the tool can serve as the instrument for the dissertation's experiments.

## Positioning

Two things belong together and neither may be watered down:

1. **Formal rigor as the foundation.** A UI-independent TypeScript core for P/T and JSON nets. It drives a seeded
   discrete-event simulation and structural and state-space analysis with DECLARE/LTLf, and it runs the same in the
   browser, on the command line and on the server.
2. **The domain view as the difference.** The simulation is drawn as the real place where the process happens:
   - A language model proposes the mapping, through a guided form or a free description with wishes.
   - Twelve rules (V1 to V12) check it against the net. The user's choices are binding, and deviations are reported.
   - The behavior comes only from the net, and every animation belongs to an event of the simulation or replay.

## Operating Context

- **Local-first in the browser.** The public build on GitHub Pages works without any server. Files are `.pn.json`, with
  autosave in the browser.
- **Group use on a small server in the KIT network.** It runs as one container behind the existing ingress and is only
  reachable from the KIT network. The server adds projects, versions, share links, a tool API, and a language model via
  Open WebUI whose key lives only on the server.
- **Research work.**
  - Command line `pnm` for batch runs and processing chains.
  - Evaluation script for language model experiments: prompt version, hashes, ablations, similarity to reference views.
  - TikZ export for LaTeX.
  - PNML exchange with ProM, pm4py and WoPeD; event logs as CSV and XES.
- **Screens.** Desktop screens are the norm; layouts are reviewed at 1280 and 1920 px wide in light and dark themes.
  Demonstrations happen on a shared screen or projector.

## Capabilities and Constraints

**Capabilities (state of version 1.5.0):**

- **Editor:** places, transitions, arcs, weights, capacities, undo, automatic layout and validation.
- **Simulation:** timed simulation in a Web Worker with key figures, trace, quantity places and user-defined indicators.
- **Replay:** event log replay with token-replay fitness.
- **Analysis:** invariants, state space, coverability, DECLARE/LTLf.
- **Domain view:**
  - counters as fill levels or pictograms;
  - appearance of a case by stage;
  - emoji as a free symbol vocabulary;
  - editing by dragging;
  - generation by a language model through any OpenAI-compatible server.
- **Exchange:** PNML, SVG, PNG, TikZ.
- **Command line and server.**

**Constraints:**

- **Interface language** is English and stays English. The content of nets (names, labels, examples) may be in any
  language, and the bundled examples are German.
- **Behavior is protected.** Golden tests pin the simulation output and the scenes of the bundled examples, and a new
  version must not change them unless that is the point of the change. The file format stays `1.0` and is extended only
  with optional fields.
- **Performance:**
  - the domain view keeps a typical frame under 8 ms for 200 tokens;
  - simulation and analysis run in workers and never block the interface.
- **Privacy:**
  - language model keys never leave the browser of their owner, or the server;
  - nothing is sent to a model unless the user starts a generation.
- **Prompts are research instruments.** The fixed texts of the prompts must not contain solutions of the bundled
  examples; a leak test guards this. Every change of their content raises `PROMPT_VERSION`.
- **Open product decisions:**
  - real-time collaboration and accounts (projects are public within the network);
  - a domain view driven by the token data of higher nets (planned as D6);
  - whether students become an audience.

## Brand Commitments

- **Name.** The application is called "Petri Net Modeler", and the repository "Petri-Net-Modeling". The command line is
  `pnm`.
- **License.** MIT.
- **Voice.** The documentation and interface text are plain, precise and factual.
- **Assets.** No logo, brand colors or other brand assets have been made binding.

## Evidence on Hand

- **Bundled example nets** in `examples/`:
  - parcel center and smart office (both with domain views);
  - bicycle frame manufacturing with CO₂e, material and recycling indicators;
  - classic nets: traffic light, producer/consumer, dining philosophers and others.
- **Documentation and decisions** in `docs/` (format, simulation, replay, domain view, analysis, CLI, server,
  limitations) and the ADRs `docs/adr/0001` to `0019`.
- **Images:** screenshots in `docs/images/` and review pictures in `docs/images/review/`.
- **Measurements:**
  - pm4py interoperability check: `docs/eval/pm4py-2026-10-28.md`.
  - The author ran the LLM acceptance A6 with a local model; both reference nets passed in the first round. The report is
    not yet in the repository.

No user studies, testimonials, publications, adoption figures or customer references exist yet. Do not invent any.

## Product Principles

1. **The net is the single source of behavior.** Views, pictures and language models show and propose; they never
   change what the net does.
2. **Every picture is truthful.** Amounts are drawn in proportion with a stated scale, roles are drawn as what they are,
   and an overflow or deviation is shown rather than hidden.
3. **Reproducible by default.** The same input gives the same result, and nothing about existing nets, views or outputs
   changes silently between versions.
4. **The language model proposes, the rules and the user decide.** Choices are binding, deviations are reported, and
   every entry records its origin.
5. **Local-first and private.** Everything works without a server, and keys and content stay where their owner put them.
