# go-darkwolf-style

[Русская версия](README-ru.md)

A Go coding-style skill with **25 local references and 25 code patterns**. The skill and references are in English.

## Install

Ask Codex:

```text
Use $skill-installer to install https://github.com/junhekdevsru/go-darkwolf-style/tree/main/go-darkwolf-style
```

Or link a checkout into the user skill directory on macOS/Linux:

```sh
git clone https://github.com/junhekdevsru/go-darkwolf-style.git go-darkwolf-style-repo
mkdir -p "$HOME/.agents/skills"
ln -s "$PWD/go-darkwolf-style-repo/go-darkwolf-style" "$HOME/.agents/skills/go-darkwolf-style"
```

Keep the checkout at that location. Update the existing installation when the skill is already installed.

## Use

```text
$go-darkwolf-style Implement this Go change.
$go-darkwolf-style Review this Go diff for applicable style conventions.
```

Automatic invocation is enabled by default. The agent reads the applicable local references before changing code. Explicit requirements and repository contracts take precedence. A local change stays local; architecture patterns apply where that architecture is used.

## References

Every reference specifies the declaration or operation style and includes its code pattern.

| Rule | Reference |
| --- | --- |
| DW-01 | [Private state and named accessors](go-darkwolf-style/references/01-private-state.md) |
| DW-02 | [Builder declaration and result](go-darkwolf-style/references/02-builders.md) |
| DW-03 | [Clone, Equal, and ownership](go-darkwolf-style/references/03-clone-and-equal.md) |
| DW-04 | [Collected mutations and commit](go-darkwolf-style/references/04-mutators.md) |
| DW-05 | [Named domain operations](go-darkwolf-style/references/05-domain-operations.md) |
| DW-06 | [Named IDs and closed statuses](go-darkwolf-style/references/06-ids-and-enums.md) |
| DW-07 | [Named domain collections](go-darkwolf-style/references/07-collections.md) |
| DW-08 | [Stored timestamps in UTC](go-darkwolf-style/references/08-utc-time.md) |
| DW-09 | [Independent validation errors](go-darkwolf-style/references/09-validation-errors.md) |
| DW-10 | [Sentinels and error context](go-darkwolf-style/references/10-error-context.md) |
| DW-11 | [Explicit constructor dependencies](go-darkwolf-style/references/11-constructor-dependencies.md) |
| DW-12 | [Interface and implementation declarations](go-darkwolf-style/references/12-interfaces.md) |
| DW-13 | [Read, write, and event capabilities](go-darkwolf-style/references/13-capability-interfaces.md) |
| DW-14 | [Optional module settings](go-darkwolf-style/references/14-functional-options.md) |
| DW-15 | [Command and query declarations](go-darkwolf-style/references/15-use-case-handlers.md) |
| DW-16 | [Handler and service composition](go-darkwolf-style/references/16-service-composition.md) |
| DW-17 | [Parent-package facades](go-darkwolf-style/references/17-package-facades.md) |
| DW-18 | [Explicit model conversions](go-darkwolf-style/references/18-model-conversions.md) |
| DW-19 | [Typed query construction](go-darkwolf-style/references/19-typed-queries.md) |
| DW-20 | [Repository update callbacks](go-darkwolf-style/references/20-repository-updates.md) |
| DW-21 | [Old and new event snapshots](go-darkwolf-style/references/21-change-events.md) |
| DW-22 | [Logging through decorators](go-darkwolf-style/references/22-logging-decorators.md) |
| DW-23 | [Names, receivers, and files](go-darkwolf-style/references/23-naming.md) |
| DW-24 | [Formatting, imports, and chains](go-darkwolf-style/references/24-layout.md) |
| DW-25 | [Behavioral tests and handwritten doubles](go-darkwolf-style/references/25-tests.md) |

Entry point: [SKILL.md](go-darkwolf-style/SKILL.md). Codex UI metadata: [agents/openai.yaml](go-darkwolf-style/agents/openai.yaml).

This is an instruction package with no CLI, MCP server, or private dependencies. It guides implementation and review; project tooling supplies automated checks. Examples using `slices` need Go 1.21 or later; generated code must match the target module.
