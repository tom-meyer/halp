### Basic .screenrc

    hardstatus on
    hardstatus alwayslastline
    hardstatus string "%{.bW}%-w%{.mW}%n %t%{-}%+w %=%{..G} %H %{..Y}[%Y-%m-%d]   %c "
    term screen-256color

### Stop auto-changing title

    unset PROMPT_COMMAND
    
Supposidly, `defdynamictitle off` in .screenrc will disable it entirely. Have not
confirmed yet. Spotted on https://unix.stackexchange.com/a/587774
