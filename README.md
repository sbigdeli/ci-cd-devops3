# CI/CD Pipeline for Nginx with Minikube and Ansible

How to set up a local CI/CD pipeline for deploying an Nginx containerized app to Minikube using Ansible.

## Features

- Builds and pushes a Docker image to GitHub Container Registry (GHCR).
- Deploys the application to Minikube using Kubernetes.
- Performs rolling updates with Ansible.
- Provides a local dashboard for monitoring.

## Prerequisites (Optional)

Install tools below:
- [Minikube](https://minikube.sigs.k8s.io/docs/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Ansible](https://www.ansible.com/)
- [Docker](https://docs.docker.com/get-docker/) 

## 1. Clone the repository
```bash
git clone git@github.com:sbigdeli/ci-cd-devops3.git
```

## 2. Run on local machine

```bash
minikube start

kubectl apply -f nginx-deployment.yml
kubectl apply -f nginx-service.yml

kubectl get pods
kubectl get deployment

minikube service nginx-service

minikube dashboard
```

## 3. Change to a new version

```bash
ansible-playbook deploy-playbook.yml --extra-vars "new_version=v15.0.0" # See tags, try a tag that's not tagged.
```

## 4. Check if the version is updated

```bash
minikube dashboard
kubectl get pods
kubectl rollout status deployment/nginx-deployment
```

## 5. Exit

```bash
minikube stop
minikube delete --all --purge # Removes images and volumes!
```

