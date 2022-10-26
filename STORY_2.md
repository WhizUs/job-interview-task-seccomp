# WhizCash Bank - Request from a colleague

A colleague comes to you and asks for your support. His goal is to protect a file from read access. He has found 2 binaries on the internet with which he tries to read the file.

## What your colleague tried

The colleague has prepared a Docker image that he gives you to test. He shows you the following on his computer:

1. First he creates a container

       sudo docker run --name nsjail --rm -it whizus/nsjail-seccomp /bin/bash
    
2. Then he creates a test secret

       echo "Very secret!" > /tmp/secret

3. He runs the first binary (a go programm that reads the /tmp/secret)

       nsjail --disable_clone_newcgroup --disable_clone_newuser --disable_clone_newns --disable_clone_newuts --disable_clone_newipc --disable_clone_newpid --disable_clone_newnet -Mo --chroot / --seccomp_string 'POLICY a { DENY { read } } USE a DEFAULT ALLOW' -- /main

4. Afterwards he tries the second binary
    
       nsjail --disable_clone_newcgroup --disable_clone_newuser --disable_clone_newns --disable_clone_newuts --disable_clone_newipc --disable_clone_newpid --disable_clone_newnet -Mo --chroot / --seccomp_string 'POLICY a { DENY { read } } USE a DEFAULT ALLOW' -- /bypass

5. Your colleague is at a loss and asks you for help and asks you if you know what happened.