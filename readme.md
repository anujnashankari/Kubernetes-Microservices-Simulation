# Kubernetes-Microservices-Simulation

A comprehensive Kubernetes-like cluster simulator that demonstrates container orchestration, pod scheduling, and resource management using Docker containers and a modern web interface.

## 🚀 Features

- **Real Container Management**: Uses Docker to create and manage actual containers for nodes and pods
- **Multiple Scheduling Algorithms**: 
  - First Fit
  - Best Fit  
  - Worst Fit
- **Node Management**: Add, update, remove, and monitor cluster nodes
- **Pod Orchestration**: Launch, reschedule, and manage pods with CPU resource allocation
- **Health Monitoring**: Automatic health checks with heartbeat mechanism
- **Real-time Updates**: Live dashboard with automatic refresh
- **Interactive UI**: Bootstrap-powered responsive web interface

## 🏗️ Architecture

### Backend Components
- **Node Manager**: Handles cluster node lifecycle and resource tracking
- **Pod Scheduler**: Implements various scheduling algorithms for optimal pod placement
- **Docker Manager**: Manages actual Docker containers for realistic simulation
- **Health Monitor**: Monitors node health and handles failure scenarios

### Frontend
- **Modern Web UI**: Bootstrap 5 with responsive design
- **Real-time Dashboard**: Live updates of cluster status
- **Interactive Controls**: Forms for managing nodes, pods, and scheduling algorithms

## 📋 Prerequisites

- **Node.js** (v14 or higher)
- **Docker** (running and accessible)
- **npm** or **yarn**

## 🔧 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/anujnashankari/Kubernetes-Microservices-Simulation.git
   cd Kubernetes-Microservices-Simulation
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Ensure Docker is running**
   ```bash
   docker --version
   ```

4. **Start the server**
   ```bash
   npm start
   ```

5. **Open your browser**
   Navigate to `http://localhost:3000`

## 🎮 Usage

### Adding Nodes
1. Enter a unique Node ID
2. Specify CPU cores available
3. Click "Add Node" - a Docker container will be created

### Launching Pods
1. Specify CPU requirement
2. Click "Launch Pod" - the scheduler will find the best node
3. A Docker container will be created and linked to the selected node

### Scheduling Algorithms
- **First Fit**: Assigns pod to the first node with sufficient resources
- **Best Fit**: Assigns pod to the node with the least available resources that can still fit
- **Worst Fit**: Assigns pod to the node with the most available resources

### Monitoring
- **System Status**: Overview of total nodes, health status, and pod count
- **Resource Usage**: Visual bars showing CPU utilization per node
- **Health Checks**: Automatic monitoring with heartbeat mechanism
- **Container IDs**: Real Docker container identifiers displayed

## 🐳 Docker Integration

The simulator creates real Docker containers:
- **Node Containers**: Represent cluster nodes running Alpine Linux
- **Pod Containers**: Represent application pods with proper labeling
- **Automatic Cleanup**: Containers are properly removed when nodes/pods are deleted

### Container Naming Convention
- Nodes: `{nodeId}-{timestamp}`
- Pods: `pod-{podId}-{timestamp}`

## 📡 API Endpoints

### Nodes
- `POST /api/nodes` - Add a new node
- `GET /api/nodes` - List all nodes
- `GET /api/nodes/:nodeId` - Get specific node details
- `PUT /api/nodes/:nodeId` - Update node configuration
- `DELETE /api/nodes/:nodeId` - Remove node
- `POST /api/nodes/:nodeId/heartbeat` - Send heartbeat

### Pods
- `POST /api/pods` - Launch a new pod
- `GET /api/pods` - List all pods
- `GET /api/pods/:podId` - Get specific pod details
- `PUT /api/pods/:podId` - Update pod configuration
- `DELETE /api/pods/:podId` - Remove pod

### Scheduler
- `POST /api/scheduler/algorithm` - Set scheduling algorithm
- `GET /api/scheduler/algorithm` - Get current algorithm

## 🧪 Example Scenarios

### Basic Cluster Setup
```bash
# Add nodes with different capacities
curl -X POST http://localhost:3000/api/nodes \
  -H "Content-Type: application/json" \
  -d '{"nodeId": "node-1", "cpuCores": 4}'

curl -X POST http://localhost:3000/api/nodes \
  -H "Content-Type: application/json" \
  -d '{"nodeId": "node-2", "cpuCores": 8}'

# Launch pods with different requirements
curl -X POST http://localhost:3000/api/pods \
  -H "Content-Type: application/json" \
  -d '{"cpuRequirement": 2}'
```

### Algorithm Testing
```bash
# Set scheduling algorithm
curl -X POST http://localhost:3000/api/scheduler/algorithm \
  -H "Content-Type: application/json" \
  -d '{"algorithm": "best-fit"}'
```

## 🔍 Monitoring & Debugging

### Health Monitoring
- Nodes send heartbeats every 5 seconds
- Nodes marked unhealthy after 10 seconds of missed heartbeats
- Automatic pod rescheduling on node failure

### Logging
- Server logs all container operations
- Failed operations are logged with detailed error messages
- Health check results are logged periodically

### Docker Commands for Debugging
```bash
# List all simulation containers
docker ps -a --filter label=type=cluster-node
docker ps -a --filter label=type=pod

# View container logs
docker logs <container-name>

# Clean up all simulation containers
docker rm -f $(docker ps -aq --filter label=type=cluster-node)
docker rm -f $(docker ps -aq --filter label=type=pod)
```

## 🛠️ Development

### Project Structure
```
├── server.js          # Express server with API endpoints
├── public/
│   └── index.html     # Frontend web interface
├── package.json       # Dependencies and scripts
└── README.md         # This file
```

### Key Technologies
- **Backend**: Node.js, Express.js
- **Container Runtime**: Docker
- **Frontend**: Bootstrap 5, Vanilla JavaScript
- **HTTP Client**: Fetch API
