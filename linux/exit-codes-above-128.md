Exit Codes Above 128
================
Exit codes 128 have a special meaning in Linux: exit codes `128 + n` are used for kills due to signal `n`. O common sight is processes dying with exit code 137, or 128 + 9. Signal 9 is SIGKILL.

This happens, for instance, with HashiCorp's Nomad when processses exceed the memory allocated to them: they get killed with code 137 (Linux cgroup limit, `dmesg` shows this nicely). It can also happen on Hadoop when YARN decides to kill a process when it starts using more memory than "promised" in its resource request.

Likewise, processes terminated by CTRL-C get exit code 130, because CTRL-C sends a SIGINT, signal number 2.

