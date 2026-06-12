<!-- vale ears = NO -->
# vale-ears

A [Vale](https://vale.sh/) package for validating requirements written in the [EARS (Easy Approach to Requirements Syntax)](https://alistairmavin.com/ears/) format.

EARS constraints natural language into a structured, standardized format to reduce ambiguity and improve consistency in requirements engineering.

## Rules

### `ears.Syntax`

Checks that any sentence containing the word `shall` conforms to one of the standard EARS patterns:

- **Ubiquitous:** the `<system>` shall `<action>`
- **Event-driven:** when `<trigger>`, the `<system>` shall `<action>`
- **State-driven:** while `<precondition>`, the `<system>` shall `<action>`
- **Unwanted behavior:** if `<trigger>`, then the `<system>` shall `<action>`
- **Optional feature:** where `<feature>`, the `<system>` shall `<action>`

### `ears.Shall`

Ensures that requirements use the word `shall` rather than `must`, `will`, `should`, or `may` (which formal requirements commonly discourage).

### `ears.PassiveVoice` (and `ears.PassiveVoiceAdverb`)

Ensures requirements use the active voice. EARS dictates that the system (or user) must explicitly be the actor performing the action.

### `ears.WeakWords`

Flags words that introduce ambiguity into requirements (such as `approximately`, `usually`, `several`, `fast`, `robust`, `user-friendly`). Requirements should be precise and measurable.

## Examples

The following are valid EARS requirements:

<!-- vale Google = NO -->
<!-- vale ai-tells = NO -->
<!-- vale ai-tells-experimental = NO -->
<!-- vale ears = YES -->

The system shall log all errors.

When a user logs in, the system shall display the dashboard.

While the server is running, the application shall accept connections.

If the network drops, then the system shall retry the connection.

Where the system detects a camera, the application shall record video.

<!-- vale ears = NO -->
<!-- vale ai-tells-experimental = YES -->
<!-- vale ai-tells = YES -->
<!-- vale Google = YES -->

The following are examples of **violations** that `vale-ears` will flag:

- `ears.Syntax`: "The system shall, when it receives a message, log the error." (Does not match a standard EARS template)
- `ears.Shall`: "The system must log all errors." (Uses `must` instead of `shall`)
- `ears.PassiveVoice`: "All errors shall be logged by the system." (Written in passive voice)
- `ears.WeakWords`: "The system shall load the dashboard fast." (Uses ambiguous weak words like `fast`)

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
