# .files

My dotfile configuration

## Usage

See [Prerequisites](./README.md#prerequisites) section before using.

Refer to the [Resources / References](./README.md#resources--references) Section to learn about how to use Chezmoi.

**NOTE:** You shouldn't create dotfiles directly in the Chezmoi repo, instead, use `chezmoi add` to add the dotfiles to the chezmoi repo.

```bash
# QUICK INSTALL
chezmoi init --apply git@github.com:pszponder/dotfiles.git
```

List of commands:

```bash
# Initialize chezmoi on a new machine (should only need to do this once)
chezmoi init git@github.com:pszponder/dotfiles.git
```

```bash
# Pull changes from remote repo
chezmoi update                                           # Pulls and applies changes from remote

chezmoi git pull -- --autostash --rebase && chezmoi diff # Pull & view changes, don't apply
chezmoi apply                                            # If changes from above command are ok, apply them

# Add a directory / file to be tracked by chezmoi
chezmoi add $FILE # Replace $FILE with absolute path to dotfile/directory you want chezmoi to manage

# cd into the chezmoi repo from anywhere
chezmoi cd

# Edit a file managed by chezmoi
# (alternatively, "chezmoi cd" and edit files in the chezmoi repo w/ editor of choice)
chezmoi edit                # Open chezmoi source directory
chezmoi edit $FILE          # Replace $FILE with abs path to dotfile path you wish to edit
chezmoi edit --apply $FILE  # Apply changes when you quit the editor
chezmoi edit --watch $FILE  # Apply changes whenever you save the file

# See what changes chezmoi would make (without applying changes)
chezmoi diff

# Apply changes to dotfiles tracked by chezmoi to your computer
chezmoi apply -vn # (alternative to chezmoi diff)
chezmoi apply -v  # Actually apply changes

# Merge changes from your home directory into chezmoi repository
chezmoi merge $FILE # Replace $FILE with dotfile abs path you with to merge into chezmoi

# Push changes into remote repo
chezmoi cd # cd into local chezmoi repo
git add .
git commit -m "your commit message"
git push

# Exit the shell in the chezmoi source directory to return to where you were (if you use "chezmoi cd")
exit
```

## Prerequisites

### Setup Homebrew

Execute the following script to install and setup homebrew

```bash
./scripts/setup_homebrew.sh
```

### Setup ZSH

If you are not using `ZSH` as your default shell, run the following script

```bash
./scripts/setup_zsh.sh
```

### Fonts

Installing Fonts:
1. Download one or more fonts from the list
    1. [CaskaydiaCove Nerd Font](https://www.nerdfonts.com/font-downloads)
    2. [Comic Code](https://tosche.net/fonts/comic-code) (May need to use `Symbols Nerd Font` as secondary for Powerline Support)
    3. [Monaspace](https://github.com/githubnext/monaspace)
    4. [JetBrains mono](https://www.jetbrains.com/lp/mono/)
    5. [Nerd Fonts](https://www.nerdfonts.com/font-downloads) (Grab and install Symbols Nerd Font to be used for fallback when PL not integrated into language)
2. After downloading, unpack each font-family into its own directory under `~/.local/share/fonts`
3. Run `fc-cache -f` to rebuild the font cache

If you are using a font family w/o support for PowerLine fonts, you can update the `fonts.conf` file under `~/.config/fontconfig` directory. For each font family, specify the `SymbolsNerdFont` as the secondary font.

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<!-- ~/.config/fontconfig/fonts.conf -->
<fontconfig>
    <!-- Rule for ComicCode -->
    <match target="pattern">
        <test qual="any" name="family">
            <string>ComicCodeLigatures</string>
        </test>
        <edit name="family" mode="append" binding="strong">
            <string>SymbolsNerdFont</string>
        </edit>
    </match>

    <!-- Rule for JebBrainsMono -->
    <match target="pattern">
        <test qual="any" name="family">
            <string>JetBrainsMono</string>
        </test>
        <edit name="family" mode="append" binding="strong">
            <string>SymbolsNerdFont</string>
        </edit>
    </match>
</fontconfig>
```

Refer to the following video for setting up fonts in different terminals: [Elijah Manor - Effective Nerd Fonts in Multiple Terminals](https://www.youtube.com/watch?v=mQdB_kHyZn8)

To test if your font is properly installed, you can create a bash script (from Elijah's video). If the Nerd Font is properly setup, you will see the correct symbols when the script gets executed.

```bash
#!/usr/bin/env bash

# https://gist.github.com/elijahmanor/c10e5787bf9ac6b8c276e47e6745826c

smoke_tests="Normal
\033[1mBold\033[22m
\033[3mItalic\033[23m
\033[3;1mBold Italic\033[0m
\033[4mUnderline\033[24m
== === !== >= <= =>
󰐊     󰄉      󰑓 󰒲 "

printf "%b" "${smoke_tests}"
```

## Optional

### Color Themes

- [Catppuccin Theme](https://github.com/catppuccin)
- [Catppuccin Theme - Gnome Terminal](https://github.com/catppuccin/gnome-terminal)
- [Catppuccin Theme - NeoVim](https://github.com/catppuccin/nvim)

### GUI Apps

If on linux, refer to `./scripts/install_apps.sh`
If on macOS, refer to `./scripts/setup_brew.sh` (installs CLI + GUI tools on macOS)

### Programming Languages

Run `./scripts/install_rtx-polyglot.sh` to setup [rtx](https://github.com/jdx/rtx) and install pre-configured languages from `./rtx/.config/rtx/config.toml`

## Resources / References

Managing Dotfiles w/ chezmoi
- [chezmoi - Dotfiles Manager](https://www.chezmoi.io/)
- [chezmoi - Quick Start](https://www.chezmoi.io/quick-start/)
- [chezmoi - How do I edit my dotfiles with chezmoi?](https://www.chezmoi.io/user-guide/frequently-asked-questions/usage/#how-do-i-edit-my-dotfiles-with-chezmoi)
- [chezmoi - Daily Operations](https://www.chezmoi.io/user-guide/daily-operations/)
- [Jerry Ng - How to Manage Dotfiles w/ Chezmoi](https://jerrynsh.com/how-to-manage-dotfiles-with-chezmoi/)
- [Chris Titus - Easily Moving Linux Installs](https://www.youtube.com/watch?v=x6063EuxfEA)
- [Chris Titus Blog - Easily Moving Linux Installs](https://christitus.com/chezmoi/)
- [Jacob Bolda - chezmoi dotfile management](https://www.jacobbolda.com/chezmoi-dotfile-management/)

Dotfile Examples
- [GitHub Dotfiles](https://dotfiles.github.io/)
- [Andrew Burgess - Dotfiles! Here's how I organize them](https://www.youtube.com/results?search_query=dotfiles)
- [chris@machine dotfiles](https://github.com/ChristianChiarulli/Machfiles/tree/master)
- [edheltez - dotfiles](https://github.com/edheltzel/dotfiles)
- [dt dotfiles](https://gitlab.com/dwt1/dotfiles)
- [Mathias's dotfiles](https://github.com/mathiasbynens/dotfiles)
- [Awesome Dotfiles](https://github.com/webpro/awesome-dotfiles)
- [webpro dotfiles](https://github.com/webpro/dotfiles)
- [Jogendra - I Do Dotfiles](https://jogendra.dev/i-do-dotfiles)