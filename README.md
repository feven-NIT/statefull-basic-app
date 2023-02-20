oc create secret generic postgres-credentials     --from-literal=POSTGRES_USER=task-user     --from-literal=POSTGRES_PASSWORD=mysecretpassword     --from-literal=POSTGRES_DB=task     --from-literal=POSTGRES_PORT=5432


cd todo-demo

./mvnw package

podman build -f src/main/docker/Dockerfile.jvm -t quay.io/feven/todoapp:latest .
podman tag quay.io/feven/todoapp:latest quay.io/feven/todoapp:$APP_VERSION
podman push quay.io/feven/todoapp:$APP_VERSION
podman push quay.io/feven/todoapp:latest    
