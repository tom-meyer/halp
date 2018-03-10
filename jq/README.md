### Using select()

    # get Tom's size
    jq '.people[] | select(.name == "Tom").size' <<< '{"people": [{"name":"Tom","size":"large"},
                                                                  {"name":"Tim","size":"tiny"}]}'

### Use filters

    jq '[.things[].size | select(. != "unknown") | tonumber ] | max' <<< '{"things":[{"size": "1"},
                                                                                     {"size": "9"},
                                                                                     {"size": "unknown"},
                                                                                     {"size": "5"}]}'
