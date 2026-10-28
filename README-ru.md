# go-darkwolf-style

[English version](README.md)

Скилл Go-кодстайла: **25 локальных references и 25 образцов кода**. Сам скилл и все references написаны на английском.

## Установка

Попросите Codex:

```text
Используй $skill-installer и установи https://github.com/junhekdevsru/go-darkwolf-style/tree/main/go-darkwolf-style
```

Или создайте ссылку на checkout в пользовательском каталоге скиллов на macOS/Linux:

```sh
git clone https://github.com/junhekdevsru/go-darkwolf-style.git go-darkwolf-style-repo
mkdir -p "$HOME/.agents/skills"
ln -s "$PWD/go-darkwolf-style-repo/go-darkwolf-style" "$HOME/.agents/skills/go-darkwolf-style"
```

Оставляйте checkout по этому пути. Если скилл уже установлен, обновляйте существующую установку.

## Использование

```text
$go-darkwolf-style Реализуй это изменение в Go.
$go-darkwolf-style Проверь этот Go diff на применимые соглашения кодстайла.
```

Автоматический вызов включён по умолчанию. Перед изменением кода агент читает нужные локальные references. Явные требования и контракты репозитория имеют приоритет. Локальная правка остаётся локальной; архитектурные соглашения применяются к соответствующей архитектуре.

## References

В каждом файле — конкретные соглашения по записи и образец кода.

| Правило | Reference |
| --- | --- |
| DW-01 | [Закрытое состояние и getters](go-darkwolf-style/references/01-private-state.md) |
| DW-02 | [Форма builder](go-darkwolf-style/references/02-builders.md) |
| DW-03 | [Clone, Equal и владение данными](go-darkwolf-style/references/03-clone-and-equal.md) |
| DW-04 | [Форма mutator и фиксация изменений](go-darkwolf-style/references/04-mutators.md) |
| DW-05 | [Предметные операции](go-darkwolf-style/references/05-domain-operations.md) |
| DW-06 | [Типы ID и закрытые статусы](go-darkwolf-style/references/06-ids-and-enums.md) |
| DW-07 | [Именованные коллекции](go-darkwolf-style/references/07-collections.md) |
| DW-08 | [Хранение времени в UTC](go-darkwolf-style/references/08-utc-time.md) |
| DW-09 | [Накопление ошибок валидации](go-darkwolf-style/references/09-validation-errors.md) |
| DW-10 | [Sentinel errors и контекст](go-darkwolf-style/references/10-error-context.md) |
| DW-11 | [Зависимости конструктора](go-darkwolf-style/references/11-constructor-dependencies.md) |
| DW-12 | [Интерфейс и реализация](go-darkwolf-style/references/12-interfaces.md) |
| DW-13 | [Разделение read/write и событий](go-darkwolf-style/references/13-capability-interfaces.md) |
| DW-14 | [Functional options](go-darkwolf-style/references/14-functional-options.md) |
| DW-15 | [Декларации command/query handlers](go-darkwolf-style/references/15-use-case-handlers.md) |
| DW-16 | [Композиция сервисов](go-darkwolf-style/references/16-service-composition.md) |
| DW-17 | [Фасады пакетов](go-darkwolf-style/references/17-package-facades.md) |
| DW-18 | [Преобразования моделей](go-darkwolf-style/references/18-model-conversions.md) |
| DW-19 | [Типизированные запросы](go-darkwolf-style/references/19-typed-queries.md) |
| DW-20 | [Callback обновления репозитория](go-darkwolf-style/references/20-repository-updates.md) |
| DW-21 | [Old/New в событиях](go-darkwolf-style/references/21-change-events.md) |
| DW-22 | [Декораторы логирования](go-darkwolf-style/references/22-logging-decorators.md) |
| DW-23 | [Имена, receivers и файлы](go-darkwolf-style/references/23-naming.md) |
| DW-24 | [Форматирование и цепочки](go-darkwolf-style/references/24-layout.md) |
| DW-25 | [Тесты и рукописные doubles](go-darkwolf-style/references/25-tests.md) |

Точка входа: [SKILL.md](go-darkwolf-style/SKILL.md). Метаданные Codex: [agents/openai.yaml](go-darkwolf-style/agents/openai.yaml).

Отдельный CLI, MCP-сервер и приватные зависимости не нужны. Скилл задаёт соглашения для реализации и ревью, автоматические проверки выполняют инструменты проекта. Примеры с `slices` требуют Go 1.21 или новее; изменения должны соответствовать версии целевого модуля.
