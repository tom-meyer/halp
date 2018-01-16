### Use rabbitmqctl

    rabbitmqctl list_connections pid port state user vhost recv_cnt

### Get the rabbitmqadmin script

    curl http://localhost:15672/cli/rabbitmqadmin > rabbitmqadmin
    # If above fails, might need to enable management functionality:
    rabbitmq-plugins enable rabbitmq_management

### Use rabbitmqadmin

    rabbitmqadmin get queue=test requeue=false # create a queue
    
More examples: https://www.rabbitmq.com/management-cli.html
