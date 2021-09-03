# Custom zsh prompt<!-- omit in toc -->

How customize the zsh prompt for the macOS terminal to show the name of the current git branch.

## Table of contents<!-- omit in toc -->

- [Documentation](#documentation)
- [Configuration](#configuration)
- [Formatting description](#formatting-description)

## Documentation

For additional information see the official z shell [documentation](http://zsh.sourceforge.net).

## Configuration

This is the result for the customization described in this guide:

```text
userName ~ %
userName ~/Developer %
userName Developer/Projects %
userName Projects/SomethingDemo %
```

If the current directory is a git repository, the prompt will display the name of the current branch:

```text
userName Projects/ProjectFooBar (master) %
```

To customize the zsh prompt in this style, navigate to the hidden configuration file under the home directory (`/~/.zshrc`). Create the file if it's not already there; otherwise, make a backup copy.

Open the `.zshrc` file and add these lines to the end of the file:

```zsh
# Load version control information
autoload -Uz vcs_info
precmd() { vcs_info }

# Format the vcs_info_msg_0_ variable
zstyle ':vcs_info:git:*' formats ' (%F{10}%b%f)'

# Set up the prompt
setopt PROMPT_SUBST

# Define the new prompt
PROMPT='%n %2~${vcs_info_msg_0_} %# '
# The style is: userName parentDir/currentDir (GitBranch) %

# This is the same prompt with bold and color directory styling:
# PROMPT='%n %B%F{45}%2~%b%f${vcs_info_msg_0_} %# '
```

## Formatting description

The zsh `PROMPT` variable is what sets the custom appearance in the terminal. There are many customization options. The ones specific to this example are described below:

| Option             | Description                                                         |
| ------------------ | ------------------------------------------------------------------- |
| %n                 | Show the name of the current user                                   |
| %B%b               | Mark the start and end of bold text                                 |
| %F{45}%f           | Mark the start and end of blue color text                           |
| %2~                | Show the last two elements in the path to the current directory     |
| ${vcs*info_msg_0*} | Show the name of the current branch (when in a git directory)       |
| %F{10}%f           | Mark the start and end of green color text                          |
| %#                 | Show a `#` prompt under root privileges, otherwise `%` for standard |
