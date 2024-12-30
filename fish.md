# Config file

`~/.config/fish/config.fish`

```fish
# Aliases
# DNF
alias cu='sudo dnf check-update'
alias dnfi='sudo dnf install'
alias dnfe='sudo dnf remove'
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
set -x PYTHONBREAKPOINT "pudb.set_trace"

# Other
set EDITOR hx
set PATH $PATH /home/user/bin
set PATH $PATH /home/user/.cargo/bin
set PATH $PATH /home/user/.local/bin

bind \es 'echo ""; git s; commandline -f repaint;'
bind \ed 'echo ""; git d; commandline -f repaint;'
bind \ec 'echo ""; git dc; commandline -f repaint;'
```

# Prompt

`~/.config/fish/functions/fish_prompt.fish`

This is the default prompt with added time.

```fish
function fish_prompt --description 'Write out the prompt'
    set -l last_pipestatus $pipestatus
    set -lx __fish_last_status $status # Export for __fish_print_pipestatus.
    set -l normal (set_color normal)
    set -q fish_color_status
    or set -g fish_color_status red

    # Color the prompt differently when we're root
    set -l color_cwd $fish_color_cwd
    set -l suffix '>'
    if functions -q fish_is_root_user; and fish_is_root_user
        if set -q fish_color_cwd_root
            set color_cwd $fish_color_cwd_root
        end
        set suffix '#'
    end

    # Write pipestatus
    # If the status was carried over (if no command is issued or if `set` leaves the status untouched), don't bold it.
    set -l bold_flag --bold
    set -q __fish_prompt_status_generation; or set -g __fish_prompt_status_generation $status_generation
    if test $__fish_prompt_status_generation = $status_generation
        set bold_flag
    end
    set __fish_prompt_status_generation $status_generation
    set -l status_color (set_color $fish_color_status)
    set -l statusb_color (set_color $bold_flag $fish_color_status)
    set -l prompt_status (__fish_print_pipestatus "[" "]" "|" "$status_color" "$statusb_color" $last_pipestatus)

    echo -n -s (set_color 666666) '['(date "+%H:%M:%S") '] '$normal(prompt_login)' ' (set_color $color_cwd) (prompt_pwd) $normal (fish_vcs_prompt) $normal " "$prompt_status $suffix " "
end
```

# Icons for eza

Download [Nerd Fonts](https://www.nerdfonts.com/font-downloads) for DejaVu Sans Mono, unzip into `~/.fonts`.
