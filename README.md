# mongodb

### mongodb
```bash
# docker network create mongodb-network
# docker network ls

mkdir -p /opt/crudapi/mongodb
chmod 777 /opt/crudapi/mongodb

docker rm -f mongodb
docker run --privileged --name "mongodb" \
    --restart=always \
    -e "MONGO_INITDB_DATABASE=crudapi" \
    -e "MONGO_INITDB_ROOT_USERNAME=root" \
    -e "MONGO_INITDB_ROOT_PASSWORD=root" \
    -p "27017:27017" \
    -v /opt/crudapi/mongodb:/data/db \
    -d mongo
```

###  mongo-express
```bash
docker rm -f mongo-express
docker run --name mongo-express \
   --link mongodb:mongo \
   --restart=always \
   -p 7017:8081 \
   -e ME_CONFIG_MONGODB_SERVER="mongo" \
   -e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" \
   -e ME_CONFIG_MONGODB_ADMINUSERNAME="root" \
   -e ME_CONFIG_MONGODB_ADMINPASSWORD="root" \
   -e ME_CONFIG_BASICAUTH_USERNAME="crudapi" \
   -e ME_CONFIG_BASICAUTH_PASSWORD="crudapi" \
   -d mongo-express:0.54
docker logs -f mongo-express
```
