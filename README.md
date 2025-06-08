# **Tmux** (Terminal Multiplexer)
   [tmux](https://github.com/tmux/tmux/wiki) is a terminal multiplexer.</br>
   It makes switching between several programs in one terminal easily, detach and reattach them to a different terminal.</br>
   Tmux is useful for splitting Terminal window because some terminal emulator such [_Alacritty_](https://alacritty.org) doesn't support splliting window or tab-like by default.</br></br>
   Install by running by following the steps [here](https://github.com/tmux/tmux/wiki/Installing)</br>

After succesfully installed Tmux. Create a `.tmux-conf` file in your home directory if you haven't already, and add this custom tmux setup:
```
# --- GENERAL SETTINGS ---
set -g mouse on                                         # Enable mouse support
set -g history-limit 10000                              # Scrollback history
set -g base-index 1                                     # Start windows at 1
setw -g pane-base-index 1                               # Start panes at 1
set-option -g detach-on-destroy off                     # Don't exit if a session is destroyed
set-option -g renumber-windows on                       # Auto-renumber windows
set-option -ga terminal-overrides ",xterm-256color:Tc"  # Enable 24-bit colors

# --- KEY BINDINGS ---
unbind C-b                               # Unbind default prefix
set -g prefix C-a                        # Use Ctrl-a as the new prefix
bind C-a send-prefix                     # Allow sending Ctrl-a to programs

bind r source-file ~/.tmux.conf \; display "Config reloaded!"  # Reload config

# --- PANE NAVIGATION ---
# Use Ctrl+a and Vim-like keys for pane navigation
bind -r h select-pane -L
bind -r j select-pane -D
bind -r k select-pane -U
bind -r l select-pane -R

# Resize panes
# Use Ctrl+a and < or > or + or - 
bind -r < resize-pane -L 5
bind -r > resize-pane -R 5
bind -r + resize-pane -U 5
bind -r - resize-pane -D 5

# --- CLIPBOARD (macOS) ---
# Requires 'reattach-to-user-namespace' for tmux < 3.2
# If using tmux ≥ 3.2 on macOS, built-in pbcopy support is available:
bind-key -T copy-mode-vi 'y' send -X copy-pipe-and-cancel "pbcopy"

# --- STATUS BAR ---
set -g status-interval 5
set -g status-justify centre
set -g status-left-length 60
set -g status-right-length 120
set -g status-left '#[fg=black]#S #[default]'
set -g status-right '#[fg=black]%Y-%m-%d #[fg=black]%H:%M #[default]'
set -g status-bg '#cdd6f4'
set -g status-fg white

# --- COLORS & THEME ---
set -g default-terminal "screen-256color"
set -ga terminal-overrides ",xterm-256color:Tc"

# Use Vim keys in copy mode
setw -g mode-keys vi

# --- VI MODE SELECTION ENHANCEMENTS ---
# Make 'v' start characterwise selection (like vim visual mode)
bind -T copy-mode-vi v send -X begin-selection

```
