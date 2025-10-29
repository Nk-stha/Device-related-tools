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

*   `spring_boot_app`: The main Spring Boot application, configured to interact with MySQL and RabbitMQ.
*   `web-test-tool-demo`: A Nuxt.js web application for testing.
*   `web-cabinet-bind`: A web interface for cabinet binding.
*   `emqx1`, `emqx2`: EMQX MQTT brokers.
*   `mysql`: MySQL 8.0 database service.
*   `rabbitmq`: RabbitMQ message broker with management plugin.
*   `rabbitmq-init`: A one-time initialization service responsible for pre-creating essential RabbitMQ resources. It ensures that specific queues (like `ybt.delay.pb.open.lock`) are declared and ready *before* the Spring Boot application starts, preventing race conditions and ensuring reliable application startup. This service runs its command and then exits.

### Spring Boot Application (`spring_boot_app`) container

This service represents the core Spring Boot 2.2.6 application.

**Key Features:**
*   **API Documentation:** Knife4j is enabled for interactive API documentation, accessible at `http://localhost:10000/doc.html`.
*   **Database Connectivity:** Connects to the `mysql` service using the `utils-demo` database, with username `admin` and password `admin123`.
*   **Message Queuing:** Connects to the `rabbitmq` service using username `admin` and password `admin123`. It expects the `ybt.delay.pb.open.lock` queue to be pre-created.
*   **Port:** Exposed on host port `10000`.

**Configuration:**
*   The application's database and RabbitMQ connection details, along with Knife4j settings, are managed in `Device-related tools/device-util-demo/brezze-communication/src/main/resources/application.yml`.
*   The Docker image is built from the `Dockerfile` located at `./Device-related tools/device-util-demo`.

**Access:**
*   **Application API:** `http://localhost:10000`
*   **Knife4j UI:** `http://localhost:10000/doc.html`

### Network (`emqx-bridge`)

The `emqx-bridge` is a custom Docker bridge network that facilitates communication between all the services in this Docker Compose setup.

**Key aspects of this network:**
*   **Inter-Service Communication:** All services (EMQX brokers, MySQL, RabbitMQ, Spring Boot app, web frontends) are connected to this network, allowing them to communicate with each other.
*   **Service Discovery:** Services can refer to each other by their service names (e.g., `mysql`, `rabbitmq`) as hostnames within this network.
*   **Isolation:** It provides network isolation for the project's services from other networks on the host.
*   **EMQX Clustering:** This network is essential for the EMQX brokers (`emqx1`, `emqx2`) to form a cluster, as they use aliases within this network for inter-broker communication.
