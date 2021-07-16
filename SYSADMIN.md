# Devbox: Systems Administration, DevOps, and server-side Linux

This file contains a list of tools that you can use for systems administration (as well as DevOps and server-purpose Linux in general). If you're looking for tools and services that you can self-host, look at `SELFHOSTED.md`.

This file contains both a list of tools that you can use on your server, along with custom scripts and operating system recommendations.

## Operating Systems for Systems Administration

- [Ubuntu](https://www.ubuntu.com/) - A popular Debian-based operating system. The best Linux distribution for sysadmins who are just starting out or are familiar with Debian-based distributions.
  
- [Red Hat Enterprise Linux](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux) - A Linux distribution developed by Red Hat, the company that also sponsors the [Fedora](https://fedoraproject.org) project. RHEL is used in core infrastructures of many high-profile companies, and is specifically developed and optimised for production environments.
  
- [Rocky Linux](https://rockylinux.org) - A free-as-in-freedom Linux distribution based on Red Hat Enterpise Linux.
  
## Tools for project management and CI/CD
- [GitLab](https://about.gitlab.com/) - An open source code collaboration, project management, and CI/CD tool utilising Git. Available as SaaS and as a self-hosted solution.
- [Gitea](https://gitea.io) - A lightweight self-hosted Git service, similar to the likes of GitHub and GitLab.
- [Jenkins](https://jenkins.io/) - A CI/CD tool for automating build analysis and creating artifacts for deployments.

## An introduction to virtualisation and containerisation
*Why do you need containers and virtual machines, you might ask?* Virtualisation and containerising environments may just sound unnecessary. However, there are many benefits to containerising/virtualising your deployments into separate environments.

### What are the benefits of deployment isolation?

- **Isolation and Security** - By using containers/VMs, you are able to isolate one project from the rest of your system. That way, if a project goes rogue, you won't need to worry about the rest of the system being affected since the project won't have access to data from other deployments, nor will it have access to any other data on your server.

- **Resource allocation** - With containers or VMs, you are able to allocate resources to each project. For example, you may want to allocate a specific amount of RAM to your web server, while leaving the remaining resources for the rest of your deployments and the server in general.
  
- **Cloning and templates** - With a containerised or virtualised configuration, you are able to easily set up templates. This way, you're able to easily create multiple containers using the same software and container OS configuration with ease.

### How do I isolate my deployments?
There are many ways to isolate your deployments. However, I will be covering two of the most popular methods of isolation, both of which have already been mentioned above; containerisation and virtualisation.

- **Virtualisation** - Essentially, you could think about virtualisation as if you were placing a whole computer inside another computer--except this computer is completely virtual, emulated.
  
  With virtualisation, you can create an entirely new *virtual* computer using your own *existing* hardware using emulation. Everything is separated from the software perspective--meaning that you could run an entirely different operating system on this VM, or even replicate an entirely different CPU architecture.

  There are a few limitations to virtualisation, however. The first limitation is the slight performance overhead. Virtualisation is *slightly* slower than running on bare-metal, however it depends on what you're doing and what tool you're using to virtualise. The second limitation is that you are still confined to the limits of your own physical hardware. In simpler terms, you can't give your VM more RAM, CPU, or storage than the physical system actually has.

- **Containerisation** - While containerisation is similar to virtualisation, the difference is with the implementation and limitations. While virtualisation emulates an entire *computer* using technologies found in the CPU itself, containerisation only uses the abilities of the operating system kernel in order to isolate a container from the rest of the system. 
  
    While this may sound like a con, it's actually a benefit due to how the container uses a securely isolated version of the same kernel as the host system, whilst still being able to run a different OS and configuration (as long as it can run under the same kernel) in an OS image. This lowers the cost of upkeep since it means that you won't have to spend time maintaining an entirely different kernel from the main system. 
    
    Depending on the container solution that you use, the container may also update the operating system image automatically. Even if it doesn't, it is still extremely easy to update the container's OS image.

## Tools for virtualisation and containerisation

### Virtualisation tools

- [KVM](https://www.linux-kvm.org/) - A type-1 hypervisor that runs within the Linux kernel. KVM virtual machines are commonly used to achieve near-native speeds without most of the performance overhead that is given with a type-2 hypervisor that runs above the kernel. 
  
  **Do note that KVM cannot be run on its' own. It simply provides an API that must be managed by separate programs in the Linux userspace. KVM is commonly used with QEMU (see below)**.
  
- [Xen](https://xenproject.org/) - A type-1 hypervisor similar to KVM, however Xen is developed outside of the Linux kernel project; this is in contrast to KVM, which is developed alongside the Linux kernel. 

- [QEMU](https://www.qemu.org/) - A cross-platform type-2 hypervisor that runs above the Linux, Mac, or Windows kernel. It can be also used with the type-1 KVM or Xen hypervisor to achieve near-bare-metal performance.

- [VMWare ESXi](https://www.vmware.com/products/esxi/) - A type-1 hypervisor shipped in the standalone operating system. Unlike other virtualisation tools in this list, ESXi is a commercial product and is not open-source.

### Containerisation tools

- [Docker](https://www.docker.com/) - A free and open-source container platform powered by [containerd](https://containerd.io). Docker has a massive community of developers and users backing the project, and has a massive [OCI](https://opencontainers.org/) container image registry called Docker Hub. It is by far the most popular container solution.

- [Podman](https://podman.io) - Another free and open-source container platform that is very similar to Docker, sponsored by Red Hat. The major difference between Podman and Docker is that Docker uses a daemon-client model, whilst Podman does not have a daemon and the client directly interacts with Podman. Podman supports OCI images and has Docker Hub as a registry enabled by default, along with [Quay](https://quay.io), a separate container registry run by Red Hat.

- [LXC](https://linuxcontainers.org/) - A widely-known backend API for using and managing the Linux kernel's container isolation features. It is sponsored by Canonical, the developers of Ubuntu, and was Docker's default container API for a long time.