# Jenkins · Docker image pipeline

A Jenkins pipeline builds a Python image and publishes it to Docker Hub.


```mermaid
flowchart LR
    N0["Build image"]
    N1["Log in to Docker Hub"]
    N2["Push build-number tag"]
    N3["Log out"]
    N0 --> N1 --> N2 --> N3
```


## Before running the pipeline

- Use a Jenkins agent with Docker available.
- Configure the Jenkins credential ID `dockerhub`.
- The Jenkinsfile publishes `fadi7ay/fadi_jenkins_docker22:<BUILD_NUMBER>`.

## Try the image locally

```bash
docker build -t jenkins-python-demo .
docker run --rm jenkins-python-demo
```

| File | Purpose |
| --- | --- |
| [Jenkinsfile](Jenkinsfile) | Build, login and push stages; logout runs afterward. |
| [Dockerfile](Dockerfile) | Python 3.9 slim image that runs app.py. |
| [app.py](app.py) | Container entry point. |
