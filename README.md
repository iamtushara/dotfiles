# 🌿 Dotfiles for WSL (Ubuntu)

A curated collection of configuration files for shell environments like Bash and Zsh, managed using **[GNU Stow](https://www.gnu.org/software/stow/)** for easy installation and portability.

This document outlines the setup process for restoring the environment after a fresh **Ubuntu on WSL** install. Steps include Git configuration, Git Credential Manager usage, Stow installation, and symlink creation for configuration files.

---

## 📁 Repository Structure

```
dotfiles/
├── dotfiles/
│   ├── bash/
│   │   └── .bashrc
│   ├── zsh/
│   │   └── .zshrc
│   ├── aliases/
│   │   └── .aliases
│   ├── git/
│   │   └── .gitconfig
├── README.md
```

Each subdirectory inside `dotfiles/dotfiles/` represents a package of dotfiles. `stow` will create symlinks from files in these directories to the home directory (`~`).

---

## 🛠 Prerequisites

- Windows with **WSL** (Ubuntu)
- A GitHub account
- Git Credential Manager installed and configured
- GNU Stow installed in WSL

---

## 🚀 Fresh Setup Guide (Step-by-Step)

### 1. Clone the Repository

Git should be configured to use the Git Credential Manager:

```bash
git config --global credential.helper "/mnt/c/Program\ Files\ \(x86\)/Git\ Credential\ Manager/git-credential-manager.exe"
```

Clone the repository:
```bash
git clone https://github.com/iamtushara/dotfiles.git ~/Code/dotfiles
cd ~/Code/dotfiles
```

---

### 2. Install GNU Stow

Install Stow with:
```bash
sudo apt update
sudo apt install stow
```

---

### 3. Apply Dotfiles with Stow

Navigate to the stow packages directory:
```bash
cd ~/Code/dotfiles/dotfiles
```

Apply all packages to the home directory:
```bash
stow -t ~ *
```

---

### 4. Verify Symlinks

Check whether files like `~/.bashrc`, `~/.zshrc`, and `~/.aliases` exist as symlinks pointing to the repository files.

```bash
ls -l ~/.bashrc
```

Expected output:
```
lrwxrwxrwx 1 user user 55 May 23 13:00 .bashrc -> /home/user/Code/dotfiles/dotfiles/bash/.bashrc
```

---

## ♻️ Updating Dotfiles

To update configurations:
1. Edit files in `~/Code/dotfiles/dotfiles/<folder>/<file>`
2. Stage, commit, and push changes:

```bash
git add .
git commit -m "Update bashrc with alias tweaks"
git push origin main
```

---

## 🔄 Reverting / Removing Links

To undo symlinks:
```bash
cd ~/Code/dotfiles/dotfiles
stow -D -t ~ bash
stow -D -t ~ zsh
stow -D -t ~ aliases
```

---

## 🧠 Tips and Best Practices

- Subfolders inside `dotfiles/dotfiles/` should mimic the directory structure where the files will reside.
- Use `stow -nv -t ~ *` to preview changes.
- Backups of original dotfiles may be made before first use:
  ```bash
  cp ~/.bashrc ~/.bashrc.bak
  ```

---

## 🐧 For Multiple Environments

Additional folders can be added inside `dotfiles/dotfiles/` as needed:
- `git/` → `~/.gitconfig`
- `nvim/` → `~/.config/nvim`
- `tmux/` → `~/.tmux.conf`

Symlinks can then be created with:
```bash
cd ~/Code/dotfiles/dotfiles
stow -t ~ *
```

---

## 📦 Optional: Setup Script

A basic automation script can be used for setup:
```bash
#!/bin/bash
cd ~/Code/dotfiles/dotfiles || exit
stow -t ~ *
```

Make the script executable:
```bash
chmod +x setup.sh
```

Execute it:
```bash
./setup.sh
```

---
