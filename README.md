**Note to readers from outside the theological space**: This is a data systems and knowledge representation project. Theology was chosen as the initial domain because it supplies unusually rich, publicly available, historically deep textual data with well-documented layers of reinterpretation. The tooling and modeling techniques are intended to be portable. Primary intention is to explore usage of AI agents to atomize complex historical contexts and trends into manageable and irreducible atomic data. Once relevant sections of graph data and ideas across history are atomized, the foundation can be systematically audited, and corruptions highlighted through a Directed Acyclic Graph (DAG). Project will explore the limits of this approach.

This project is a companion to an emerging field we have come to call Open Source Theology. It is a domain full of opportunity to solve complex historical data and corruption problems in a domain traditionally dominated by division more than unity. For the first time in history manuscripts have been published to the internet and real historical analysis can take place. This platform is designed to aid these efforts to turn endless debates into productive analysis.


# Sovereign Node

**A general-purpose platform for exploring and linting corrupted, historically layered textual data.**

Sovereign Node is an open-source knowledge graph and semantic analysis system designed to ingest complex textual domains, extract claims, map them to underlying primitives, and surface institutional drift, rhetorical patterns, and logical inconsistencies.

Theology is used as the initial high-signal dataset because it offers one of the richest available environments for this kind of work: centuries of textual variants, layered translations, institutional reinterpretation, and high-stakes rhetorical language. The architecture itself is domain-agnostic and intended to generalize to other historically dense corpora (legal history, medical literature, technical documentation with legacy assumptions, etc.).

## The Problem

Many important domains accumulate **corrupted data** over time:

- Original source material gets filtered through institutional incentives
- Rhetorical patterns become standardized without their original context
- Translations and interpretations drift while retaining the appearance of continuity
- Claims get detached from their primary evidence layers

Traditional search and LLM summarization tools are poorly suited to this problem because they optimize for fluency rather than traceability. They tend to reproduce the dominant institutional framing instead of exposing where the framing diverged from the source material.

## Approach

Sovereign Node treats textual domains as **immutable, versioned graphs** rather than flat documents.

Core model:

- **Idea Nodes** — abstract concepts (e.g. "restorative justice", "divine council", "atonement mechanics")
- **Assertion Nodes** — specific claims made by individuals or institutions about those ideas
- **Evidence Layer** — primary source atoms (Strong’s numbers, morphological data, manuscript variants, lexical entries from Thayer’s/LSJ, ANE parallels, etc.)

A via-negativa analysis engine (the "linter") compares modern claims against the evidence layer and flags:
- Detachment from primary lexical/historical data
- Rhetorical patterns that function as institutional control mechanisms
- Logical inconsistencies introduced by later interpretive layers
- Over-reliance on secondary or tertiary sources

The system is designed to remain useful even when the underlying data is incomplete or contested. It surfaces **what is being assumed** rather than enforcing a single correct interpretation.

## Why Start with Theology

Theology provides an unusually good test corpus for corrupted data analysis:

- Extremely long revision history with clear institutional breakpoints (pre- and post-Constantinian, Reformation, modern denominational formation)
- Publicly available high-quality lexical and manuscript datasets (MorphGNT, Open Scriptures Hebrew Bible, Thayer’s, LSJ, Dead Sea Scrolls variants)
- Dense rhetorical tradition with well-documented patterns of reuse and reframing
- Existing independent scholarship (e.g. work in the style of Michael Heiser or the Berean Patriot) that already performs rigorous source tracing

The goal is not to produce theological conclusions. The goal is to build tooling that makes the **process** of source tracing and drift detection scalable and reproducible across any domain that has accumulated similar layers of institutional interpretation.

## Technical Architecture

- **Data Layer**: Immutable facts with strong support for historical versioning
  and graph queries.
- **Primitive Atoms**: Strong’s numbers + upgraded lexical data (Thayer’s, LSJ) + morphological sequences (MorphGNT / OSHB) linked through Book-Chapter-Verse containers.
- **Decoupled Model**: Idea nodes are kept separate from the evidence that supports or contradicts them. This allows multiple scholarly or institutional assertions to attach to the same concept without forcing premature consensus.
- **Analysis Engine**: Structured output from capable models (AI model TBD) that map free text to the graph while remaining auditable.
- **UI**: Clojure Electric for reactive, full-stack interfaces with minimal boilerplate. Designed for both quick exploration and deeper research workflows.
- **Extensibility**: Vector embeddings and clustering for trend detection across large corpora of claims over time.

The architecture prioritizes **traceability** and **composability** over convenience features. Every relationship in the graph should be explainable back to primary source atoms.

## Current Status

Early development. The initial focus is on:

1. Ingesting and normalizing open lexical and morphological datasets into a queryable graph.
2. Building the core schema for Idea / Assertion / Evidence separation.
3. Creating a basic exploration interface for Strong’s numbers, lexical entries, and verse-level data.
4. Establishing clean ingestion pipelines for both scholarly monographs and modern textual claims (sermons, articles, etc.).

Later phases will add:
- Structured claim extraction from longer-form sources
- Cross-corpus trend analysis
- Public contribution paths for new evidence layers and assertions

## Tech Stack

- Clojure + ClojureScript
- Electric (reactive full-stack)
- DataScript / Datomic
- Shadow-CLJS + Tailwind
- Open data sources: MorphGNT, Open Scriptures, Thayer’s, LSJ, Strong’s (public domain / permissive)

## Getting Started (Early)

This project is currently in active foundational development. The most useful contributions at this stage are:

- High-quality ingestion scripts for additional public lexical or manuscript datasets
- Careful schema design feedback on the Idea/Assertion/Evidence model
- Tooling for structured extraction that preserves traceability

See the `data/` directory and ingestion namespaces for the current state of the primitive layer.

## Philosophy

The project operates on a via-negativa principle: progress is made by systematically removing layers of institutional and rhetorical corruption rather than by constructing new positive frameworks. The value lies in making the underlying structure of claims visible and debatable again.

This is fundamentally an engineering and data problem applied to a domain that has historically been treated as purely interpretive.

## License

MIT (or equivalent permissive license — to be confirmed on first tagged release).

---