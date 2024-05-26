### How to use  `ps` commands

`ps` stands for "process status." This command is used to display information about processes running on your system.

**Flags:**

`a` - This flag tells ps to list all processes, regardless of who owns them or their terminal status.

`x` - This flag tells ps to include processes that are not connected to a terminal. These are typically background processes.

`u` - This flag tells ps to display the output in a user-oriented format. This format provides more detailed information about each process, including:

`USER`: The username of the process owner

`PID`: The process ID (unique identifier)

`%CPU`: The percentage of CPU time the process is using

`%MEM`: The percentage of memory the process is using

`VSZ`: The virtual memory size of the process (total memory it can potentially use)

`RSS`: The resident set size of the process (amount of physical memory currently in use)

`STAT`: The current state of the process (e.g., running, sleeping, waiting)

`START`: The time the process was started

`TIME`: The total CPU time the process has used

`COMMAND`: The name of the command that started the process

**Example:**

###### Example of `kill` a process

```bash
ps axuw | grep dockerd | grep  -v grep | awk '{print $2}' | xargs kill -9