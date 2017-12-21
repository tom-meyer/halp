### Directory name of script

    SCRIPT_DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"

### Array expansion: [@] vs [*]

`[@]` is almost aways the desired form. Details:

`${words[@]}` -> quote each item in the array

`${words[*]}` -> join all items with IFS and wrap in quotes

To see how this works, use `ls`'s error output to see how the words were expanded:

    $ CMD=('foo bar' shazam)
    $ ls "${CMD[@]}"
    ls: cannot access foo bar: No such file or directory
    ls: cannot access shazam: No such file or directory
    $ ls "${CMD[*]}"
    ls: cannot access foo bar shazam: No such file or directory

### History search

(technically this is a readline thing) In `~/.inputrc`, put:

    "\e[A": history-search-backward
    "\e[B": history-search-forward

### Good prompt

    export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\W\[\033[m\]\$ "
