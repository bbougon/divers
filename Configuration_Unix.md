# Vim
 
 ```bash
  set mouse=a 
  set clipboard=unnamed 
  set number 
  syntax enable 
  set background=dark 
  let g:solarized_termcolors = 256
 ```

# Tmux
```bash
  set -g default-terminal "xterm-256color"
  
  #souris active pour la sélection des fenêtres
  set-option -g mouse on
  
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
```
