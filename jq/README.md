### String interpolation

    jq -r '.[] | "Hello, \(.name)"' <<<'[{"name":"Tom"}]'

### Using select()

    # get Tom's size
    jq '.people[] | select(.name == "Tom").size' <<< '{"people": [{"name":"Tom","size":"large"},
                                                                  {"name":"Tim","size":"tiny"}]}'

### Use filters

    jq '[.things[].size | select(. != "unknown") | tonumber ] | max' <<< '{"things":[{"size": "1"},
                                                                                     {"size": "9"},
                                                                                     {"size": "unknown"},
                                                                                     {"size": "5"}]}'
### Use match()

    jq '.[] | select(.RoleName | match("Jupyter"))' <<< '[{"RoleName": "JupyterDev"}, {"RoleName":"EC2Role"}]'

### Sorting

    jq sort <<< '[2,3,1]'
    jq '[.[] | .id] | sort' <<< '[{"id":3}, {"id":1}, {"id":2}]'
    jq 'sort_by(.foo)' <<< '[{"foo":4, "bar":10}, {"foo":3, "bar":100}, {"foo":2, "bar":1}]'
