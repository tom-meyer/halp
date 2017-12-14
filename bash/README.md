### Directory name of script

    SCRIPT_DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"

### History search

(technically this is a readline thing) In `~/.inputrc`, put:

    "\e[A": history-search-backward
    "\e[B": history-search-forward

### Good prompt

    export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\W\[\033[m\]\$ "
