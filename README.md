# Docker Lite Container Runtime from Scratch

A comprehensive implementation of a lightweight container runtime system built from scratch, demonstrating core containerization concepts including namespaces, cgroups, networking, and service orchestration.

## 📋 Project Overview

This project implements a Docker-like container runtime system with four main tasks that progressively build up containerization capabilities:

- **Task 1**: Linux Namespace Isolation
- **Task 2**: Basic Container Implementation
- **Task 3**: Container Management System (Conductor)
- **Task 4**: Service Orchestration with Microservices

## 🏗️ Project Structure

```
├── task1/                    # Linux Namespace Implementation
│   └── namespace_prog.c     # Demonstrates PID and UTS namespaces
├── task2/                    # Basic Container Implementation
│   ├── container_prog.c     # Container program with isolation features
│   └── simple_container.sh  # Shell script for container management
├── task3/                    # Container Management System
│   ├── conductor.sh         # Main container orchestration tool
│   └── config.sh           # Configuration file for conductor
└── task4/                    # Service Orchestration
    ├── counter-service/     # C-based counter microservice
    ├── external-service/    # Python Flask web service
    ├── service-orchestrator.sh  # Service deployment script
    └── .containers/         # Container runtime directory
```

## 🚀 Getting Started



### Prerequisites

- Linux system (Ubuntu/Debian recommended)
- Root privileges (for namespace operations)
- Required packages:
  ```bash
  sudo apt-get update
  sudo apt-get install build-essential debootstrap iproute2 bridge-utils
  ```

### Building and Running

#### Task 1: Namespace Isolation

```bash
cd task1
gcc -o namespace_prog namespace_prog.c
sudo ./namespace_prog
```

This demonstrates Linux namespace isolation by creating child processes with separate PID and UTS namespaces.

#### Task 2: Basic Container

```bash
cd task2
gcc -o container_prog container_prog.c
sudo ./simple_container.sh
```

Runs a basic container with hostname isolation and root filesystem listing.

#### Task 3: Container Management

```bash
cd task3
sudo ./conductor.sh build my-image
sudo ./conductor.sh run my-image my-container -- sleep infinity
sudo ./conductor.sh exec my-container -- /bin/bash
```

The conductor provides a complete container management system with:
- Image building using debootstrap
- Container lifecycle management
- Network configuration
- Process execution within containers

#### Task 4: Service Orchestration

```bash
cd task4
sudo ./service-orchestrator.sh
```

Deploys a complete microservices architecture:
- **Counter Service**: C-based HTTP service with increment functionality
- **External Service**: Python Flask web service that communicates with counter service
- **Network Configuration**: Isolated container networking with port forwarding

## 🔧 Key Features

### Namespace Isolation (Task 1)
- **PID Namespace**: Process isolation
- **UTS Namespace**: Hostname isolation
- **Clone System Call**: Demonstrates namespace creation

### Container Implementation (Task 2)
- **Hostname Modification**: Container-specific hostnames
- **Root Filesystem Listing**: Isolated file system view
- **Benchmark Testing**: Performance measurement within containers

### Container Management (Task 3)
- **Image Management**: Build and manage container images
- **Container Lifecycle**: Create, start, stop, and delete containers
- **Network Configuration**: Bridge networking with port forwarding
- **Process Execution**: Execute commands within running containers

### Service Orchestration (Task 4)
- **Microservices Architecture**: Counter and web services
- **Container Networking**: Peer-to-peer and external network connectivity
- **Port Forwarding**: Host-to-container port mapping
- **Service Discovery**: Automatic IP address resolution

## 🌐 Networking

The system supports multiple networking modes:
- **Bridge Networking**: Containers connected to host network
- **Peer Networking**: Direct container-to-container communication
- **Port Forwarding**: Host port to container port mapping
- **Internet Access**: External connectivity for containers

## 📊 API Endpoints

### Counter Service (Port 8080)
- `GET /get_counter` - Get current counter value
- `GET /increment_counter` - Increment counter
- `GET /get_and_increment_counter` - Get and increment counter
- `GET /reset_counter` - Reset counter to zero

### External Service (Port 3000 on host)
- `GET /` - Main endpoint that communicates with counter service

## 🛠️ Development

### Building Services

#### Counter Service
```bash
cd task4/counter-service
make
```

#### External Service
```bash
cd task4/external-service
pip install flask requests
```

### Testing

1. **Basic Container Test**:
   ```bash
   cd task2
   sudo ./simple_container.sh
   ```

2. **Service Integration Test**:
   ```bash
   cd task4
   sudo ./service-orchestrator.sh
   curl http://localhost:3000
   ```

## 🔍 Troubleshooting

### Common Issues

1. **Permission Denied**: Ensure you're running with root privileges
2. **Network Issues**: Check if bridge interface is properly configured
3. **Container Won't Start**: Verify image exists and dependencies are installed

### Debug Commands

```bash
# Check container status
sudo ./conductor.sh ps

# View container logs
sudo ./conductor.sh exec <container> -- dmesg

# Network debugging
ip netns list
ip addr show
```

## 📚 Learning Objectives

This project demonstrates:
- Linux kernel namespaces and cgroups
- Container runtime implementation
- Network virtualization
- Service orchestration
- Microservices architecture
- System programming concepts



