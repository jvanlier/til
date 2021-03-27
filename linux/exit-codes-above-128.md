Exit Codes Above 128
================
Exit codes 128 have a special meaning in Linux: exit codes `128 + n` are used for termination due to signal `n`. A common sight is processes dying with exit code 137, or 128 + 9. Signal 9 is SIGKILL.

This happens, for instance:

- With HashiCorp's Nomad when processses exceed the memory allocated to them: they get killed with code 137 (Linux cgroup limit, `dmesg` shows this nicely). 
- Processes running on the JVM that need more memory than reserved in the virtual machine (tune Xmx).
- On Hadoop when YARN decides to kill a process when it starts using more memory than "promised" in its resource request (this might simply be due to the previous bullet).

Likewise, processes terminated by CTRL-C get exit code 130, because CTRL-C sends a SIGINT, signal number 2.

