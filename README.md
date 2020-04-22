# Udagram Microservices

This starter code was provided by Udacity. This project is made for learning Kubernetes, docker and stuff related to deployment
It is split into 3 projects. 2 Microservices and 1 Front-End Application


### Installing Node and NPM
This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (NPM is included) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

### Installing Ionic Cli
The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI can be found in the [Ionic Framework Docs](https://ionicframework.com/docs/installation/cli).

### Installing project dependencies

The three projects need this command to be run inside their directiories to install all needed dependencies.
```bash
npm install
```

***
### Running the Development Server
Ionic CLI provides an easy to use development server to run and autoreload the frontend. This allows you to make quick changes and see them in real time in your browser. To run the development server, open terminal and run:

```bash
ionic serve
```

### Kubernetes Cluster Deployment
Firstly create docker images for each of the projects and push to docker hub:
```bash
docker build -t <username>/<project> .
docker push <username>/<project>
```
The next step is to create nginx image. The configuration file is inside /udacity-c3-deployment/docker:
```bash
docker build -t <your_dockerhub_username_lowercase>/reverseproxy .
```

For next steps I would suggest using minikube to setup local kubernetes cluster:
[https://kubernetes.io/docs/tasks/tools/install-minikube/](https://kubernetes.io/docs/tasks/tools/install-minikube/).

To setup the cluster use:
```bash
minikube start
```

Then apply configuration and secrets that are inside /udacity-c3-deployment/k8s:
```bash
kubectl apply -f env-configmap.yaml
kubectl apply -f env-secret.yaml
```
The next step is to apply deployments and services for each of the project and reverseproxy
```bash
kubectl apply -f <project>.yaml
kubectl apply -f <project>.yaml
```
After doing it, we should the application deployed and fully configured.