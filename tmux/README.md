### .tmux.conf

    set-option -g prefix C-a
    set -g mouse on
    set-window-option -g window-status-current-bg red
    bind-key C-a last-window
    set-option -g allow-rename off

### Commands

    :rename-window NAME

### Copying text

Hold down `shift` while selecting with the mouse will bypass the mouse hijacking that
tmux does with `set -g mouse on`. Selected text is copied to system clipboard as expected.

Block selection is possible too with `shift-ctrl` while selecting with mouse.

Alternatively, just turn off mouse support with `set -g mouse off` to get normal selectable
terminal text.
