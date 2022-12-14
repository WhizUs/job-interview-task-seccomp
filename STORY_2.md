# WhizCash Bank - Request from a Bob

Bob comes to Alice and asks for her support. His goal is to protect a file from read access. After a research in the internet he found 2 binaries on the internet with which he tries to read the file.

## What your colleague tried

Bob's idea was to secure the file by using seccomp and preventing the read syscall. Bob has prepared a Docker image that he gives Alice to test. He shows Alice the following on his computer:

1. First he creates a container

       sudo docker run --name nsjail --rm -it whizus/nsjail-seccomp /bin/bash
    
2. Then he creates a test secret

       echo "Very secret!" > /tmp/secret

3. He runs the first binary (a go programm that reads the /tmp/secret)

       nsjail --disable_clone_newcgroup --disable_clone_newuser --disable_clone_newns --disable_clone_newuts --disable_clone_newipc --disable_clone_newpid --disable_clone_newnet -Mo --chroot / --seccomp_string 'POLICY a { DENY { read } } USE a DEFAULT ALLOW' -- /main

4. Afterwards he tries the second binary
    
       nsjail --disable_clone_newcgroup --disable_clone_newuser --disable_clone_newns --disable_clone_newuts --disable_clone_newipc --disable_clone_newpid --disable_clone_newnet -Mo --chroot / --seccomp_string 'POLICY a { DENY { read } } USE a DEFAULT ALLOW' -- /bypass

Bob is wondering: Even though both binaries are started with the same seccomp restriction to read the file it seems to be not the case for the second executable which somehow bypasses it.

# Alice want to help

Alice is a team player and would like to help Bob with his problem. She would like to take a closer look at why the second executable can read the file, even though both binaries are started with the same seccomp restriction to read the file.