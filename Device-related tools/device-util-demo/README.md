# Brezze Communication Service

## Project Overview

This project, `brezze-communication`, is a Spring Boot application that serves as the backend for a power bank rental system. It manages communication with IoT-enabled power bank stations, handles user authentication, processes payments, and monitors the status of the devices in real-time.

The system is designed as a multi-module Maven project, with a core communication module and a shared utilities module.

## How It Works

The application uses a combination of REST APIs and the MQTT protocol to communicate with the power bank stations.

1.  **Device Authentication**: Power bank stations authenticate with the server to establish a secure connection.
2.  **Real-time Communication**: The server uses MQTT to send commands to the stations (e.g., to pop a power bank) and to receive status updates, such as battery levels and station health.
3.  **User Interaction**: Users can interact with the system via a frontend (not included in this repository) that communicates with the REST APIs to rent and return power banks.
4.  **Payment Processing**: The system integrates with Stripe to handle payments for power bank rentals.
5.  **Order Management**: The application manages the lifecycle of rental orders, including sending email notifications to users.

## Key Features

*   **Device Management**: Onboarding and authentication of new power bank stations.
*   **Real-time Monitoring**: Live tracking of station and power bank status via MQTT.
*   **Remote Control**: Send commands to stations to perform actions like releasing a power bank.
*   **Order and Rental-Billing**: Manages rental sessions and billing.
*   **Payment Integration**: Secure payment processing using Stripe.
*   **RESTful API**: A comprehensive set of endpoints for frontend integration and system management.
*   **API Documentation**: Interactive API documentation provided by Knife4j.

## Technologies Used

*   **Backend**: Java 8, Spring Boot 2.2.6
*   **Data Persistence**: MySQL, MyBatis Plus
*   **Messaging**: RabbitMQ
*   **Communication**: MQTT (with EMQX and Aliyun IoT), Netty
*   **Payments**: Stripe
*   **API Documentation**: Knife4j
*   **Build Tool**: Maven

## How to Use It

### Prerequisites

*   Java 8
*   Maven
*   MySQL
*   RabbitMQ
*   An MQTT broker (like EMQX)

### Configuration

1.  Clone the repository.
2.  Set up your MySQL database and configure the connection details in `brezze-communication/src/main/resources/application.yml`.
3.  Configure your RabbitMQ and MQTT broker connection details in the same `application.yml` file.
4.  Add your Stripe API keys to the configuration.

### Building and Running

1.  Build the project from the root directory:
    ```bash
    mvn clean install
    ```
2.  Run the application:
    ```bash
    java -jar brezze-communication/target/brezze-communication-1.0.jar
    ```

The application will start on port `10000` by default.

### API Documentation

Once the application is running, you can access the API documentation at:

[http://localhost:10000/doc.html](http://localhost:10000/doc.html)

This will open the Knife4j interface, where you can explore and interact with all the available API endpoints.
