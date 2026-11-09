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
| [TinyTask](https://github.com/eduard-s/tiny-task) | Train local text classifiers and route uncertain requests to review. Measure accepted accuracy, coverage, and unknown acceptance with TF-IDF or SetFit. Python. |
| [Nematic game](https://github.com/eduard-s/nematic-game) | Interactive 2D liquid crystal and material model with ions, fields, and local brushes. Reusable React component and web demo. TypeScript. |
| [TableProof](https://github.com/eduard-s/table-proof) | Find suspected errors in extracted PDF tables with source evidence, HTML reports, and optional local vision models. Python. |
| [ToolBoundary](https://github.com/eduard-s/tool-boundary) | Find changes to AI tool arguments, results, and errors across MCP and agent framework boundaries. Python and Node.js. |
| [Workflow engine: Python services](https://github.com/eduard-s/event-driven-workflow-orchestration-engine) | Runs parallel JSON workflows with an API, orchestrator, workers, PostgreSQL, and Redis Streams. |
| [Workflow engine: Go monolith](https://github.com/eduard-s/event-driven-workflow-orchestration-engine-monolith) | Runs durable JSON workflows in one Go app with PostgreSQL, retries, and recovery. |
| [Workflow engine: LangGraph monolith](https://github.com/eduard-s/event-driven-workflow-orchestration-engine-monolith-langgraph) | Runs JSON workflows with FastAPI and LangGraph. PostgreSQL stores state and checkpoints. |
| [Skills](https://github.com/eduard-s/skills) | Reusable Markdown skills for AI assistants. The first skill examines evidence for everyday science questions. |

## Use TinyTask

[Source installation and demo](https://github.com/eduard-s/tiny-task#try-the-support-inbox) · [Comparison with Prompt2Model and SetFit](https://github.com/eduard-s/tiny-task/blob/main/docs/COMPARISON.md) · [MVP plan](https://github.com/eduard-s/tiny-task/blob/main/docs/MVP_PLAN.md)

TinyTask is a source alpha. It trains a classifier for a stable label set and routes uncertain requests to review. Its acceptance report helps examine a local candidate before deployment.

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

## Use ToolBoundary

[Python on PyPI](https://pypi.org/project/tool-boundary-py/) · [Node.js on npm](https://www.npmjs.com/package/@esmirnov.ai/tool-boundary) · [Examples and explanation](https://esmirnov.ai/blog/tool-boundary/)

ToolBoundary compares what a tool parser expects with what a framework delivers to a handler or client. Use it to check input defaults, structured results, and error messages.

For Python 3.11 or later, install the MCP adapter in a virtual environment.

```sh
python -m pip install 'tool-boundary-py[mcp-v1]'
```

Save this as `check_tool.py`. It checks that the default `limit: 10` reaches a test handler and that its result reaches the MCP client.

```python
import asyncio

from pydantic import BaseModel
from tool_boundary import probe_mcp_tool, report_to_json


class Input(BaseModel):
    limit: int = 10


def count(limit: int = 10) -> dict[str, int]:
    return {"count": limit}


def register(server, handler):
    server.tool()(handler)


report = asyncio.run(probe_mcp_tool(
    case_id="python.default",
    tool_name="count",
    arguments={},
    reference=Input.model_validate,
    register=register,
    stub_handler=count,
    expected_structured={"count": 10},
))
print(report_to_json(report))
```

Run `python check_tool.py`. The JSON report includes an `outcome` and the expected and observed values. This example should return `pass`; a mismatch returns `fail` with the field path. `unsupported` and `harness_error` mean the check could not complete.

Use a stub handler when adapting the example to your own tool registration. The probe runs locally and needs no API key.

For Node.js 22 or later, install the package and the MCP adapter dependencies.

```sh
npm install @esmirnov.ai/tool-boundary @modelcontextprotocol/sdk zod
```

Follow the [MCP Node.js example](https://github.com/eduard-s/tool-boundary/blob/main/packages/typescript/examples/mcp-output.mjs) to check structured output. The [WorkflowAgent example](https://github.com/eduard-s/tool-boundary/blob/main/packages/typescript/examples/workflow-input.mjs) checks parser defaults and transforms through a separate adapter.

## Use TableProof

[Python on PyPI](https://pypi.org/project/table-proof-py/) · [Regression example](https://github.com/eduard-s/table-proof#try-the-real-regression-case) · [Benchmark evidence](https://github.com/eduard-s/table-proof/blob/main/benchmarks/README.md)

TableProof is an alpha Python library that finds suspected errors in extracted PDF tables. It compares cell text and row or column positions with the original PDF regions.

Use Python 3.11 or later in a virtual environment. Install the package, then audit a digital PDF and its Docling JSON export.

```sh
python -m pip install table-proof-py
table-proof source.pdf docling-export.json --html report.html --json report.json
```

`source.pdf` is the original PDF. `docling-export.json` must contain the extracted table cells and their source coordinates. Open `report.html` to inspect findings beside source evidence, or use `report.json` in your own workflow.

You can also run an audit from Python.

```python
import json
from pathlib import Path

from table_proof import audit_tables

document = json.loads(Path("docling-export.json").read_text())
report = audit_tables("source.pdf", document)
print(report.status)
report.export_json("report.json")
report.export_html("report.html", source_pdf="source.pdf")
```

The CLI returns `0` for `no_findings`, `1` for suspected errors (`review`), `3` for missing or ambiguous evidence (`uncertain`), and `2` for an execution error. `no_findings` means the selected checks found no error; it does not prove semantic accuracy.

To try it with supplied files, follow the [recorded regression case](https://github.com/eduard-s/table-proof#try-the-real-regression-case). The affected fixture reports two swapped row labels and exits with code `1`; the fixed control exits with code `0`.
