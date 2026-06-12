# vale-ears

A [Vale](https://vale.sh/) package for validating requirements written in the [EARS (Easy Approach to Requirements Syntax)](https://alistairmavin.com/ears/) format.

EARS constraints natural language into a structured, standardized format to reduce ambiguity and improve consistency in requirements engineering.

## Rules

### `ears.Syntax`

Checks that any sentence containing the word `shall` conforms to one of the standard EARS patterns:
- **Ubiquitous:** The `<system>` shall `<action>`
- **Event-driven:** When `<trigger>`, the `<system>` shall `<action>`
- **State-driven:** While `<precondition>`, the `<system>` shall `<action>`
- **Unwanted behavior:** If `<trigger>`, then the `<system>` shall `<action>`
- **Optional feature:** Where `<feature>`, the `<system>` shall `<action>`

### `ears.Shall`

Ensures that requirements use the word `shall` rather than `must`, `will`, `should`, or `may` (which are commonly discouraged in formal requirements).

## Installation

Add the package to your `.vale.ini`:

```ini
Packages = https://github.com/tbhb/vale-ears/releases/latest/download/ears.zip

[*.md]
BasedOnStyles = ears
```

Then run:

```bash
vale sync
```

## Contributing

See the `Justfile` for development commands.
