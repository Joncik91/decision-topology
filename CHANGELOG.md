# Changelog

All notable changes to this project will be documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.2] - 2026-03-02

### Fixed
- **Shell injection vulnerability:** Added stdin support to topology.js so the agent pipes JSON args instead of embedding user-derived content in shell strings. This prevents shell metacharacter injection (e.g. `$(cmd)`, backticks, `&&`) in topics, summaries, queries, and other user input.

### Changed
- All SKILL.md command examples now use stdin piping pattern (`echo '{}' | node topology.js cmd`) instead of inline shell args
- CLI router reads args from stdin when no argv[3] is provided; no-arg commands (`list`, `analyze`, `rebuild-index`) skip stdin entirely
- Updated README and CONTRIBUTING.md examples to match

## [1.0.1] - 2026-03-02

### Changed
- Reframed "silent/covert" language as "unobtrusive" to better reflect intent
- Renamed "Silent Operation" section to "Unobtrusive Operation"
- Clarified that nodes store structural summaries, never verbatim conversation content

### Added
- Privacy note in SKILL.md: user consents by installing, all data stays local
- Rule 8: local only — no network calls, no external APIs, no telemetry
- `always: true` in metadata to match always-on activation behavior

## [1.0.0] - 2026-03-02

### Added
- Initial release
- Tree structure with 4 node types: root, proposal, pivot, merge
- 3 status values: active, dead, merged
- Schema v2 with 6-char hex IDs
- 13 CLI commands: init, add-node, kill-branch, merge, render, export, fork, list, stats, associate, analyze, concept, rebuild-index
- Concept index with automatic cross-tree linking
- Companion .md file generation for semantic search indexing
- Auto-association: score-based matching to existing trees
- ASCII tree rendering and Mermaid diagram export
- Cross-tree analysis with pattern detection
- Configurable storage via `TOPOLOGY_TREES_DIR` environment variable
- Zero external dependencies (Node.js built-ins only)
