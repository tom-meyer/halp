### SGR sequences

    echo -e "\033[31mRed\033[0m"        # bash
    print("\033[32mGreen\033[0m")       # python
    console.log("\033[34mBlue\033[0m")  # javascript

Common parameters:

    0 # reset
    1 # bold
    31 # red
    32 # green
    34 # blue

Combining parameters:

    echo -e "\033[31;46;1;4mWowzers\033[0m" # red fg (31), cyan bg (46), bold (1), underline (4)

Reference:
- https://stackoverflow.com/questions/4842424/list-of-ansi-color-escape-sequences
- https://en.wikipedia.org/wiki/ANSI_escape_code#SGR_(Select_Graphic_Rendition)_parameters
- https://en.wikipedia.org/wiki/ANSI_escape_code#Colors
