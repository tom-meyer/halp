### Directory name of script

    SCRIPT_DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"

### History search

(technically this is a readline thing) In `~/.inputrc`, put:

    "\e[A": history-search-backward
    "\e[B": history-search-forward
