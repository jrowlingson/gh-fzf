# gh fzf

An fzf wrapper around the GitHub CLI.

## Installation

1. Install the [GitHub CLI](https://github.com/cli/cli#installation) (`>= v2.0.0`) and [fzf](https://github.com/junegunn/fzf#installation) if you don't already have them. For example:
   - **Homebrew:** `brew install gh fzf`
   - **DNF:** `sudo dnf install gh fzf`
   - ... see the links above for other package managers
2. Authenticate with the GitHub CLI: `gh auth login`
3. Install the extension: `gh extension install benelan/gh-fzf`
4. [???](#usage)
5. PROFIT

## Usage

```sh
gh fzf <command> [flags]
```

The extension adds a new command that wraps GitHub's "list" subcommands with fzf to make them fuzzy findable. A preview of the current selection is displayed, and keybindings are available to perform actions on the item.

There are a few global keybindings that can be used with any `gh fzf` command:

- `ctrl-o`: Open the selected item in the browser
- `ctrl-y`: Copy the selected item's URL to the clipboard
- `ctrl-r`: Reload the list to its initial state
- `alt-1` to `alt-9`: Change the number of items fetched from GitHub to 100, 200, ..., 900

### issue

**Usage:** `gh fzf issue [flags]`

**Aliases:** `i`, `issues`, `-i`, `--issue`, `--issues`

**Flags:** See `gh issue list --help` for available options

**Keybindings:**

- `enter`: Edit the selected issue in the CLI via prompts (see `gh issue edit --help`)
- `alt-o`: Checkout the branch linked to the selected issue, creating one if necessary (see `gh issue develop --help`)
- `alt-c`: Add a comment to the selected issue (see `gh issue comment --help`)
- `alt-X`: Close the issue (see `gh issue close --help`)
- `alt-O`: Reopen the issue (see `gh issue reopen --help`)
- `alt-a`: Filter the list, showing issues assigned to you
- `alt-A`: Filter the list, showing issues authored by you
- `alt-m`: Filter the list, showing issues where you are mentioned

### pr

**Usage:** `gh fzf pr [flags]`

**Aliases:** `p`, `prs`, `-p`, `--pr`, `--prs`

**Flags:** See `gh pr list --help` for available options

**Keybindings:**

- `enter`: Edit the selected pull request in the CLI via prompts (see `gh pr edit --help`)
- `alt-o`: Checkout the pull request's branch (see `gh pr checkout --help`)
- `alt-c`: Add a comment to the selected issue (see `gh issue comment --help`)
- `alt-C`: Show the pull request's status checks (see `gh pr checks --help`)
- `alt-d`: Show the pull request's diff (see `gh pr diff --help`)
- `alt-r`: Start/continue/finish a review for the pull request (see `gh pr review --help`)
- `alt-R`: Mark a draft pull request as "ready for review" (see `gh pr ready --help`)
- `alt-M`: Merge the pull request (see `gh pr merge --help`)
- `alt-X`: Close the pull request (see `gh pr close --help`)
- `alt-O`: Reopen the pull request (see `gh pr reopen --help`)
- `alt-a`: Filter the list, showing issues assigned to you
- `alt-A`: Filter the list, showing issues authored by you

### run

**Usage:** `gh fzf run [flags]`

**Aliases:** `r`, `runs`, `-r`, `--run`, `--runs`

**Flags:** See `gh run list --help` for available options

**Keybindings:**

- `enter`: Watch the selected run's status updates (see `gh run watch --help`)
- `alt-l`: Show the selected run's logs (see `gh run view --help`)
- `alt-r`: Rerun the selected run (see `gh run rerun --help`)
- `alt-x`: Cancel the selected run (see `gh run cancel --help`)
- `alt-b`: Filter the list, showing runs from the current branch
- `alt-u`: Filter the list, showing runs triggered by you
- `alt-f`: Filter the list, showing failed runs

## Configuration

Environment variables are used to configure different options in `gh-fzf`.

| Variable               | Description                                                                                                                                                                            | Default                                                                                                      |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `GH_FZF_DEFAULT_LIMIT` | the initial number of items to request from GitHub. The number of items can be changed at runtime with the `alt+1` to `alt+9` commands, see the [Usage](#usage) section for more info. | `69`                                                                                                         |
| `GH_FZF_COPY_CMD`      | The command used by your operating system to copy an item's URL to the clipboard. Expects the URL from stdin. This only needs to be set if the default doesn't work.                   | [see code](https://github.com/benelan/gh-fzf/blob/432aac672061ac25b67c396d60fc20839aed5449/gh-fzf#L78-L88C1) |

## Related projects

- [`gh-f`](https://github.com/gennaro-tedesco/gh-f): another `fzf` wrapper around `gh`, which also provides some `git` functionality.

**NOTE:** `gh-fzf` leaves `git` functionality to other tools, and instead focuses on providing more keybindings for the GitHub commands. The following `fzf` wrappers around `git` are both good options to fill that gap:

- [`forgit`](https://github.com/wfxr/forgit) (I use this one)
- [`git-fuzzy`](https://github.com/bigH/git-fuzzy)
