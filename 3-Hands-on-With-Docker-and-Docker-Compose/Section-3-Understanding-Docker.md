# Understanding Docker
- Docker containers are not virtual machines

## Virtual Machines vs Docker Containers
- Both requires an infrastructure, can be a computer, a machine on a datacenter, etc.
- Both requires a host operating system
- VMs Requires hypervisor
    - Type 1: Hyperkit (OSX) / Hyper-V (Windows) / KVM (Linux) - interacts directly with the infrastructure
    - Type 2: VirtualBox / VMWare Workstation - guest OSes, software side
- Docker does not need a hypervisor, requires docker daemon

### Docker's Analogy
- Virtual machines are houses
- Docker containers are apartments
- Houses (VMs) are fully self contained
- Houses (VMs) might give you too much
- Apartments (Docker Containers) have shared infrastructure
- Apartments (Docker Containers) maximize your size needs

## VMs and Docker Containers in the Real World
- When to use VMs and docker containers?
    - Virtual Machines
        - On web hosting company - separating each customer
        - Testing entire systems - perform tests in an environment that matches the production server
        - Ubuntu in production - run specific distribution
    - Docker containers
        - Isolate a single process, not just for web apps
        - Package manager for applications

- VMs isolate systems
- Docker isolate applications

## Visualizing Docker's Architecture
- Docker daemon is a service that runs on the host operating system, and only on linux
- Exposes the REST API, a number of different tools can communicate to the API
- The most widespread tool is the docker cli, a CLI that let's you talk to the docker daemon directly
