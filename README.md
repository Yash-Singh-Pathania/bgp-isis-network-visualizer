# BGP-ISIS Network Visualizer


## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)

## Introduction

Welcome to the **BGP-ISIS Network Visualizer**! This project is a Python-based application designed to simulate and visualize Border Gateway Protocol (BGP) and Intermediate System to Intermediate System (IS-IS) routing protocols within a Dockerized environment. It demonstrates in-depth knowledge of routing protocols, UNIX systems, TCP/IP networking fundamentals, and modern containerization techniques.

## Features

- **Routing Protocol Simulation:** Implements BGP and IS-IS protocols using FRRouting (FRR) to showcase dynamic routing and network convergence.
- **Containerization:** Utilizes Docker and Docker Compose to create isolated, reproducible network environments.
- **Real-Time Visualization:** Employs Python libraries like NetworkX and Matplotlib to generate real-time visual representations of network topologies and routing tables.
- **Automation:** Automates network configurations and protocol interactions with Python scripts.
- **Network Manipulation:** Allows for the addition of static routes, simulation of network conditions (e.g., latency, packet loss), and real-time troubleshooting using UNIX networking tools.

## Technologies Used

- **Programming Languages:** Python, Bash
- **Containerization:** Docker, Docker Compose
- **Routing Software:** FRRouting (FRR)
- **Visualization Libraries:** NetworkX, Matplotlib
- **Networking Protocols:** BGP, IS-IS
- **Automation Tools:** Netmiko, Paramiko
- **Operating Systems:** UNIX/Linux

## Architecture

The architecture consists of multiple Docker containers acting as routers running FRRouting. Python scripts interact with these containers to retrieve routing information and visualize the network topology dynamically.

## Prerequisites

Before you begin, ensure you have met the following requirements:

- **Operating System:** Ubuntu 20.04 or later
- **Docker:** Installed and running
- **Docker Compose:** Installed
- **Python:** Python 3.8 or later
- **Git:** Installed

## Installation

Follow these steps to set up the project locally.

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/bgp-isis-network-visualizer.git
cd bgp-isis-network-visualizer
```

### 2. Install Docker and Docker Compose

If Docker and Docker Compose are not already installed, install them using the following commands:

```bash
# Update package list
sudo apt-get update

# Install Docker
sudo apt-get install -y docker.io

# Install Docker Compose
sudo apt-get install -y docker-compose

# Start and enable Docker
sudo systemctl start docker
sudo systemctl enable docker
```

### 3. Install Python and Required Libraries

Ensure Python 3 and pip are installed. Then, install the necessary Python libraries:

```bash
sudo apt-get install -y python3 python3-pip
pip3 install -r requirements.txt
```

*Contents of `requirements.txt`:*
```
netmiko
paramiko
matplotlib
networkx
```

### 4. Build the Docker Image

Build the Docker image for FRRouting:

```bash
docker build -t frrouting .
```

### 5. Deploy Router Containers

Use Docker Compose to deploy the router containers:

```bash
docker-compose up -d
```

## Usage

### 1. Configure Networking Between Routers

Assign IP addresses and bring up network interfaces:

```bash
docker exec -it router1 ip addr add 192.168.1.1/24 dev eth0
docker exec -it router1 ip link set eth0 up

docker exec -it router2 ip addr add 192.168.2.2/24 dev eth0
docker exec -it router2 ip link set eth0 up
```

### 2. Start FRR Services Inside Containers

Start FRRouting services:

```bash
docker exec -it router1 /usr/local/sbin/frrinit.sh start
docker exec -it router2 /usr/local/sbin/frrinit.sh start
```

### 3. Verify Routing Protocols

Access the FRR shell and check BGP and IS-IS configurations:

```bash
docker exec -it router1 vtysh
```

Inside `vtysh`:

```bash
# Check BGP neighbors
show ip bgp summary

# Check IS-IS routes
show ip route isis
```

### 4. Visualize the Network

Run the Python visualization script to see the network topology:

```bash
python3 src/visualize_network.py
```

### 5. Dynamic Visualization

For real-time updates, run the dynamic visualization script:

```bash
python3 src/dynamic_visualization.py
```

### 6. Network Manipulation

Add static routes or simulate network conditions:

```bash
# Add a static route
docker exec -it router1 ip route add 10.0.0.0/24 via 192.168.1.2

# Simulate network latency and packet loss
docker exec -it router1 tc qdisc add dev eth0 root netem delay 100ms loss 10%
```

## Project Structure

```
bgp-isis-network-visualizer/
├── Dockerfile
├── docker-compose.yml
├── frr/
│   ├── bgpd.conf
│   └── isisd.conf
├── src/
│   ├── retrieve_routes.py
│   ├── visualize_network.py
│   └── dynamic_visualization.py
├── assets/
│   ├── logo.png
│   └── architecture.png
├── README.md
├── requirements.txt
├── LICENSE
└── .gitignore
```

- **Dockerfile:** Defines the Docker image for FRRouting.
- **docker-compose.yml:** Configures and deploys multiple router containers.
- **frr/**: Contains FRRouting configuration files (`bgpd.conf`, `isisd.conf`).
- **src/**: Python scripts for retrieving routes and visualizing the network.
- **assets/**: Images and diagrams used in the README.
- **requirements.txt:** Python dependencies.
- **LICENSE:** Project license.
- **.gitignore:** Specifies files to ignore in Git.

## Contributing

Contributions are welcome! Please follow these steps to contribute:

1. **Fork the Repository**

2. **Create a Feature Branch**

   ```bash
   git checkout -b feature/YourFeature
   ```

3. **Commit Your Changes**

   ```bash
   git commit -m "Add YourFeature"
   ```

4. **Push to the Branch**

   ```bash
   git push origin feature/YourFeature
   ```

5. **Open a Pull Request**

Please ensure your code follows the project's coding standards and includes appropriate tests.

## License

This project is licensed under the [MIT License](LICENSE).

## Contact

- **Your Name**
- **Email:** your.email@example.com
- **LinkedIn:** [linkedin.com/in/yourprofile](https://www.linkedin.com/in/yourprofile)
- **GitHub:** [github.com/yourusername](https://github.com/yourusername)

Feel free to reach out for any questions or collaboration opportunities!

## Acknowledgements

- **FRRouting (FRR):** [https://frrouting.org/](https://frrouting.org/)
- **Docker:** [https://www.docker.com/](https://www.docker.com/)
- **NetworkX:** [https://networkx.org/](https://networkx.org/)
- **Matplotlib:** [https://matplotlib.org/](https://matplotlib.org/)
- **Netmiko:** [https://github.com/ktbyers/netmiko](https://github.com/ktbyers/netmiko)
