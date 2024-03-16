# Config file

`~/.config/fish/config.fish`

```fish
# Aliases
# DNF
alias cu='sudo dnf check-update'
alias dnfi='sudo dnf install'
alias dnfe='sudo dnf erase'
alias dnfu='sudo dnf update'
alias dnfhl='sudo dnf history list | head -n 15'
alias dnfhu='sudo dnf history undo'
alias dnfs='dnf search'

# Basic tools
alias l='eza --group-directories-first --no-quotes'
alias ls='eza --group-directories-first --no-quotes'
alias sl='eza --group-directories-first --no-quotes'
alias la='eza --group-directories-first -a --no-quotes'
alias ll='eza --group-directories-first -l -g --no-quotes --icons'
alias cat='bat'

# Dev
alias py3='python3'
alias ipy='ipython3'
alias py3Profile='py3 -m cProfile -s time'
alias diffstat='diffstat -C'
alias pip3update='pip3 list --outdated --user --format json | jq ".[].name" | sd \'"\' \'\' | string join " "'

# Env
set -x DOCKER_HOST unix:///run/user/(id -u)/podman/podman.sock
set -x EXA_COLORS "tm=2:mu=35:lo=35:*.dll=0:do=94:sc=0:*.lock=2"

# Other
set EDITOR hx
set PATH $PATH /home/user/bin
set PATH $PATH /home/user/.cargo/bin
set PATH $PATH /home/user/.local/bin

bind \es 'echo ""; git s; commandline -f repaint;'
bind \ed 'echo ""; git d; commandline -f repaint;'
bind \ec 'echo ""; git dc; commandline -f repaint;'
```

# Icons for eza

Download [Nerd Fonts](https://www.nerdfonts.com/font-downloads) for DejaVu Sans Mono, unzip into `~/.fonts`.
