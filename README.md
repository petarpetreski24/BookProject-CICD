# Book Project

Ова е веб апликација користена за докеризација и оркестрација за проектната задача по предметот Континуирана интеграција и Испорака

## Docker

За иницијализација на проектот користејќи Docker, чекорите се:

1. Креирање на .env фајл во root-от со следниве околински променливи:

    ```env
    POSTGRES_USERNAME=username за базата на податоци
    POSTGRES_DATABASE=име на датабазата
    POSTGRES_PASSWORD=лозинка за базата на податоци
    ```

2. Започнување на Docker контејнерите:

    ```sh
    docker-compose up
    ```

## Kubernetes

За иницијализација на проектот користејќи Kubernetes, чекорите се (доколку се користи k3d):

1. Креирање на кластер

    ```sh
    k3d cluster create bookproject -p "9000:80@loadbalancer"
    ```

2. Применување на манифестите (манифестите се наоѓаат во kubernetes фолдерот)

    ```sh
    kubectl apply -f namespace.yaml -f db-configmap.yaml -f db-secret.yaml -f db-pvc.yaml -f db-statefulset.yaml -f db-service.yaml -f configmap.yaml -f secret.yaml -f deployment.yaml -f service.yaml -f ingress.yaml
    ```

3. Применување на миграциите (доколку не се применети):

    ```sh
    kubectl exec -it <pod-name> -n bookproject-cicd -- python manage.py migrate
    ```

