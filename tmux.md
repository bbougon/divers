Fichier tmux.conf

```bash
set -g default-terminal "xterm-256color"

#souris active pour la sélection des fenêtres
set-option -g mouse on
#bind-key -T copy-mode M-w send -X copy-pipe 'reattach-to-user-namespace pbcopy'

#On utlise control + flèches pour naviguer entre les terminaux
bind-key -n C-right next
bind-key -n C-left prev

#on utilise alt + flèches our naviguer entre les panels
bind-key -n M-left select-pane -L
bind-key -n M-right select-pane -R
bind-key -n M-up select-pane -U
bind-key -n M-down select-pane -D

#On met les panneaux non actif en gris
set -g pane-border-fg colour244
set -g pane-border-bg default
 
#On met le panneau actif en rouge
set -g pane-active-border-fg colour124
set -g pane-active-border-bg default
 
#On met la barre de status en gris
set -g status-fg colour235
set -g status-bg colour250
set -g status-attr dim
 
# On surligne les fenêtres actives dans la barre de status en gris foncés
set-window-option -g window-status-current-fg colour15
set-window-option -g window-status-current-bg colour0

# increase space on right status bar
set -g status-right-length 100

# remove everything on the right (just tmux-gitbar will show up)
set -g status-right ""

#Affichage de la branche git actuelle
source-file "$HOME/.tmux-gitbar/tmux-gitbar.tmux"

```

CheatSheet

start new with session name:

    tmux new -s myname

attach:

    tmux a  #  (or at, or attach)

attach to named:

    tmux a -t myname

list sessions:

    tmux ls

kill session:

    tmux kill-session -t myname

In tmux, hit the prefix `ctrl+b` and then:

## Sessions

    :new<CR>  new session
    s  list sessions
    $  name session

## Windows (tabs)

    c           new window
    ,           name window
    w           list windows
    f           find window
    &           kill window
    .           move window - prompted for a new number
    :movew<CR>  move window to the next unused number

## Panes (splits)

    %  horizontal split
    "  vertical split
    
    o  swap panes
    q  show pane numbers
    x  kill pane
    ⍽  space - toggle between layouts

## Window/pane surgery

    :joinp -s :2<CR>  move window 2 into a new pane in the current window
    :joinp -t :1<CR>  move the current pane into a new pane in window 1
