## README: Introduction to Containers, Docker, and IBM Cloud Container Registry Lab

### Objectives
In this lab, you will:
- Pull an image from Docker Hub
- Run an image as a container using Docker
- Build an image using a Dockerfile
- Push an image to IBM Cloud Container Registry

### Important Notes
- **Complete the lab in a single session** to avoid errors due to the lab environment going offline.
- If issues/errors occur, **log out from the lab environment**, clear your browser cache and cookies, and try again.
- You will be using an **IBM Cloud account** generated for the lab, not your personal IBM Cloud account.

### Prerequisites
Before starting, ensure that:
- Docker CLI is installed (`docker --version`)
- IBM Cloud CLI is installed (`ibmcloud version`)

### Steps

#### 1. Verify Environment and Command Line Tools
- Open a terminal window (`Terminal > New Terminal`).
- Verify that `docker` and `ibmcloud` CLI are installed by running the following commands:
  ```bash
  docker --version
  ibmcloud version
  ```

#### 2. Clone the Lab Repository
- Change to your project folder:
  ```bash
  cd /home/project
  ```
- Clone the Git repository if it doesn't already exist:
  ```bash
  [ ! -d 'CC201' ] && git clone https://github.com/ibm-developer-skills-network/CC201.git
  ```
- Change to the lab directory:
  ```bash
  cd CC201/labs/1_ContainersAndDocker/
  ```

#### 3. Pull an Image from Docker Hub and Run It as a Container
- List your images (this will show an empty table if no images are present):
  ```bash
  docker images
  ```
- Pull the `hello-world` image from Docker Hub:
  ```bash
  docker pull hello-world
  ```
- List images again to see the `hello-world` image:
  ```bash
  docker images
  ```
- Run the `hello-world` image as a container:
  ```bash
  docker run hello-world
  ```
- List all containers, including those that have exited:
  ```bash
  docker ps -a
  ```
- Remove the container using the `CONTAINER ID` from the previous output:
  ```bash
  docker container rm <container_id>
  ```
- Verify the container has been removed:
  ```bash
  docker ps -a
  ```

#### 4. Build an Image Using a Dockerfile
- Review the files needed for the Node.js app:
  - `app.js`: Main application, prints "Hello, World!" with the hostname.
  - `package.json`: Defines application dependencies.
  - `Dockerfile`: Instructions to build the image.

- Build the Docker image:
  ```bash
  docker build . -t myimage:v1
  ```
- List the images to see your newly created image:
  ```bash
  docker images
  ```

#### 5. Run the Built Image as a Container
- Run the image as a container:
  ```bash
  docker run -dp 8080:8080 myimage:v1
  ```
- Verify the app is running using `curl`:
  ```bash
  curl localhost:8080
  ```
- Stop the container:
  ```bash
  docker stop $(docker ps -q)
  ```
- Verify that the container has stopped:
  ```bash
  docker ps
  ```

#### 6. Push the Image to IBM Cloud Container Registry
- Verify the IBM Cloud account target:
  ```bash
  ibmcloud target
  ```
- List available namespaces:
  ```bash
  ibmcloud cr namespaces
  ```
- Set the appropriate region for your cloud account (e.g., `us-south`):
  ```bash
  ibmcloud cr region-set us-south
  ```
- Log into IBM Cloud Container Registry:
  ```bash
  ibmcloud cr login
  ```
- Export your namespace as an environment variable:
  ```bash
  export MY_NAMESPACE=sn-labs-$USERNAME
  ```
- Tag your image to prepare it for pushing to the IBM Cloud Container Registry:
  ```bash
  docker tag myimage:v1 us.icr.io/$MY_NAMESPACE/hello-world:1
  ```
- Push the image to the IBM Cloud Container Registry:
  ```bash
  docker push us.icr.io/$MY_NAMESPACE/hello-world:1
  ```
- Verify the image has been successfully pushed:
  ```bash
  ibmcloud cr images
  ```

Optionally, you can restrict the view to images within your namespace:
```bash
ibmcloud cr images --restrict $MY_NAMESPACE
```

### Congratulations!
You have successfully completed the lab, including:
- Pulling an image from Docker Hub
- Running a container
- Building and running a Docker image
- Pushing the image to IBM Cloud Container Registry

### License
© IBM Corporation. All rights reserved.

This lab is part of the **Introduction to Containers, Docker, and IBM Cloud Container Registry** course on CognitiveClass.ai.
