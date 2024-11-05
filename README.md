## Agile Software Practice - Assignment 1.
# Agile Software Practice - Assignment 1
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

  