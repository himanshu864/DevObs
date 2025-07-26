#devops 

This repository contains my personal macOS configuration, covering setups for zsh (with Starship), Neovim, tmux, VSCode, and other essential tools. It’s designed to streamline the process of setting up a new system.

---
## Prerequisites

Before proceeding, ensure you have the following installed:

**macOS**  
(Tested on recent versions)

**Xcode Command Line Tools**  
Install them with:
```bash
xcode-select --install
```

**Git**  
(Available via Xcode or Homebrew)

**Homebrew**  
Install Homebrew by visiting [brew.sh](https://brew.sh/) or run:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---
## Installation Steps

### 1. Clone the Repository

Clone the repository into your home directory and navigate to it:

```bash
git clone https://github.com/yourusername/dotfiles.git ~/dotfiles
cd ~/dotfiles
```

### 2. Create Symbolic Links

Link your configuration files from the repository to your home directory. For example:

```bash
ln -sv ~/dotfiles/.zshrc ~/
ln -sv ~/dotfiles/.zprofile ~/
ln -sv ~/dotfiles/.tmux.conf ~/
ln -sv ~/dotfiles/.vimrc ~/
ln -sv ~/dotfiles/.gitconfig ~/
ln -sv ~/dotfiles/.obsidian.vimrc ~/
ln -sv ~/dotfiles/.vscode ~/
ln -sv ~/dotfiles/.config ~/
```

Alternatively, you can use [GNU Stow](https://www.gnu.org/software/stow/) for simplified management:

```bash
brew install stow
stow -t ~ .
```

### 3. Install Homebrew Packages & Applications

Run the Brewfile to install all necessary packages and applications:

```bash
brew bundle --file=Brewfile
```

### 4. Install the Starship Prompt

If Starship isn’t already installed via your Brewfile, install it with:

```bash
brew install starship
```

### 5. Reload Your Shell

To apply the changes, either restart your terminal or execute:

```bash
exec zsh
```

---

## Configuration Details

**zsh & Starship**  
Your `.zshrc` file initializes Starship with:

```bash
eval "$(starship init zsh)"
```

It also sets up syntax highlighting. Note: Although the file defines `ZSH_CUSTOM`, oh‑my‑zsh is not actively loaded. If you’re not using oh‑my‑zsh, you can remove it with:

```bash
rm -rf ~/.oh-my-zsh
```

**Neovim**  
Neovim configuration files are located in the `.config/nvim` directory.

**tmux**  
Custom settings are specified in `.tmux.conf`.

**Git**  
Global Git configurations are managed in `.gitconfig`.

**VSCode**  
Custom keybindings and settings reside in the `.vscode` folder.

**Additional Utilities & Applications**  
The Brewfile installs various command-line utilities (such as `btop`, `htop`, `ranger`, and `neofetch`) along with applications like iTerm2 and Obsidian.

---
## Additional Notes

- **Machine-Specific Configurations:**  
    Review each file for any settings that may be specific to your machine (such as file paths or credentials) and adjust them accordingly.
- **Keep Updated:**  
    Regularly update this repository with any changes to your configuration. This makes it easier to bootstrap future setups.

---

## Troubleshooting

- **Starship Initialization Issues:**  
    Ensure that Starship is installed and that you have reloaded your shell after making changes.
- **Symlink Conflicts:**  
    Check that there are no existing files in your home directory that could conflict with the new symbolic links before creating them.

---

Enjoy your efficient, version-controlled macOS setup!