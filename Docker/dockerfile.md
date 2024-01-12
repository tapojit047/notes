# Dockerfile
- A Dockerfile is a text document that contains instructions for building a Docker image. It is a script-like file that specifies a set of commands and parameters to define the steps needed to create a Docker container image. Docker uses these instructions to automate the process of building an image, making it reproducible and shareable.
- A typical Dockerfile includes instructions to:
- Specify a Base Image: Use the FROM instruction to specify the base image on which your Docker image will be built. This base image provides the initial file system and environment for your application.
```dockerfile
FROM ubuntu:20.04
```
- 