# Use of Seccomp Profiles to secure container workloads

The aim of this task is to build an understanding of seccomp, and to use seccomp to secure containers.

## Guidance

1. Prepare and read about seccomp so you get a feel for what seccomp is all about. You should then be able to talk about terms like syscalls, seccomp and seccomp profile.
2. Create an Exoscale Account and a VM (Linux Ubuntu 22.04 LTS 64-bit) and make sure you can SSH into it. **If you have already received an invitation by e-mail for Exoscale, you can of course use this account.**
3. Install docker on the vm.
4. Read the [Story](STORY.md)
5. Read [Story 2](STORY_2.md) and help your colleague.

## Additional task

* Maybe you can help Alice with her task.
* Maybe you can support Alice and Bob with their problem as well.
* Check out [tracee](https://github.com/aquasecurity/tracee) from aquasecurity to trace syscalls.
* Check out how you could use seccomp to secure a Kubernetes Cluster

## Notes

* Link to seccomp description: https://www.kernel.org/doc/html/v4.18/userspace-api/seccomp_filter.html
* List of syscalls: https://de.wikipedia.org/wiki/Liste_der_Linux-Systemaufrufe
* Kubernetes Seccomp Documentation: https://kubernetes.io/docs/tutorials/security/seccomp/