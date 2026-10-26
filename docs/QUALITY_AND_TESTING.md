# CLI Development and Operational Safety Guide

stacli-Opsli is an operations-oriented CLI workspace. Inspect the current source and manifest to identify the exact executable, commands, flags, and supported integrations.

## Setup and command discovery

```bash
git clone https://github.com/kandisaikishore/stacli-Opsli.git
cd stacli-Opsli
```

Use the package/build instructions in the repository. Document the actual help command, prerequisites, configuration variables, and supported subcommands. Do not include real credentials or production resource identifiers in examples.

## Command design and validation

For each implemented command, document:
- Purpose and required permissions
- Required/optional arguments and defaults
- Example invocation and expected output
- Exit codes and error behavior
- Whether it reads, creates, modifies, or deletes resources

Test missing arguments, invalid values, unknown subcommands, malformed configuration, and dependency failures. Errors should explain the next step without printing secrets.

## Destructive operations

For commands that delete, overwrite, revoke, or mutate resources, provide a dry-run or preview when feasible. Require explicit confirmation for destructive interactive actions, and document safe non-interactive behavior. Cancellation must not mutate state. Tests should prove that dry-run performs no writes.

## Security and reliability

Use least-privilege credentials, avoid shell-injection-prone command construction, and never log tokens. Bound retries and timeouts for remote operations. Test partial failure and repeated execution to determine whether operations are idempotent.

## Pull-request checklist

- [ ] Update command help and docs with the implementation.
- [ ] Test success, invalid input, permission denial, and cancellation.
- [ ] Verify dry-run behavior for destructive operations.
- [ ] Run the declared lint/test/build commands.
- [ ] State any live integration checks that were not run.
