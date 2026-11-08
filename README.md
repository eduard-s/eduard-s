# Hi, I am Eduard 👋

**Software development · Applied AI · Science**

I work on AI tools and software systems. My interests include model training, agents, and software design.

In my free time, I explore liquid crystals and molecular self-assembly.

- **Website:** [https://esmirnov.ai](https://esmirnov.ai/)
- **Email:** [eduard@esmirnov.ai](mailto:eduard@esmirnov.ai)
- **NematicLab:** [https://nematiclab.com](https://nematiclab.com/)

## Public repositories

| Repository | What it does |
| --- | --- |
| [Nematic game](https://github.com/eduard-s/nematic-game) | A React component and web app for a 2D material model. It has liquid crystals, ions, fields, and local brushes. |
| [TableProof](https://github.com/eduard-s/table-proof) | Python audits for PDF table associations, with source evidence, an optional local vision model, and reproducible regression cases. |
| [ToolBoundary](https://github.com/eduard-s/tool-boundary) | Finds input, result, and error mismatches across MCP and AI SDK tool paths. It has Python and Node.js packages. |
| [Workflow engine: Python services](https://github.com/eduard-s/event-driven-workflow-orchestration-engine) | Runs parallel JSON workflows with an API, orchestrator, workers, PostgreSQL, and Redis Streams. |
| [Workflow engine: Go monolith](https://github.com/eduard-s/event-driven-workflow-orchestration-engine-monolith) | Runs durable JSON workflows in one Go app with PostgreSQL, retries, and recovery. |
| [Workflow engine: LangGraph monolith](https://github.com/eduard-s/event-driven-workflow-orchestration-engine-monolith-langgraph) | Runs JSON workflows with FastAPI and LangGraph. PostgreSQL stores state and checkpoints. |
| [Skills](https://github.com/eduard-s/skills) | Reusable Markdown skills for AI assistants. The first skill examines evidence for everyday science questions. |

## Use Nematic game

[Open the lab](https://esmirnov.ai/nematic-game/) · [Read the component API](https://github.com/eduard-s/nematic-game/blob/main/docs/API.md)

Nematic game supplies a reusable React component and a standalone demo.
The field uses the full component width.
The controls appear below the field.
The model uses relative scales for play and explanation.

Install the component in a React app.

```sh
npm install https://github.com/eduard-s/nematic-game/archive/refs/tags/v0.1.0.tar.gz
```

Import the component and its stylesheet.

```tsx
import { NematicLab } from "@eduard-s/nematic-game";
import "@eduard-s/nematic-game/styles.css";

<NematicLab
  initialMaterial={{ heat: 0.15, density: 0.65 }}
  theme={{ sample: "#172D42", rodHigh: "#91DCE5" }}
/>
```

The component supplies defaults for the other settings.
Reset sample restores the initial configuration.
You can change the source to add your own tools and visual effects.

## Try ToolBoundary

[Python on PyPI](https://pypi.org/project/tool-boundary-py/) · [Node.js on npm](https://www.npmjs.com/package/@esmirnov.ai/tool-boundary) · [Examples and explanation](https://esmirnov.ai/blog/tool-boundary/)

## Try TableProof

[Source installation and example](https://github.com/eduard-s/table-proof#try-the-real-regression-case) · [Benchmark evidence](https://github.com/eduard-s/table-proof/blob/main/benchmarks/README.md) · [MVP plan](https://github.com/eduard-s/table-proof/blob/main/docs/MVP_PLAN.md)

TableProof is an alpha library. It compares extracted cells with source evidence and reports uncertain cases. PyPI publication is deferred.
