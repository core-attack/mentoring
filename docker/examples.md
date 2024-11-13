```
docker build -t your_project-dev  --file src/YourProject/Dockerfile ./src/YourProject

docker run -d -p 5007:8080 your_project-dev
```