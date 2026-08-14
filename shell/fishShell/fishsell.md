# Fish shell notes

User friendly and smart command line. More details [here](https://fishshell.com).

- [Fish shell notes](#fish-shell-notes)
  - [Installation, setup \& run](#installation-setup--run)
  - [Configuration file](#configuration-file)
- [Interactive usage](#interactive-usage)
  - [Useful commands](#useful-commands)
  - [Variables](#variables)
  - [Expansion](#expansion)
  - [Quoting](#quoting)
- [Scripting](#scripting)


## Installation, setup & run

```bash
sudo apt-get install fish
fish
# exit to finish the session.
```
Maybe is not a good idea to change the default shell of the system, ubuntu requires a bourne-compatible shell to read /etc/profile.

For run fish scripts must use the shebang `#!/usr/bin/env fish`

## Configuration file

The configuration file (as .bashrc) is stored at `~/.config/fish/config.fish`. Also all the .fish scripts at `~/.config/fish/conf.d/` are also automatically executed before the `config.fish`.

# Interactive usage
## Useful commands
Same as bash: `cd`,`ls`,`man`,`mv`,`cp`,`less`, etc...

The commands finish with either a semicolon or a newline.

## Variables

## Expansion

## Quoting
* Either single or double quotes, but:
  * In single quotes : No variable expansions.
  * In double quotes : Variable expansion and command subs.


# Scripting

