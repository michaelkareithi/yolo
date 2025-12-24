# Choice of the Base Image
Client & Backend: node:20-alpine
-Lightweight and secure, optimized for production.
-Alpine reduces image size and attack surface.

Database: mongo:6.0
-Official MongoDB image guarantees compatibility and stability.

# Dockerfile Directives
-WORKDIR:Defines working directory within container (/app).
-COPY package*.json ./*: Copies dependency files first for efficient caching.
-RUN npm install: Installs the dependencies.
COPY. .: Copies application code.
-EXPOSE: Specifies the container port. Usually, 3000 for the frontend and 5000 for the backend.
-CMD ["npm", "start"]: Defines startup command.

# Docker-Compose Networking
-Bridge Network: The custom network ecommerce-net connects all services.
-Port Mapping:depends on makes sure the correct order at startup: backend waits for MongoDB, frontend waits for backend.
Client → 3000:3000
Backend → 5000:5000
MongoDB → 27017:27017

# Docker-Cmpose Volumes
-mongo-data:/data/db
Ensures that the persistence of product data remains even across container restarts.
Thus, this feature is critical to test an "Add Product" functionality.

# Git Workflow
-Branching: docker-setup branch is created for containerization tasks. 
-Commits: Incremental commits for Dockerfiles, docker-compose.yml and explanation.md. 
-Push & Merge: Branched has been pushed to GitHub and merged into the main.
-For Practice: Use clear commit messages, such as "Added Docker setup for ecommerce app".