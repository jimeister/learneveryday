# `exec` processes

Using `exec` runs executable in context of existing process, replacing the current executable and preserving PID. This contrasts with just running an executable in `bash` for example, which forks a process.

Example using `exec`:
```
$ ps
  PID TTY           TIME CMD
90275 ttys000    0:00.13 -bash
$ exec sleep 5m

# In new bash window
$ ps
  PID TTY           TIME CMD
90275 ttys000    0:00.13 sleep 5m  # existing bash window process now running sleep
90399 ttys001    0:00.13 -bash     # new bash window process
```
Running Ctrl-C on the first `bash` window exits the entire terminal.

Example without `exec`:
```
$ ps
  PID TTY           TIME CMD
90399 ttys001    0:00.13 -bash
$ sleep 5m

$ ps
  PID TTY           TIME CMD
90484 ttys000    0:00.13 -bash     # new bash window process
90399 ttys001    0:00.13 -bash     # existing bash window process
90481 ttys001    0:00.00 sleep 5m  # new process for sleep
```
Running Ctrl-C on the first `bash` window preserves terminal.

[reference](https://en.wikipedia.org/wiki/Exec_(system_call))
