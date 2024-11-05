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