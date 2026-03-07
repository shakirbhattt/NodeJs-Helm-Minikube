# NodeJs DevOps - Local

This is a demo application to use for working on the Swimlane DevOps hiring practical project.

### Install

Required environment variables:
- `MONGODB_URL` - Full MongoDB connection URI to connect to

### Testing Locally
```sh
git clone git://github.com/swimlane/devops-practical.git
npm install
cp .env.example .env
npm start
```

Then visit [http://localhost:3000/](http://localhost:3000/)


# NodeJs DevOps - Minikube

Node.js + MongoDB app containerized with Docker and deployed to Kubernetes (Minikube) using Helm.

## Repo Structure

```

├── app-source
    └── Dockerfile
    └── helm/
    └── swimlane-app/
       ├── Chart.yaml
       ├── values.yaml
       └── templates/
           ├── mongodb-deployment.yaml
           ├── mongodb-pvc.yaml
           ├── mongodb-service.yaml
           ├── deployment.yaml
           ├── service.yaml
```

## Deploy Steps

```bash
# 1. Start Minikube
minikube start --driver=docker --profile=swimlane

# 2. Build image inside Minikube
eval $(minikube -p swimlane docker-env)
docker build -t swimlane-app:latest .

# 3. Deploy with Helm
kubectl create namespace swimlane
helm install swimlane ./helm/swimlane-app --namespace swimlane

# 4. Wait for pods
kubectl get pods -n swimlane -w

# 5. Get URL
minikube -p swimlane service swimlane-app -n swimlane --url

# 6. Share via ngrok
ngrok http <url-from-above>
```


