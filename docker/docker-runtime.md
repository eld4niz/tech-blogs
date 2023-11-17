# Deep Dive into Docker Runtimes - Understanding containerd and runc

## ***Introduction***

Docker, the containerization technology, operates through a sophisticated interplay of components, seamlessly blending runtime intricacies, daemon orchestration, and container management. In this technical exploration, we dissect one of the Docker's core component: The Runtime.

However, there are at least three things to be aware of when referring to
Docker as a technology:

1. The runtime
2. The daemon (a.k.a. engine)
3. The orchestrator

![[docker-architecture]](docker-architecture.png)

## ***Containerd: The Core Container Runtime***

- _Overview:_ Containerd serves as the core runtime for Docker, managing the complete container lifecycle. It was originally a part of the Docker project but has evolved into an independent, industry-standard runtime.
- _Architecture:_ Containerd is designed with a modular architecture, allowing it to handle essential container operations such as image transfer, storage, and container execution. It communicates with higher-level orchestration systems like Kubernetes or Docker Swarm.

## ***Runc: The Container Execution Tool***

- _Role:_ Runc is a lightweight, command-line tool responsible for spawning and running containers. It leverages the underlying Linux features, such as cgroups and namespaces, to create isolated environments for applications.
- _OCI Compatibility:_ Runc is based on the Open Container Initiative (OCI) specifications, ensuring compatibility with other container runtimes that adhere to the same standards. This compatibility enables users to run containers across different runtimes seamlessly.

## ***Understanding communication between containerd and runc***

- _Handshake:_ Containerd and runc communicate through a well-defined API. Containerd instructs runc to start and manage containers, while runc reports back to containerd about the container's status and resource usage.
- _Flexibility:_ The separation of concerns between containerd and runc provides flexibility. Developers can choose alternative runtimes, such as kata-runtime or cri-o, without affecting the overall Docker ecosystem.

## ***Security***

- _Namespace Isolation:_ Both containerd and runc heavily rely on Linux namespaces to isolate processes, filesystems, and network resources. This ensures that containers are isolated from each other and the host system.
- _Capabilities:_ Runc allows fine-grained control over Linux capabilities, restricting containerized processes to only the necessary privileges. This enhances security by reducing the attack surface of containers.
