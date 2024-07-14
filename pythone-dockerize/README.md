# Flask Project README

This project is a Python Flask application that demonstrates how to build a Docker image for a Flask web application using a multi-stage Dockerfile.

## Getting Started

### Prerequisites

- Docker installed on your local machine or server ([Docker installation guide](https://docs.docker.com/get-docker/))

### Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/your/repository.git
   cd repository-name
2. Build the Docker image using Dockerfile:
   ```bash
   docker image build -t <tag name >:version .
3. Run the Docker container:
   ```bash
   docker container run -it -p 5000:5000 <image name> /bin/bash
4. Access the application in your browser at http://<public ip>:5000.
  ### Dockerfile
  The Dockerfile provided uses multi-stage builds to optimize the final Docker image size. Here's a breakdown of the Dockerfile:
   ```bash
   # Stage 1: Build environment
FROM python:3.9-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Stage 2: Runtime environment
FROM python:3.9-slim AS runtime
WORKDIR /app
COPY --from=builder /usr/local/lib/python3.9/site-packages /usr/local/lib/python3.9/site-packages
COPY . .
CMD ["python", "app.py"]
