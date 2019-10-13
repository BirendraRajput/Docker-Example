This tutorial teaches you how to build a Docker image that contains your .NET Core application. The image can be used to create containers for your local development environment, private cloud, or public cloud.

You'll learn to:

Create and publish a simple .NET Core app

Create and configure a Dockerfile for .NET Core


Build a Docker image


Create and run a Docker container


You'll understand the Docker container build and deploy tasks for a .NET Core application.


The Docker platform uses the Docker engine to quickly build and package apps as Docker images. 


These images are written in the Dockerfile format to be deployed and run in a layered container.


You need a .NET Core app that the Docker container will run. Open your terminal, 


create a working folder if you haven't already, and enter it. In the working folder,


run the following command to create a new project in a subdirectory named app:

//Create .NET Core app
>dotnet new console -o app -n myapp

//change dir
cd app

//Run
> dotnet run

//Publish .NET Core app
>dotnet publish -c Release

> dir bin\Release\netcoreapp2.2\publish

//Create the Dockerfile
//In your terminal, navigate up a directory to the working folder you created at the start. Create a file named Dockerfile 
//in your working folder and open it in a text editor. Add the following command as the first line of the file:
FROM mcr.microsoft.com/dotnet/core/runtime:2.2

//Notice that the two images share the same IMAGE ID value. The value is the same between both images because the 
//only command in the Dockerfile was to base the new image on an existing image. Let's add two commands to the Dockerfile. 
//Each command creates a new image layer with the final command representing the image the myimage repository will point to.

COPY app/bin/Release/netcoreapp2.2/publish/ app/

ENTRYPOINT ["dotnet", "app/myapp.dll"]


//build
docker build -t myimage -f Dockerfile .

//see list of images
docker images

//build again
docker build -t myimage -f Dockerfile .


//Create a container
docker create myimage

//List all containers
docker ps -a

//run
docker run -it --rm myimage

//Stop containers that are running
docker stop CONTAINER_NAME

//Delete the container
docker rm CONTAINER_NAME

//build again with username and tag
docker build -t birendrarajput/myimage:v1 -f Dockerfile .

//push with the following:
docker push birendrarajput/myimage:v1

//run again
docker run -it birendrarajput/myimage:v1





