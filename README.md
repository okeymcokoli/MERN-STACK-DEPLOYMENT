## Dockerizing a MERN stack 3 tier application and deploying on K8s cluster. Then using Githubs actions and ArgoCD to automate updates and deployment of the manifests to the kubernetes cluster.


## Table of Contents
- [Dockerizing a MERN stack 3-tier application on K8s:](#dockerizing a MERN stack 3-tier application on K8s)
- [Table of Contents](#table-of-contents)
  - [Getting Started](#getting-started)
  - [Endpoints](#endpoints)
  - [Credits](#credits)
  - [Contributing](#contributing)


### Getting Started

1. Clone the repository:
   ```
   git clone https://github.com/okeymcokoli/MERN-STACK-DEPLOYMENT.git
   ```

2. Create a bridge network for the application.
   ```
   docker network create <network-name>

   ```
3. Deploy and test application locally.
    a. cd into mern/frontend folder and build the required images.

    ```
    cd mern/frontend
    docker build -t <image-name> . 
    ```

    b. Run below command to start the application and access it locally.
    ```
    docker run --name=frontend --network=<network-name> -d -p 5173:5173 <image-name>

    ```

    c. Verify that frontend is up and running. Copy and run below code on your browser.
    ```
    http://localhost:5173
    ```

    d. Start mongodb container and verify connection.
    ```
    docker run --network=demo --name mongodb -d -p 27017:27017 -v ~/opt/data:/data/db mongodb:latest
    ```
    ```
    http://localhost:27017
    ```
    e. Build backend.
    ```
    cd mern/backend
    docker build -t <image-name> .
    ```

    f. Run backend and verify accessibility.
    ```
    docker run --name=backend --network=demo -d -p 5050:5050 <image-name>
    ```

    h. Go to http://localhost:5173 and create, edit and delete entries to confirm successful deployment of your application locally

4. cd into K8s and update frontend, backend and mongodb folders to suit your needs.
   Ensure your cluster is configures and give the right privileges and run the following commands.

   ```
   kubectl apply -f ./frontend/frontend-deployment.yaml
   ```

   ```kubectl apply -f ./frontend/frontend-service.yaml
   ```

   ```
   kubectl apply -f ./mongodb/mongodb-deployment.yaml
   ```

   ```
   kubectl apply -f ./mongodb/mongodb-service.yaml
   ```
   
   ```
   kubectl apply -f ./mongodb/persistent-volume.yaml
   ```

   ```
   kubectl apply -f ./backend/deployment.yaml
   ```

   ```kubectl get all
   ```
   Verify all pods and svcs are deployed and running, access your application using the ClusterIP, NodePort or LoadBalancer

5. Optionally deploy using Helm folder provided as well or proceed to set up your Github Actions for your CI and ArgoCD for deploying your manifests.
   
6. set up your github workflows ci.yaml to suite your needs.
   
7. Push your changes to Github to trigger your CI workflow.

8. Ensure your cluster is connected on ArgoCD and verify the connection.
   
9.  Build your applications on the UI: frontend, mongodb and backend in that order and verify successful sync and healthy state of these applications.

10. Access your application frontend using your svc ClusterIP, NodePort or Loadbalancer.


### Credits
1. Big shoutout to Abhishek.Veeramalla whose insights and codes were curled for this project

### Contributing
Contributions are welcome! Feel free to open issues, submit pull requests, or provide suggestions to improve this project.