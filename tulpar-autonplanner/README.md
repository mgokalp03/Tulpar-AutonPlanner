# Tulpar AutonPlanner

A modular toolkit for planning and simulating VEX V5RC autonomous strategies.

This repository is the foundation for a future autonomous planning studio: a field-aware model that can represent the game, scoring elements, robot constraints, and autonomous timing in one consistent structure.

## Project vision

The core idea is simple:

Game → Field → Objects → Scoring locations → Robot constraints → Autonomous period

Instead of hardcoding logic for one season at a time, the app separates game data from the tooling layers. That means a future season can be added by swapping in a different game definition without changing the editor, simulator, or code-generation pipeline.

## What is in this repo

This is the current v0.1 slice: the game layer.

### Included modules

- `src/game/game-shapes.ts` — season-agnostic interfaces for the game model
- `src/game/field-math.ts` — coordinate conversion, snapping, and heading helpers
- `src/game/game-catalog.ts` — registry for loading and selecting active games
- `src/game/games/season-2026-27.ts` — VEX V5RC 2026-2027 game definition
- `src/game/game-layer.ts` — public export surface for the module

### Design principles

- Units are stored in inches
- The field origin is the center of the field
- Heading is measured in degrees counterclockwise from +X
- `GameObject.kind` is intentionally free-form so new seasons can introduce new object types without changing the shared model
- Scoring data may include notes instead of fake constants when live state affects value

## Current game data

The repository includes a populated definition for the 2026-2027 VEX Over/Under season.

The data in `src/game/games/season-2026-27.ts` is sourced and documented inline, with references to:

- the official VEX game manual
- the manual changelog where needed for rule clarifications
- the public element-count data from VEX
- published VEXcode VR coordinates, converted from millimeters to inches

Important caveat: the VR Playground data represents a simplified virtual-skills field and is not a perfect substitute for the official competition field. Some details are intentionally left as notes or `undefined` values when the source was not trustworthy enough to fabricate a number.

## Quick start

```bash
npm install
npm run typecheck
```

## Repository structure

```text
.
├── README.md
├── package.json
├── tsconfig.json
├── index.html
├── field-diagram.png
├── tulpar-team-logo.png
├── atatürk-bayrak.gif
├── src/
│   └── game/
│       ├── field-math.ts
│       ├── game-catalog.ts
│       ├── game-layer.ts
│       ├── game-shapes.ts
│       └── games/
│           └── season-2026-27.ts
└── vex-auton-studio/
    └── README.md
```

## Roadmap

This repository is intentionally scoped to the foundational layer. The remaining pieces planned for the full studio include:

- field editor UI with canvas drawing and object placement
- timeline-based autonomous sequence editing
- code generation for robot programs
- simulation and debugger tooling
- richer scoring evaluation and validation

## Status

This project is under active development and is currently focused on establishing a robust, season-independent data model for VEX autonomous planning.

The goal is to make the app extendable to future seasons by updating data rather than rewriting the application architecture.




