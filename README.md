# Orthanc KeyCloak Exploration
This project aims to explore the integration of Orthanc, a lightweight and open-source DICOM server, with Keycloak, a centralized Identity and Access Management (IAM) solution. By combining these tools, you can enhance security, authentication, and authorization for your medical imaging applications.

## Project Components
1. Nginx (Reverse Proxy for Orthanc and Keycloak)
    - Image: orthancteam/orthanc-nginx:24.5.1
    - Purpose: Handles incoming requests, routes them to the appropriate service (Orthanc or Keycloak), and provides an entry point for external access.
    - Configuration:
        - Enables Orthanc and Keycloak.
        - Disables HTTPS (for local development).
        - Enables OHIF (Open Health Imaging Foundation) viewer.
2. Orthanc (DICOM Server)
    - Image: orthancteam/orthanc:24.5.1
    - Purpose: Manages medical images and provides a RESTful API for querying and retrieving DICOM data.
    - Configuration:
        - Enables Stone Web Viewer and DICOM Web plugins.
        - Connects to a PostgreSQL database (configured in orthanc-config.json).
        - Enables verbose logging during startup.
3. Orthanc Auth Service
    - Image: orthancteam/orthanc-auth-service:24.5.1
    - Purpose: Provides authentication and authorization services for Orthanc.
    - Configuration:
        - Reads permissions from permissions.jsonc.
        - Integrates with Keycloak for user management.
        - Defines public endpoints for Orthanc and OHIF.
4. PostgreSQL (Database for Orthanc and Keycloak)
    - Image: postgres:14
    - Purpose: Stores Orthanc metadata and Keycloak configuration.
    - Configuration:
        - Trusts all connections (for local development).
5. OHIF Viewer
    - Image: orthancteam/ohif-v3:24.5.1
    - Purpose: Provides a web-based viewer for medical images (integrated with Orthanc).
6. Keycloak (Centralized IAM)
    - Image: orthancteam/orthanc-keycloak:24.5.1
    - Purpose: Manages user authentication, authorization, and identity federation.
    - Configuration:
        - Admin credentials: admin / change-me
        - Uses PostgreSQL as the database.
## Usage
1. Clone this repository.
2. Set up your environment variables (e.g., secrets, URLs).
3. Run docker-compose up -d to start the services.
4. Access Orthanc at http://localhost/orthanc/ and Keycloak at http://localhost/auth/.