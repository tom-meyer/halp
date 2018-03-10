### Using select()

    # get Tom's size
    jq '.people[] | select(.name == "Tom").size' <<< '{"people": [{"name":"Tom","size":"large"},
                                                                  {"name":"Tim","size":"tiny"}]}'
