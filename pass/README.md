### Basic commands

    pass ls
    pass edit some/website
    pass -c some/website  # copy to clipboard


### Post install steps

    gpg --full-generate-key  # follow the interactive prompts, defaults are fine
    gpg --list-secret-keys --keyid-format LONG  # show the key just created
    pass init <email used when generating key>
    pass git init
