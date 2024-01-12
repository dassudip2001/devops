# Create Docker Network

- docker network create <your network name>

# Show All The Network

- docker network ls

# Create mongo db

- docker run -d \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=admin \
  --network mongo
  --name mongodb \
  mongo

# Create mongo Express Container

- docker run -d \
  -p 8081:8081 \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME =admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD =admin \
  -e ME_CONFIG_MONGODB_SERVER=mongodb  
  --network mongo
  --name mongodb-express \
  mongo-express

# check password for mongo express

docker log mongo-express is

# How To Export Secret

export MONGO_ADMIN_USERNAME=
export MONGO_ADMIN_PASSWORD=
