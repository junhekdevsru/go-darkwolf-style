---
name: go-darkwolf-style
description: "Apply Darkwolf Go coding conventions when writing, refactoring, or reviewing Go. Use the matching local references for concrete declaration, construction, mutation, error, handler, repository, and test patterns."
---

# Go Darkwolf Style

Write code in the forms specified by the local references below. Each reference contains the convention and its code pattern.

Read the applicable references before editing. Resolve paths relative to this skill directory. Examples use neutral names and companion types from the surrounding code; adapt those names to the target module.

Honor explicit task requirements, repository contracts, and the target Go version. Apply model conventions to models and architecture conventions to the matching application modules. Keep a local fix local. Use modern syntax that preserves the specified ownership and validation behavior.

## References

| Rule | Read when | Local reference |
| --- | --- | --- |
| DW-01 | Declaring a domain entity | `references/01-private-state.md` |
| DW-02 | Adding or extending a model builder | `references/02-builders.md` |
| DW-03 | Returning, storing, or comparing mutable model state | `references/03-clone-and-equal.md` |
| DW-04 | Adding coordinated changes to an existing entity | `references/04-mutators.md` |
| DW-05 | Implementing a state transition | `references/05-domain-operations.md` |
| DW-06 | Declaring significant IDs or a closed status set | `references/06-ids-and-enums.md` |
| DW-07 | Adding collection behavior for a domain type | `references/07-collections.md` |
| DW-08 | Setting or comparing domain timestamps | `references/08-utc-time.md` |
| DW-09 | Validating a value or several constructor inputs | `references/09-validation-errors.md` |
| DW-10 | Propagating or translating an operation failure | `references/10-error-context.md` |
| DW-11 | Constructing a handler or service | `references/11-constructor-dependencies.md` |
| DW-12 | Declaring a handler or a composed module | `references/12-interfaces.md` |
| DW-13 | Choosing a collaborator interface | `references/13-capability-interfaces.md` |
| DW-14 | Adding optional settings to an infrastructure module | `references/14-functional-options.md` |
| DW-15 | Adding a use case in a handler-based application | `references/15-use-case-handlers.md` |
| DW-16 | Grouping related use cases into a service | `references/16-service-composition.md` |
| DW-17 | Extending an existing parent-package facade | `references/17-package-facades.md` |
| DW-18 | Crossing domain, application, storage, or transport representations | `references/18-model-conversions.md` |
| DW-19 | Extending an existing typed query interface | `references/19-typed-queries.md` |
| DW-20 | Updating a stored entity | `references/20-repository-updates.md` |
| DW-21 | Publishing an event for a persisted change | `references/21-change-events.md` |
| DW-22 | Adding shared handler logging or tracing | `references/22-logging-decorators.md` |
| DW-23 | Naming declarations and files | `references/23-naming.md` |
| DW-24 | Formatting declarations or fluent calls | `references/24-layout.md` |
| DW-25 | Testing changed domain or handler behavior | `references/25-tests.md` |

## Completion

Check the changed code against every applicable reference. Run gofmt and the relevant project checks. For ownership or mutation changes, verify copying and rollback; for handler changes, verify errors and events. Report actual checks and concrete findings. Keep review-only requests read-only.
