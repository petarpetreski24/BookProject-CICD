# Book Project

This is a web application used for Dockerization and orchestration for a Django Project.

## Docker

To initialize the project using Docker, follow these steps:

1. Create a `.env` file in the root directory with the following environment variables:

    ```env
    POSTGRES_USERNAME=database username
    POSTGRES_DATABASE=database name
    POSTGRES_PASSWORD=database password
    ```

2. Start the Docker containers:

    ```sh
    docker-compose up
    ```

## Kubernetes

To initialize the project using Kubernetes, follow these steps (if using k3d):

1. Create a cluster:

    ```sh
    k3d cluster create bookproject -p "9000:80@loadbalancer"
    ```

2. Apply the manifests (the manifests are located in the `kubernetes` folder):

    ```sh
    kubectl apply -f namespace.yaml -f db-configmap.yaml -f db-secret.yaml -f db-pvc.yaml -f db-statefulset.yaml -f db-service.yaml -f configmap.yaml -f secret.yaml -f deployment.yaml -f service.yaml -f ingress.yaml
    ```

3. Apply the migrations (if not already applied):

    ```sh
    kubectl exec -it <pod-name> -n bookproject-cicd -- python manage.py migrate
    ```

---
