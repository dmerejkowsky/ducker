# Ducker

A terminal app for managing docker containers, inpired by [K9s](https://k9scli.io/)

This is perhaps obviously very much a work in progress...


![](https://raw.githubusercontent.com/robertpsoane/ducker/master/demo.gif?raw=true)


## Installation

There isn't currently a downloadable build; to install you will need cargo installed:

```bash
cargo install --locked ducker
```

### AUR

You can install `ducker` from the [AUR](https://aur.archlinux.org/packages/ducker) with using an [AUR helper](https://wiki.archlinux.org/title/AUR_helpers).

```sh
paru -S ducker
```

## Configuration

Ducker is configured via a yaml file found in the relevant config directory for host platform.  On linux this is `~/.config/ducker/config.yaml`.

The following table summarises the available config values:

| Key          | Default     | Description                                                                                                                 |
|--------------|-------------|-----------------------------------------------------------------------------------------------------------------------------|
| prompt       | 🦆          | The default prompt to display in the command pane                                                                           |
| default_exec | `/bin/bash` | The default prompt to display in the command pane. NB - currently uses this for all exec's; it is planned to offer a choice |
| theme        | [See below] | The colour theme configuration                                                                                              |

If a value is unset or if the config file is unfound, Ducker will use the default values.  If a value is malformed, Ducker will fail to run.

To create a fully populated default config, run ducker with the `-e/--export-default-config` flag; this will write the default config to the default location, overwriting any existing config.

### Themes

By default, ducker uses the terminal emulator's preset colours.  However, it is possible to set a custom colour theme in config.  This is set in the `theme` section of the config file.  The following table describes the theme options.  The default theme provides the colours provided in the GIF in this README.

| Key                | Default   | Description                                                                                          |
|--------------------|-----------|------------------------------------------------------------------------------------------------------|
| use_theme          | `false`   | When `true` uses the colour scheme defined in config, when `false` uses the default terminal colours |
| title              | `#96E072` | The colour used for the Ducker font in the header                                                    |
| help               | `#EE5D43` | The colour used in the help prompts in the header                                                    |
| background         | `#23262E` | The colour used in the background                                                                    |
| footer             | `#00E8C6` | The colour used for the text in the footer                                                           |
| success            | `#96E072` | The colour used for a successful result                                                              |
| error              | `#EE5D43` | The colour used for an error result                                                                  |
| positive_highlight | `#96E072` | The colour used for highlighting in a happy state                                                    |
| negative_highlight | `#FF00AA` | The colour used for highlighting in a sad state                                                      |

### Tmux

Some characters in ducker use italics/boldface.  This doesn't work by default when running in tmux.  To fix this, add the following to your add to tmux.conf
```
set -g default-terminal "tmux-256color"
set -as terminal-overrides ',xterm*:sitm=\E[3m'
```
