### Rsync with sudo and specific identity file

    rsync --rsync-path='sudo rsync' -e 'ssh -i key.pem' -r ec2-user@somehost:/etc/ ./backup/etc/

### Notes on options

    -ain # archive, itemize, dry-run

Archive mode: `--a` is same as `-rlptgoD`. Break that down:

    -r, --recursive             recurse into directories
    -l, --links                 copy symlinks as symlinks
    -p, --perms                 preserve permissions
    -o, --owner                 preserve owner (super-user only)
    -g, --group                 preserve group
    -t, --times                 preserve modification times

### The trailing slash

* Mostly just use slashes on both when sync'ing directories
* A slash indicates to rsync that the entity is a directory and will do the appropriate thing
* A slash on the dest doesn't matter except when the source is a file and the dest dir doesn't exist

No slashes (existence of dest dir doesn't matter for all 4 of these cases) 

    rsync -r testing test_backup # result: ./test_backup/testing/ (test/ is copied as if it were a file)

Slash on both

    rsync -r testing/ test_backup/ # result: .test_backup/ (contents of test/ end up in test_backup/)

Slash on the source

    rsync -r testing/ test_backup # result: .test_backup/ (same as with slashes on both)

Slash on the destination

    rsync -r testing test_backup/ # result: ./test_backup/testing/ (same as with no slashes)

See http://qdosmsq.dunbar-it.co.uk/blog/2013/02/rsync-to-slash-or-not-to-slash/

### Identity file

    rsync -r -e "ssh -i key.pem" user@somehost:mydir/ mydir/
