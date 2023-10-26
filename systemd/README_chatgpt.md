> (I ask about running a docker container as a service)

Using systemd to manage Docker containers involves some considerations when determining whether to run the container in the foreground or background. Here's a breakdown of the trade-offs for both approaches:

## Running Docker Container in the Foreground (`docker run -d=false`):

**Pros:**

1. **Direct Logging**: Output from the container goes directly to `journald`, the logging system of systemd. This means you can use `journalctl` to view the logs directly without needing to inspect the container.
2. **Immediate Feedback on Failure**: If the container fails to start, systemd will be immediately notified and can take the configured actions on failure.
3. **Simpler Configuration**: Only `ExecStart` is required.

**Cons:**

1. **Less Flexibility**: The container's lifecycle is directly tied to the lifecycle of the systemd service. This can be limiting in some scenarios, such as when you want to restart just the container without affecting the service.

## Running Docker Container in the Background (`docker run -d=true`):

**Pros:**

1. **Decoupling**: The container's lifecycle is somewhat decoupled from the systemd service. This provides flexibility, for example, when updating the image or manually restarting the container.
2. **Explicit Control**: By having both `ExecStart` and `ExecStop`, you have explicit control over the start and stop commands, providing more granularity in container management.

**Cons:**

1. **Logging Indirection**: Logs will go to Docker's logging system (e.g., json-file) by default. If you want the logs in `journald`, additional configuration or log drivers may be required.
2. **Complexity**: You have to manage both starting and stopping commands and ensure that the container is cleanly stopped. This may involve getting the container ID, storing it somewhere (e.g., in a file), and using that ID to stop the container later.

## Recommendations:

1. **For Simplicity**: If you want a straightforward setup and the lifecycle of the Docker container closely tied to the systemd service, run the container in the foreground.
2. **For Flexibility**: If you require more control, perhaps due to advanced deployment setups or unique requirements, running the container in the background might be a better choice.

Regardless of the approach you choose, ensure that your systemd service file specifies the correct dependencies (like `Requires=docker.service` and `After=docker.service`) and uses appropriate options (like `Restart=always`) to make the service resilient and behave as expected.

> If the command specified in ExecStart exits with code 0, does systemd assume the service has started?

Not necessarily. The behavior of systemd in response to an exit code from the `ExecStart` command is influenced by the `Type=` directive in the service file. Here's a summary of how systemd interprets the start status based on the `Type=` directive:

1. **Type=simple (default)**: With this setting, systemd considers the service started as soon as the `ExecStart` process is spawned. It doesn't wait for the process to exit. If the process spawned by `ExecStart` exits (regardless of the exit code), the service is considered failed unless `Restart=` is set to some policy like `always`, `on-success`, etc.

2. **Type=forking**: In this mode, the process started via `ExecStart` is expected to fork a child and then exit (with the parent process exiting successfully, typically with exit code 0). This is how traditional Unix daemons operate. systemd will consider the service started once the parent process exits. The child process continues running in the background. It's often necessary to use the `PIDFile=` directive with this type to tell systemd where to find the PID of the forked process.

3. **Type=oneshot**: With this setting, systemd considers the service started only after the `ExecStart` process exits. This is useful for commands that perform a single task, exit, and then the service remains "active" until some other condition stops it.

4. **Type=dbus**: This is for services where activation is tied to a D-Bus signal. The service is considered started when the specified D-Bus signal is emitted.

5. **Type=notify**: In this mode, the service is considered started only after it sends a notification (usually via `sd_notify`). This allows more complex startup sequences where a program might need to perform multiple steps before it's "ready", even though the main process has already started.

6. **Type=idle**: This is similar to `simple`, but actual execution of the service binary is delayed until all jobs are dispatched.

So, while an exit code of 0 typically indicates success in Unix systems, it's the combination of `Type=`, the behavior of the `ExecStart` command, and potentially other directives like `PIDFile=` that inform systemd about the actual status and lifecycle of the service.
