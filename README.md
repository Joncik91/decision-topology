# Decision Topology

An OpenClaw skill that unobtrusively maps the topology of conversations where ideas evolve, branch, get rejected, pivot, or combine. Like git for thinking — runs in the background, viewable on request. All data stays local.

## What It Does

During conversations, the agent tracks the structural shape of how ideas evolve in the background:

- **Proposals** — distinct ideas or directions suggested
- **Pivots** — new directions emerging from rejections
- **Merges** — insights combining elements from multiple branches
- **Kills** — rejected paths with captured reasoning

The result is a persistent tree structure that captures *why* a conversation evolved, not just what was said.

## Features

- **Unobtrusive operation** — runs in the background, viewable on request
- **Auto-association** — checks existing trees before creating new ones
- **Concept indexing** — cross-tree linking via keyword concepts
- **ASCII rendering** — visual tree display in terminal
- **Mermaid export** — diagram export for documentation
- **Cross-tree analysis** — find patterns across multiple explorations
- **Companion .md files** — auto-generated for semantic search indexing

## Install

```bash
clawhub install decision-topology
```

Or manually copy the `SKILL.md`, `scripts/`, and `references/` folders into your OpenClaw workspace skills directory.

## Configuration

Trees are stored in `{baseDir}/trees/` by default. Override with the `TOPOLOGY_TREES_DIR` environment variable to store trees elsewhere (e.g. in a memory directory for semantic search indexing).

## Usage

The skill runs automatically — no setup needed. The user interacts naturally:

- *"Show me what we explored"*
- *"What did we kill?"*
- *"What shape is this conversation?"*
- *"What paths did we reject and why?"*
- *"Go back to that idea about X"*

### CLI Commands

```bash
node scripts/topology.js init '{"topic": "exploration topic"}'
node scripts/topology.js add-node '{"file": "<path>", "parent_id": "<id>", "type": "proposal", "summary": "description"}'
node scripts/topology.js kill-branch '{"file": "<path>", "node_id": "<id>", "reason": "why rejected"}'
node scripts/topology.js merge '{"file": "<path>", "source_ids": ["<id1>", "<id2>"], "summary": "merged insight"}'
node scripts/topology.js render '{"file": "<path>"}'
node scripts/topology.js export '{"file": "<path>"}'
node scripts/topology.js list
node scripts/topology.js stats '{"file": "<path>"}'
node scripts/topology.js analyze
node scripts/topology.js concept '{"list": true}'
```

### Example Tree Output

```
What stack to use for the web app?

(*) What stack to use for the web app?
|-- [x] Use a full React SPA (killed: too heavy for our use case)
|-- [*] Server-rendered with HTMX
|   |-- [x] Go + templ (killed: team doesn't know Go)
|   `-- (*) Node + Express + HTMX
`-- [x] Static site with JS sprinkles (killed: need real-time features)

5 branches explored, 3 killed, 2 active, depth 2
```

## Requirements

- Node.js (any recent version)
- OpenClaw (for skill integration)

## Schema

See [references/schema.md](references/schema.md) for the full v2 tree and node schema.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.

## License

MIT
