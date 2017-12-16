### Notes on options

    -ain # archive, itemize, dry-run

Archive mode: `--a` is same as `-rlptgoD`. Break that down:

        -r, --recursive             recurse into directories
        -l, --links                 copy symlinks as symlinks
        -p, --perms                 preserve permissions
        -o, --owner                 preserve owner (super-user only)
        -g, --group                 preserve group
        -t, --times                 preserve modification times
