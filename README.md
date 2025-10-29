# Device-related tools

This project contains a collection of tools for managing and interacting with devices.

## Setup Instructions

### Prerequisites

*   Docker
*   Docker Compose

### Running the Application

1.  **Clone the repository:**

    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2.  **Set permissions for emqx data directories:**

    This is a one-time setup step to ensure that the `emqx` containers have the necessary permissions to write to their data directories.

    ```bash
    mkdir -p emqx1_data emqx2_data && sudo chown -R 1000:1000 emqx1_data emqx2_data
    ```

3.  **Build and run the services:**

    ```bash
    docker compose up -d --build
    ```

    This will build the Docker images for all the services and start them in the background.

### Services

*   `device-util-demo`: The main Java application.
*   `web-test-tool-demo`: A Nuxt.js web application for testing.
*   `web-cabinet-bind`: A web interface for cabinet binding.
*   `emqx1`, `emqx2`: EMQX MQTT brokers.
