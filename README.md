# Demo Voting App Kubernetes Deployment

This repository contains Kubernetes manifests for deploying a demo voting application. The application consists of multiple components, each running in its own pod, with services to expose and connect them.

## Architecture

The application is composed of the following components:

1. **Voting App**  
   A frontend application where users can vote.  
   - Pod: `voting-app-pod`
   - Service: `voting-service` (NodePort: 30004)

2. **Result App**  
   A frontend application to display voting results.  
   - Pod: `result-app-pod`
   - Service: `result-service` (NodePort: 30005)

3. **Worker App**  
   A backend worker that processes votes and updates the database.  
   - Pod: `worker-app-pod`

4. **PostgreSQL Database**  
   A database to store voting data.  
   - Pod: `postgres-pod`
   - Service: `db` (Port: 5432)

5. **Redis**  
   A caching layer to temporarily store votes.  
   - Pod: `redis-pod`
   - Service: `redis` (Port: 6379)

## Files

The repository contains the following Kubernetes manifest files:

- `postgres-pod.yaml`: Defines the PostgreSQL pod.
- `postgres-service.yaml`: Exposes the PostgreSQL pod as a service.
- `redis-pod.yaml`: Defines the Redis pod.
- `redis-service.yaml`: Exposes the Redis pod as a service.
- `voting-app-pod.yaml`: Defines the Voting App pod.
- `voting-app-service.yaml`: Exposes the Voting App pod as a service.
- `result-app-pod.yaml`: Defines the Result App pod.
- `result-app-service.yaml`: Exposes the Result App pod as a service.
- `worker-pod.yaml`: Defines the Worker App pod.

## How to Deploy

1. Apply the manifests in the following order to ensure proper dependencies:
   ```bash
   kubectl apply -f postgres-pod.yaml
   kubectl apply -f postgres-service.yaml
   kubectl apply -f redis-pod.yaml
   kubectl apply -f redis-service.yaml
   kubectl apply -f voting-app-pod.yaml
   kubectl apply -f voting-app-service.yaml
   kubectl apply -f result-app-pod.yaml
   kubectl apply -f result-app-service.yaml
   kubectl apply -f worker-pod.yaml

2. Verify that all pods and services are running:
    ```bash
    kubectl get pods
    kubectl get services
    ```

3. Access the application:

    - **Voting App**: `http://<node-ip>:30004`
    - **Result App**: `http://<node-ip>:30005`

4. Cleanup:
    To delete all resources, run:
    ```bash
    kubectl delete -f .
    ```

5. Notes:
    - Ensure that your Kubernetes cluster is running and accessible.
    - Modify the manifests if needed to suit your environment (e.g., change NodePort values or add persistent storage for the database).
    - Enjoy deploying and using the demo voting app!