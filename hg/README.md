### Looking around

    hg id # current HEAD
    hg log -G # with graph
    hg log -l5 # show only 5 entries
    hg log -pl1 # ~ git show ('-p' is for patch)
    hg log -pr 256ec4f4 # ~ git show 256ec4f4
    hg heads # show branch heads

### Fetching and updating

    hg pull # ~ git fetch (doesn't move head)
    hg update tip     # move HEAD to very latest commit
    hg update default # move HEAD to tip of the branch called default
    hg update @       # move HEAD to the special bookmark called @

### Repo/file operations

    hg revert -C my/file.txt # ~ git checkout -- my/file.txt (without '-C' a backup file is created) 
