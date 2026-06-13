# Softy Pinko Docker Infrastructure

## Project Overview

This project demonstrates how to build a multi-container application using Docker and Docker Compose.

The architecture includes:

* Front-End server using Nginx
* Back-End API server using Flask
* Reverse Proxy using Nginx
* Docker Compose orchestration
* Round Robin Load Balancing with multiple API instances

The goal of this project is to understand how modern web applications are deployed using containers and reverse proxies.

---

## Architecture

```text
Client Browser
      |
      v
+-------------+
| Nginx Proxy |
+-------------+
      |
  +---+---+
  |       |
  v       v
Front-End API Servers
(Nginx)   (Flask)
```

The proxy server acts as the single entry point for all incoming traffic.

* Requests to `/` are forwarded to the Front-End server.
* Requests to `/api` are forwarded to the Back-End API servers.
* Multiple API instances can be launched and load balanced automatically using Docker Compose.

---

## Technologies Used

* Docker
* Docker Compose
* Nginx
* Python 3
* Flask
* Flask-CORS

---

## Project Structure

```text
task6/
│
├── back-end/
│   ├── Dockerfile
│   └── api.py
│
├── front-end/
│   ├── Dockerfile
│   ├── softy-pinko-front-end.conf
│   └── softy-pinko-front-end/
│
├── proxy/
│   ├── Dockerfile
│   └── proxy.conf
│
├── docker-compose.yml
└── 2-api-servers.txt
```

---

## Build Containers

```bash
docker compose build
```

---

## Run Application

```bash
docker compose up
```

The application will be available at:

```text
http://localhost
```

---

## Scale API Servers

Launch multiple API servers:

```bash
docker compose up --scale back-end=2
```

Example:

```bash
docker compose up --scale back-end=5
```

Docker Compose automatically creates multiple instances of the Back-End service.

---

## Reverse Proxy

The proxy server listens on port 80 and routes requests as follows:

```text
/      -> Front-End Server
/api   -> Back-End Server
```

This allows clients to communicate with a single endpoint without knowing the location of internal services.

---

## Load Balancing

Nginx performs Round Robin load balancing between API instances.

Example:

```text
Request 1 -> API 1
Request 2 -> API 2
Request 3 -> API 1
Request 4 -> API 2
```

This improves scalability and distributes traffic evenly across servers.

---

## Learning Outcomes

By completing this project, I learned:

* Docker image creation
* Container management
* Docker Compose orchestration
* Service discovery using Docker DNS
* Reverse Proxy concepts
* Nginx configuration
* Flask API deployment
* Cross-Origin Resource Sharing (CORS)
* Horizontal scaling
* Round Robin load balancing
* Multi-container application architecture

```
```
