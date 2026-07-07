# acp-repl Agent Notes

`acp-repl` is a small Go CLI that starts a stdio Agent Client Protocol (ACP)
server command and opens an interactive terminal prompt loop for sending ACP
turns.

## Project Layout

- `cmd/acp-repl/main.go`: executable entrypoint.
- `cmd/acp-repl/cmd/command.go`: Cobra command, flags, examples, and argument validation.
- `internal/apps/acprepl`: ACP session setup, prompt loop, permission handling, and output.
- `internal/apps/appio`: synchronized writer helpers.
- `internal/logging`: process-wide structured logging setup.

## Development Rules

- Keep stdout focused on REPL interaction. Debug and provider process logs must
  go to stderr.
- Keep ACP provider examples in README/help current with supported providers.
  Do not add abandoned provider examples.
- Preserve the `-- <acp-server-cmd> [args...]` contract. Arguments before `--`
  are CLI flags; arguments after it are passed to the ACP server.
- Model and mode flags should use ACP session config options. Legacy
  `session/set_mode` is only a fallback for older servers.
- Prefer small, focused changes. Avoid unrelated workflow, orchestration, or
  product-policy docs in this repository.

## Commands

```sh
task test
task lint
task
```

Equivalent direct commands:

```sh
go test ./...
go tool golangci-lint run ./...
go build -o bin/acp-repl ./cmd/acp-repl
```
