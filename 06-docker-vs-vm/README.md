# 06 — Docker vs Virtual Machines 🐳

## 1. What Is a Virtual Machine (VM)?

A Virtual Machine is a software-based computer that runs its own guest operating system on virtualized hardware using a hypervisor.

**Example:** Running Ubuntu inside VirtualBox on a Windows laptop.

## 2. What Is a Docker Container?

A Docker container provides isolation for an application and its required files and dependencies. Containers on the same host generally share the host operating system's kernel.

**Example:** Running an Nginx web server inside a Docker container.

## 3. Architecture Diagram

### Virtual Machines

```text
┌─────────────────────────────┐
│          Hardware           │
├─────────────────────────────┤
│          Hypervisor         │
├──────────────┬──────────────┤
│    VM 1      │     VM 2     │
├──────────────┼──────────────┤
│ Guest OS     │ Guest OS     │
├──────────────┼──────────────┤
│ Application  │ Application  │
└──────────────┴──────────────┘
```

### Docker Containers

```text
┌─────────────────────────────┐
│          Hardware           │
├─────────────────────────────┤
│          Host OS            │
├─────────────────────────────┤
│      Container Runtime      │
├──────────────┬──────────────┤
│  Container 1 │ Container 2  │
├──────────────┼──────────────┤
│ Application  │ Application  │
└──────────────┴──────────────┘
```

*Note: This is a simplified comparison. Docker Desktop on Windows and macOS typically runs Linux containers inside a lightweight Linux VM.*

## 4. Difference Between Docker and VM

| Feature | Virtual Machine | Docker Container |
|---|---|---|
| Virtualization | Hardware-level virtualization | Operating-system-level isolation |
| Operating system | Each VM has its own guest OS | Containers generally share the host kernel |
| Resource usage | Generally higher | Generally lower |
| Startup time | Usually slower | Usually faster |
| Size | Usually larger | Usually smaller |
| Isolation | Separate guest OS boundary | Isolated processes and resources |
| Example | Ubuntu in VirtualBox | Nginx in Docker |

## 5. Important Points

1. A VM virtualizes hardware using a hypervisor.
2. Each VM runs its own guest operating system.
3. Containers generally share the host operating system's kernel.
4. Containers are usually lightweight and start faster than VMs.
5. VMs can run different operating systems with their own kernels on a suitable hypervisor.
6. Docker is useful for packaging and running applications consistently.
7. Both VMs and containers provide isolation, but their isolation mechanisms differ.

## Conclusion

Virtual machines virtualize hardware and run separate guest operating systems, while Docker containers isolate applications and generally share the host kernel. Containers are often more lightweight, whereas VMs provide a separate guest operating system environment.
