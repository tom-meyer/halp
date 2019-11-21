### Group membership

The inventory (e.g. host.cfg) seems to be the only way to specify group membership.

For example, place localhost in two groups:

    [nginx]
    localhost
    
    [flask]
    localhost

Don't forget that every host is a member of the "all" group.

### Inventory

Usually inventory is specied in hosts.cfg, but can also be a script.

Multiple inventories can be specified on the command line with multiple `-i` flags.

Individual hosts or groups can be specided as the inventory by using the `-i` flag... use commas
to diferentiate. Example:

    ansible-playbook -i host.cfg # read inventory from a file
    ansible-playbook -i localhost, # inventory is localhost because of the comma (I just threw up a little in my mouth)

### Where vars can be specified

Here be dragons. Whole lota "magic" directories and conventions, don't get burned...

Ansible slurps up vars from files all over the place. Below are some notable places:

* command line with --extra-vars
* yaml files relative to host.cfg: group_vars, host_vars, etc
* yaml files relative to cwd: group_vars, host_vars, etc
* yaml files within the role file hierarchy
* embedded in playbook with `vars_files` keyword
* embedded in host.cfg (or other kinds of inventory)

Relevant ansible docs:

> https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#ansible-variable-precedence

### Organization of group_vars

For small things, a single file is fine:

    ./group_vars/web.yaml

But a large config can be broken up by living in a directory:

    ./group_vars/web/ec2.yaml
    ./group_vars/web/dns.yaml
    ./group_vars/web/nginx.yaml

### ansible vs ansible-playbook

`ansible` is for ad hoc invocations of a single task. E.g.

    ansible localhost -m debug -a 'msg={{vars}}'
    
`ansible-playbook` is for invoking a whole set of tasks or roles
