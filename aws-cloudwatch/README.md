## Filter syntax

Syntax reference:

> https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/FilterAndPatternSyntax.html


    # single token
    aws logs tail ... --filter-pattern ERROR --follow

    # single string
    aws logs tail ... --filter-pattern '"authentication failed"'

    # implicit AND between search terms
    aws logs tail ... --filter-pattern "error Exception"

    # prefix with ? to make it an OR
    aws logs tail ... --filter-pattern "?ERROR ?WARN ?FATAL"

    # prefix with - to make it exclude
    aws logs tail ... --filter-pattern 'execute_query -SELECT'

    # use %...% for rexex
    aws logs tail ... --filter-pattern '%(ERROR|WARN|FATAL)%'

    # use %...%i for case insenstive rexex
    aws logs tail ... --filter-pattern '%(error|warn|fatal)%i'

    # json
    aws logs tail ... --filter-pattern '{ $.status = 500 }'
