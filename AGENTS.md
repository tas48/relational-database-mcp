# AGENTS.md

## Project

Relational Database MCP is an open-source MCP server that helps AI agents discover, understand, and query complex relational databases.

The project is written in Go and is designed around independent database adapters.

## Core principles

* Keep database-specific logic inside adapters.
* Keep the core independent from any specific database engine.
* Prefer simple, explicit, maintainable Go code.
* Do not add unnecessary abstractions.
* Do not couple the core to a specific LLM or AI provider.
* MCP is the interface to AI agents; database intelligence should remain independent from the MCP layer.
* Prefer read-only database operations unless write support is explicitly required and reviewed.
* Never expose credentials or sensitive database information in logs, errors, tests, or documentation.

## Architecture

The project is organized around:

```text
cmd/
    Application entrypoints

internal/core/
    Database-independent domain models and logic

internal/database/
    Database adapter interfaces and registry

internal/intelligence/
    Schema discovery, search, relationship analysis, query planning, etc.

internal/mcp/
    MCP server, tools, resources, and protocol integration

adapters/
    Database-specific implementations
```

## Database adapters

Each database engine must implement the common database adapter interface.

Database-specific SQL, metadata queries, type mappings, and compatibility logic must remain inside its adapter.

Do not add database-specific behavior to the core when it can be implemented inside an adapter.

## Development

Before considering a change complete:

```bash
go test ./...
go vet ./...
go build ./...
```

Prefer adding tests for new behavior and bug fixes.

## Code style

Follow standard Go conventions.

Use `gofmt` and keep functions focused.

Prefer clear names over comments.

Comments should explain why something exists when the code itself cannot make the reason obvious.

Avoid premature abstractions and unnecessary interfaces.

## Commits

Use Conventional Commits.

Format:

```text
<type>(<scope>): <description>
```

Common types:

* `feat` — new functionality
* `fix` — bug fix
* `refactor` — internal restructuring
* `perf` — performance improvement
* `test` — tests
* `docs` — documentation
* `chore` — maintenance
* `build` — build or dependency changes
* `ci` — CI/CD changes

Examples:

```text
feat(firebird): add table discovery
feat(mcp): expose schema search tool
fix(schema): handle composite primary keys
test(firebird): add metadata tests
docs: update installation instructions
refactor(core): simplify database adapter interface
```

Keep commits focused on a single logical change.

Do not combine unrelated changes in the same commit.

## Pull requests

Pull requests should:

* explain what changed and why;
* include tests when appropriate;
* keep changes focused;
* avoid unrelated formatting or refactoring;
* document breaking changes.

## Agent behavior

Before making significant changes:

1. Inspect the existing architecture.
2. Identify the appropriate package or adapter.
3. Follow existing patterns.
4. Avoid modifying unrelated code.
5. Run relevant tests after the change.

Do not create new files, abstractions, dependencies, or architecture without a reason.

When requirements are ambiguous, prefer the smallest implementation consistent with the project's architecture.
