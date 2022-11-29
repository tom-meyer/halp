### Basic .screenrc

    hardstatus on
    hardstatus alwayslastline
    hardstatus string "%{.bW}%-w%{.mW}%n %t%{-}%+w %=%{..G} %H %{..Y}[%Y-%m-%d]   %c "
    term screen-256color

### Stop auto-changing title

    unset PROMPT_COMMAND
