
### Expand globs and variables

    Ctrl-x *

### Directory name of script

    script_dir="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"

### Portable shebang

MacOSX is weird, so use this that works everywhere:

    #!/usr/bin/env bash

### .bashrc & .bash_profile & .profile, oh my!

* Just stick to .bashrc
* Let distro manage .profile
* Beware: RVM adds a .bash_profile which overrides .profile

##### login shell (ssh or bash --login or sudo -i or GUI on a Mac)

Runs first of: .bash_profile, .bash_login, .profile (read: **only** the first one
is run). Generally one of those three will source .bashrc. 

##### non-login (GUI on Ubuntu)

Runs .bashrc

### Shell quoting a command

Use printf to shell quote:

    cmd_opts=( ... )
    long_command=$(printf ' %q' "${cmd_opts[@]}")
    docker run --rm alpine sh -c "$ssm_command"

Helpful to debug:

    $ printf '%s\n' foo baz\ bar '"derp"'
    foo
    baz bar
    "derp"

### Parameter expansion

http://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#Shell-Parameter-Expansion-1

##### unset or null

* ${parameter:-word} substitute if unset
* ${parameter:=word} assign if unset
* ${parameter:?err msg} print err msg if unset
* ${parameter:+word} substitute nothing if unset. handy for optional separator: "$p${r:+-}$r"

##### arrays

* ${!name[@]} keys of array
* ${#parameter} length of array
* ${name[@]} and ${name[*]} (see below)

##### strings

* ${parameter:offset:length} *Substring Expansion*. length is optional. offset can be
  negative (but a space before colon is required, eg ` -1` not `-1`)
* ${parameter/pattern/string} replace pattern
* ${parameter##prefix} delete prefix (use one `#` for non-greedy)
* ${parameter%%suffix} delete suffix (use one `%` for non-greedy)

##### black magic

* ${!word} indirect variable expansion
* ${parameter@operator} Q and E useful for quoting and escaping

### History expansion

Whole line expansion:

    $ ls /root/.ssh # say this is item 274 in the history
    $ sudo !!
    $ sudo !274

Word expansion:

    $ echo one two three four five six # say this is item 317 in the history
    $ echo !317:1 # == echo one
    $ echo !317:6 # == echo six
    $ echo !317:$ # == echo six
    $ echo !317:* # == echo one two three four five six
    $ echo !317:3-5 # == echo three four five

Word expansion, when token after ! is not a number, is a shorthand for previous:

    $ echo one two three four five six
    $ echo !* # == echo one two three four five six

    $ echo one two three four five six
    $ echo !^ # == echo one
    
    $ echo one two three four five six
    $ echo !$ # == echo six

### Array expansion: [@] vs [*]

`[@]` is almost aways the desired form. Details:

`${words[@]}` -> quote each item in the array

`${words[*]}` -> join all items with IFS and wrap in quotes

To see how this works, use `set -x` and noop (`:`) to see how the parameters were parsed:

    $ set -x
    $ a=("1 one" "2 two")
    $ : ${a[@]} :: "${a[*]}" :: "${a[@]}"
    + : 1 one 2 two :: '1 one 2 two' :: '1 one' '2 two'

### History search

(technically this is a readline thing) In `~/.inputrc`, put:

    "\e[A": history-search-backward
    "\e[B": history-search-forward

### Good prompt

    export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\W\[\033[m\]\$ "
