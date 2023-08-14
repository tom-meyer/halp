https://docs.python.org/3/library/argparse.html

### basic

    parser = argparse.ArgumentParser()
    parser.add_argument('-n', '--dryrun', action='store_true', default=False)
    parser.add_argument('--age')
    parser.add_argument('name')
    args = parser.parse_args()

### subparsers

    parser = argparse.ArgumentParser()
    cmds = parser.add_subparsers(dest='cmd')
    cmds.required = True

    subparser = cmds.add_parser('foo')
    subparser.set_defaults(Run=lambda _: run_foo_cmd())
    
    subparser = subcmds.add_parser('bar')
    subparser.set_defaults(Run=lambda _: run_bar_cmd())
    
    args = parser.parse_args()
    args.Run(args)

### nargs

    https://docs.python.org/3/library/argparse.html#nargs

    parser.add_argument('bar', nargs='?', default='d')
    parser.add_argument('bar', nargs='*')
    parser.add_argument('bar', nargs='+')
    parser.add_argument('files', nargs=2)  # 'files' will be a list, even with nargs=1
    parser.add_argument('files', nargs=argparse.REMAINDER)

### collect multiple values

To collect a list of values with the same argment name, e.g.:

    mycmd -n 1 -n 2 -n 55

Use `action='append'`

    parser.add_argument('-n', action='append')

Note that the value will be a list of one if a single flag is used, and `None` if no flags are used.
    
### nice help messages

    https://docs.python.org/3/library/argparse.html#argumentparser-objects

    parser = argparse.ArgumentParser(prog='xutil', description='a handy utility')
    parser.add_argument('number', metavar='N', help='the number to yada')
