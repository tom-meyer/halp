### Clone with key

    git clone -c 'core.sshcommand = ssh -i ~/dots/ssh/id_rsa_github -o IdentitiesOnly=yes' git@github.com:tom-meyer/halp.git

### Basic config (~/.gitconfig)

    [color]
      diff = auto
      status = auto
    [user]
      name = Tom Meyer
      email = ____
    [alias]
      st = status
      ci = commit
      co = checkout
      lol = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --exclude=refs/stash --all
      show-plain = show --name-only --pretty=
      diff-plain = diff --name-only
    [push]
      default = simple

### Diff: ^ vs .. vs ...

TODO

### Log: ^ vs .. vs ...

TODO
