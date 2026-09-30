# Relational Database MCP

MCP server that helps AI agents discover, understand, and query complex relational databases, including large schemas, composite keys, relationships, triggers, constraints, and other structures commonly found in real-world databases.

> 🚧 **Early development** — This project is currently under active development.

## Why?

Relational databases in real-world systems are often much more complex than simple examples.

They may contain thousands of tables, composite primary keys, implicit relationships, triggers, legacy structures, inconsistent naming, and little or no documentation.

Giving an AI agent the entire database schema at once is inefficient and quickly exceeds its context.

Relational Database MCP aims to provide AI agents with a structured way to **discover and understand a database on demand**, exposing only the relevant context when it is needed.

## Goals

* 🔍 Discover database schemas automatically
* 🧩 Understand tables, columns, keys, indexes, and relationships
* 🔗 Discover relationships between tables, including inferred relationships
* 🧠 Provide relevant database context to AI agents on demand
* 🗺️ Find possible paths between related tables
* 🧪 Inspect representative data when schema metadata is insufficient
* 🛡️ Validate queries before execution
* ⚡ Work efficiently with large and complex databases
* 🔌 Support multiple relational database engines through adapters

## Architecture

The project is designed around database adapters, keeping database-specific logic separate from the core intelligence layer.

```text
                    AI Agent
                       │
                       │ MCP
                       ▼
              ┌──────────────────┐
              │ Relational DB MCP│
              ├──────────────────┤
              │ Schema Discovery │
              │ Schema Search    │
              │ Relationships    │
              │ Join Paths       │
              │ Query Validation │
              └────────┬─────────┘
                       │
              ┌────────┴─────────┐
              │ Database Adapter │
              └────────┬─────────┘
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
      Firebird    PostgreSQL     SQLite
```

## Database Support

Currently:

* 🚧 Firebird — in development

Planned:

* PostgreSQL
* SQLite
* Firebird
* ClickHouse

Database support will be implemented through independent adapters so that new database engines can be added without modifying the core.

## MCP

The project is built around the [Model Context Protocol](https://modelcontextprotocol.io/), allowing compatible AI clients and agents to interact with relational databases through standardized tools and resources.

Planned capabilities include:

```text
search_schema
describe_table
find_relationships
find_join_path
sample_rows
validate_query
execute_query
```

## Development

### Requirements

* Go 1.XX+
* A supported database

### Clone

```bash
git clone https://github.com/tas48/relational-database-mcp.git
cd relational-database-mcp
```

### Build

```bash
go build ./...
```

### Run

> Configuration and database connection options are still under development.

## Contributing

Contributions are welcome.

You can contribute by:

* Adding support for new database engines
* Improving schema discovery
* Improving relationship detection
* Adding MCP tools
* Improving performance
* Fixing bugs
* Improving documentation
* Sharing ideas and use cases

Feel free to open an issue or submit a pull request.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
