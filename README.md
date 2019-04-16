# docker-all-the-things
This is the "Docker all the things" talk I did as a part of VS 2019 launch.  It walks through a simple single service web app, and expands to unit testing and multiple services in Kubernetes. 

There are a few key folders and projects included in the \src folder:
\pywebfrontend  -- ASP.NET Core web front end project w/ Dockerfile and Kubernetes/Helm charts
\pywebfrontend -- xUnit test console project w/ Dockerfile
\pywebapi -- ASP.NET Core web api project end project w/ Dockerfile and Kubernetes/Helm charts

Each project was created by simply doing a right-click -> Add Docker support, and then right-click -> Add Orchestration = Kubernetes/Helm


There are several modes and environments this can be run in using VS 2019 and Azure
1) Running directly as "native" services using IIS Express on your machine
2) Running as loosely coupled Docker containers inside the Docker Desktop environment on your machine
3) Running multiple orchestrated Docker containers inside Azure Kubernetes Service (AKS) leveraging Azure Dev Spaces
4) Running unit tests

"Native Service" mode (local)
1) Ensure that each project has a Run/Debug/F5 target using IIS Express
2) Set the service of interest as the startup project by right-clicking on project and Set as Startup Project
3) hit F5
4) Optional: in the solution properties set multiple projects to start with debugging.  This allows multiple loosely coupled services to
run inside IIS Express. Use IIS Manager or the project properties to learn the endpoints.  

Docker container mode (local)
1) Ensure that each project has a Run/Debug/F5 target using Docker
2) Set the service of interest as the startup project by right-clicking on project and Set as Startup Project
3) hit F5
4) Optional: in the solution properties set multiple projects to start with debugging.  This allows multiple loosely coupled services to
run inside Docker desktop.  Use 'docker ps' to learn the endpoints to each service.

Kubernetes & Dev Spaces mode (Azure)
1) Ensure that each project has a Run/Debug/F5 target using Azure Dev Spaces
2) Set the service of interest as the startup project by right-clicking on project and Set as Startup Project
3) hit F5
4) If Dev Spaces is not set up follow the dialog prompts to create a controller in your Dev Spaces cluster. 
4) Optional: in the solution properties set multiple projects to start with debugging.  This allows multiple loosely coupled services to
run inside Azure Dev Spaces

Unit testing
1) Right click on the .Tests project and set as start up project
2) F5 and observe Unit Test output in the Output window
3) Use the Test Explorer to Run all tests on demand
4) With any start up project, do a Release build and you will see the tests are running as a part of the Test stage in the Dockerfile
