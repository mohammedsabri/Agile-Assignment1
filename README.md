## Docker Assignment - Agile Software Practice.

Name:Mohammed sabri (20113428)

Demo: https://youtu.be/KKjfxeXIhRw for YouTube video 

This repository contains the Docker containerization setup for a multi-component Movies application. The application architecture includes a Movies API that interacts with a MongoDB database for storing movie information, a Redis server for caching and rate-limiting API requests, and Mongo Express for database management during development.
illustrated below.
![](./images/arch.png)

The application consists of four main containers:

Movies API: The core API providing movie data endpoints. It interacts with MongoDB to fetch and store movie information, with Redis caching responses to improve response times and rate-limit requests to prevent excessive usage.

MongoDB: This NoSQL database stores the main movie data. It’s optimized for flexible data storage and works well with JSON-like structures, which makes it a good choice for this kind of application.

Redis: Redis serves two purposes in this application:
Caching: Redis caches responses from the Movies API to reduce direct database calls and speed up response times.

Rate Limiting: Redis rate-limits requests to specific API endpoints, ensuring controlled access and enhancing stability under high load.

Mongo Express: This is a web-based interface for MongoDB administration. In development mode, Mongo Express allows for easy data inspection and management, making it easier to track and manage the movie records.

Container Isolation: The containers are configured with specific network rules to limit access:
The Movies API can interact with Redis and MongoDB.
Redis and MongoDB are isolated from each other for enhanced security.
Mongo Express is only accessible in development mode for easy data management

Database Seeding.

Database Seeding: A mongo-seed service is configured to populate MongoDB with initial data in development mode, allowing for easy setup and testing of the Movies API endpoints.

found an example showing how add this to the Docker compose @ https://github.com/stefanwalther/docker-mongo-seed/blob/master/docker-compose.yml

M.ulti-Stack.

the application supports both development and production stack options, with distinct configurations:

Development Stack: The full stack is deployed, including Mongo Express for MongoDB management and a seeding process to populate the database with sample data.


Production Stack: In production, Mongo Express is not deployed, and no seeding takes place.


Development Stack - docker-compose --profile development up -d 
To start the application in development mode, use the default docker-compose.yml file. This setup includes all services, with Mongo Express enabled for database management and automatic database seeding for testing.

Production Stack - docker-compose  up -d 
For production run the application without Mongo Express or database seeding. To do this, either modify the docker-compose.yml file or create an override file (docker-compose.prod.yml) that excludes the Mongo Express service and any seeding configurations.


Setup Instructions
To get started with this project, clone the repository, and follow the steps outlined in the README for configuring environment variables and running the Docker Compose file.

Using `compose.yaml` from last lab `docker-profile-app` 
Added `cache` service that uses `redis:alpine` image
 Added the movie api environments
 Added `mongo-express-database-network` network so the Express web app can only reach the MongoDB database.
Added `database-movies-network` network so the Movies API can reach the MongoDB database.
Added `cache-movies-network` network so the Movies API can reach the Redis cache.
For production  `docker compose up` starts production stack. 
fOR development `docker compose --profile development up` starts development stack.

Added  an image for seeding from expamle i found on stackoverflow
the command provided runs the mongoimport which is a MongoDB utility for importing jason data into MongoDB `--authenticationDatabase=admin` flag to avoid `mongoimport`

Container name mongo-seed to make it easier to identify in docker..

For volumes the binds gets the seeding.json file from local filesystem into the container.
The type linksa specific file or directory from the system into the container.
The source ./seeding.json is specifiespath to seeding.json in the project.

the target ./seeding.json is the path within the container where the file is accessible.

Added a  `database-mongo-seed-network` network fpr the  seed image so it can reach the MongoDB database.

  I used `command` property and bind mount instead of building a whole new image.

  Resources used

  . https://stackoverflow.com/questions/68927857/mongoexport-auth-error-using-mechanism-scram-sha-1/68937584#68937584

  . https://stackoverflow.com/questions/31210973/how-do-i-seed-a-mongo-database-using-docker-compose/55819683#55819683

  . https://docs.docker.com/compose/how-tos/profiles/

  .https://docs.docker.com/compose/intro/compose-application-model/

  .https://labex.io/tutorials/docker-how-to-isolate-networks-between-docker-containers-417536

  .https://stackoverflow.com/questions/31210973/how-do-i-seed-a-mongo-database-using-docker-compose

  .https://github.com/stefanwalther/docker-mongo-seed/blob/master/docker-compose.yml