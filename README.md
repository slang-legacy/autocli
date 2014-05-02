# autoCLI
[insert badges here... preferably the flat-style ones roots uses]

## what is it?
AutoCLI helps you make a full command line interface for a node.js program, with only describing its inputs (written in [JSON Schema](http://json-schema.org/)).

AutoCLI is not another arg-parser (if you want one of those, use [argparse](https://github.com/nodeca/argparse)). There are already plenty of great arg-parsing libraries, but they force you to describe how you want your CLI to work. This is bad because there's a lot of widely accepted conventions that you shouldn't need to think about when making a CLI.

AutoCLI doesn't ask you "how should it work?", it just asks "what info does your program need?". The entire CLI is built around that. You describe your program's input as a single JSON schema.

## features
- automatic `--version` command (obtained from `pacakge.json`)
- automatic `--help` text generation
- opinionated design tries to prevent you from making a horrible CLI (the world has enough of those already)
  - you can't break the naming/formatting conventions used by standard utils
  - the `--no-*` convention is automatically used if your option defaults to `false`
  - single-letter option shorthands are assigned based on a database of standard GNU shorthands
- typical args like `--verbose` are accepted automatically (your program should handle these, see [standard opts](#standard-opts) for the full list)
- `[command name].opts` files are supported automatically for the current directory.

## example
Lets say you have a program that [... write an interesting example here ...]

## standard opts
This is a list of options that nearly all programs should be able to take. AutoCLI defines them automatically.
- verbose

## for best results...
This section is a collection of common "best practices" that will help your CLI turn out the best CLI it can be.

### don't try to write your own version or help commands
Both of these are done for you. The version is read from your `package.json`. The help text is generated from the description, name, authors, and other stuff in your `package.json`; nearly everything in your schema (especially `description`s); and best practices gathered from studying tons of command-line programs.

Besides, you can't even name an option `version` or `help` - those are reserved names.

### naming convention
JavaScript uses camelCased names (it's baked into the langauge itself, you don't have a choice), but command line programs use `--dashed-args` (which is a convention that you [shouldn't](http://www.gnu.org/prep/standards/html_node/Command_002dLine-Interfaces.html#Command_002dLine-Interfaces) have a choice about). So, autoCLI will deal with this conversion for you. Just name your properties in camelCase in the schema, they will be converted into `--dashed-args` in the command line, and the object that you get back will have the same camelCase properties that you specified. Everyone wins!

### choosing names
The GNU maintains a wonderful list of [standard option names](http://www.gnu.org/prep/standards/html_node/Option-Table.html). Try to choose names from this list - it will help reduce the learning curve for your program by sticking with the same common vocabularly that is already used by standard UNIX and GNU utils. Also, the single-letter shorthands that autoCLI assigns are optimized for names from this list.

### try to list popular options first
Objects don't _technically_ have any order in their keys, but the order that you put them in can be determined and it will be intrepreted as their importance. So, autoCLI will use this info to assign single-letter shorthands to important options first, and keep important options on the top of the help text.







