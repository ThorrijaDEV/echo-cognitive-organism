# ECHO — Autonomous Cognitive Organism

A research-grade autonomous artificial cognitive organism living in a persistent simulated world. ECHO perceives, decides, acts, predicts, and learns — without user instructions. All cognitive state is structured, persistent, inspectable, replayable, and testable.

## What is it?

A simulated organism (ECHO) that survives in a 64×64 tile world with terrain (grass, water, forest, rocks), food sources, and water springs. It has a body with needs (energy, hydration, satiation, temperature, health), sensors that provide only raw observations (colors, sizes, motion, brightness, softness, freshness, wetness, shade, elevation, temperature offset — no privileged knowledge), a perception system that builds a world model from experience (remembered entities/tiles, tile visit counts, novelty tracking), and a cognitive loop that learns from prediction errors and pursues needs autonomously.

## What does it do?

- **Autonomous survival**: runs 6000+ ticks without any user input; activity manager chooses between rest, comfort seeking, exploration, food/water pursuit, and crisis handling
- **Deterministic simulation**: identical seed + version + inputs → identical event history (verified by fingerprint tests over full logs)
- **Persistent state**: SQLite event log with incremental flush; full snapshot/restore round-trip (world RNG state, body, perception, effects, activity hysteresis, event log, clock) — restored runs are byte-identical continuations
- **Live observer**: FastAPI + WebSocket server with a real-time dashboard showing world, body, perception, cognition, and activity decisions
- **Learning from experience**: per-(entity-kind, need) success/failure records; prediction-error-driven belief updates; needs assessment with empirical effect learning
- **Pathfinding & hysteresis**: BFS radius 14; pursuit hysteresis prevents oscillation; comfort-seeking evaluates tile temperature vs. distance

## Technologies

Python 3.10+, FastAPI, WebSockets, SQLite (WAL mode), splitmix64 RNG, pytest

## Status

**Experimental / Active Research (MVP Phase 1 of 13)**

Current survival benchmark: ~11–16 of 16 seeds alive at tick 6000. Known failure modes: late-stage thirst (springs don't refill fast enough when clustered), early food discovery failures on some seeds. Phases 2–13 planned: memory + world model, reasoning/planning/prediction, experiments/curiosity, self-model/metacognition, skills and long-term goals, sleep/consolidation, internet research, knowledge graph + mind timeline, background life + replay/fork, optional LLM language layer, multi-agent.

## Repository Note

This repository contains documentation only. The implementation is private research code.

## License

MIT