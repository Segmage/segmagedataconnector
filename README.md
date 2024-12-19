### Segmage Data Connector Installation Guide

Welcome to the **Segmage Data Connector**! This guide will help you set up the application using Docker, either using the provided `docker-compose.yml` file or directly running the container.

---

### Prerequisites

Before proceeding, ensure you have the following installed on your system:
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/) *(optional, for compose usage)*

---

### Installation Steps with Docker Compose

1. **Clone the Repository**  
   Clone the GitHub repository that contains the `docker-compose.yml` file:
   ```bash
   git clone https://github.com/your-repo-name/segmage-data-connector.git
   cd segmage-data-connector
   ```

2. **Configure the Environment** *(Optional)*  
   If you need to customize settings (e.g., time zone, certificate path, page size, etc.), edit the `docker-compose.yml` file:
   ```yaml
   environment:
     - CollectUrl="https://collect.segmage.com"  # Use only for on-premise configurations.
     - Certificate__Path="certs/certificate.pfx" # Path to your custom certificate (optional).
     - Certificate__Password="YourSecurePassword" # Password for the certificate (optional).
     - PageSize=5000                              # Page size for SQL queries (default is 5000).
     - TZ=Europe/Istanbul                         # Specify your timezone (optional).
   ```

3. **Start the Application**  
   Use Docker Compose to pull the latest image and start the application:
   ```bash
   docker-compose up -d
   ```

4. **Access the Application**  
   Once the container is running, access the application via the following URL:
   ```
   https://localhost:24443
   ```

---

### Running the Application Without Docker Compose

If you prefer not to use Docker Compose, you can run the application directly using the following steps:

1. **Pull the Docker Image**  
   Download the latest Segmage Data Connector image from Docker Hub:
   ```bash
   docker pull segmage/dataconnector:latest
   ```

2. **Run the Container**  
   Start the container with the required configurations:
   ```bash
   docker run -d \
     --name segmage-data-connector \
     -p 24443:24443 \
     -v segmage-logs:/app/logs \
     -v segmage-db:/app/db \
     segmage/dataconnector:latest
   ```

3. **Access the Application**  
   Similar to the Docker Compose method, access the application via:
   ```
   https://localhost:24443
   ```

4. **Volume Management**  
   Ensure the following volumes are properly mapped:
   - **Logs**: `segmage-logs` is used for storing error log files.
   - **Database**: `segmage-db` is used for storing the application database.

---

### Volume Configuration

- **Logs**: Error logs are stored in the `logs` volume, mapped to `/app/logs` inside the container.  
- **Database**: The application database file is stored in the `db` volume, mapped to `/app/db` inside the container.

---

### Stopping the Application

To stop and remove the containers, run:
```bash
docker-compose down
```
Or, if running without Docker Compose:
```bash
docker stop segmage-data-connector
   docker rm segmage-data-connector
```

---

### Updating the Application

To update the Segmage Data Connector to the latest version:

**With Docker Compose:**
1. Pull the latest image:
   ```bash
   docker-compose pull
   ```
2. Restart the application:
   ```bash
   docker-compose up -d
   ```

**Without Docker Compose:**
1. Pull the latest image:
   ```bash
   docker pull segmage/dataconnector:latest
   ```
2. Stop and remove the existing container:
   ```bash
   docker stop segmage-data-connector
   docker rm segmage-data-connector
   ```
3. Restart the container with the updated image:
   ```bash
   docker run -d \
     --name segmage-data-connector \
     -p 24443:24443 \
     -v segmage-logs:/app/logs \
     -v segmage-db:/app/db \
     segmage/dataconnector:latest
   ```

---

### Troubleshooting

- **Logs**: Check logs for errors:
  ```bash
  docker logs segmage-data-connector
  ```
- **Ports**: Ensure port `24443` is not used by another application.

---

Feel free to reach out for support if you encounter any issues. Happy integrating! 🎉

---

