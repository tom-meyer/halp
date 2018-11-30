### Looking around

    hg id # current HEAD
    hg log -G # with graph
    hg log -l5 # show only 5 entries
    hg log -pl1 # ~ git show ('-p' is for patch)
    hg log -pr 256ec4f4 # ~ git show 256ec4f4
    hg heads # show branch heads
    hg out # ~ git fetch && git log origin/master..
    hg in  # ~ git fetch && git log ..origin/master

### Fetching and updating

    hg pull # ~ git fetch (doesn't move head)
    hg update tip     # move HEAD to very latest commit
    hg update default # move HEAD to tip of the branch called default
    hg update @       # move HEAD to the special bookmark called @

### Repo/file operations

    hg commit -e # ~ git commit -v
    hg revert -C my/file.txt # ~ git checkout -- my/file.txt (without '-C' a backup file is created)
    hg rebase -s 103 -d tip # move a commit (rebase extension required. notable flags: --keep --collapse )
    
### Pushing

    hg push default # mostly ok, but a branch can have multiple heads...
    hg push -r 129:ec0a43a4 # be absolutely specific

### Indispensable extensions

* [Evolve](https://www.mercurial-scm.org/wiki/EvolveExtension)
* [Rebase](https://www.mercurial-scm.org/wiki/RebaseExtension)
* [Pager](https://www.mercurial-scm.org/wiki/PagerExtension)
* [Color](https://www.mercurial-scm.org/wiki/ColorExtension)
