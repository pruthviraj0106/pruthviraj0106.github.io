<!-- ---
layout: post
title: You're up and running!
---

my nafme is efsfoewi am from gandhinagar

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
 -->




---
layout: post
title: Docker 3 Tier Architecture Tutorial!
---

Hyy my name is  Pruthviraj and this is my blog post on docker 3 tier architecture

## Setting Up the Full Stack Project

To deploy a Three-Tier Application using Docker, the initial step involves setting up a Full Stack Project. While any Full Stack Project can be utilized for this purpose, if one isn’t available, an alternative project can be employed. In this instance, a straightforward project hosted on GitLab is utilized. The project, accessible via the link developing-with-docker, is constructed using HTML, CSS, JavaScript, Express, and MongoDB.

To commence, clone the Project Repository using the following command:

```bash
git clone https://gitlab.com/nanuchi/developing-with-docker




Creating a Network for Docker Containers
To run a Three Tier Application, we need to run three Docker Containers simultaneously. So, it is necessary to run all these containers inside a network to avoid their interaction with other containers.

So, Network can be created by using the following command after starting the Docker Engine with name mongo-network:

docker network create mongo-network

![_config.yml]({{ site.baseurl }}/images/2.png)

Pulling and Running MongoDB Image
To pull the MongoDB image from DockerHub and run it as a container, execute the following command:

docker run -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --network=mongo-network --name=21BCP295-mongodb -d mongo


![_config.yml]({{ site.baseurl }}/images/3.png)

Here, the mongo image will be automatically pulled from DockerHub to run the container in detachable mode with the name 21BCP295-mongodb in the network mongo-network. The container will be running on the default port 27017. You can check all the running containers using the command docker ps. Environment variables such as Username and Password are also passed to run the container. Similarly, we will be creating another container for Express by pulling its image from DockerHub.

Running Express Container
The Express Container can be run using the following command:

docker run -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=21BCP295-mongodb --network=mongo-network --name=21BCP295-express -d mongo-express

[_config.yml]({{ site.baseurl }}/images/44.png)

Here, the container with the name 21BCP295-express is configured to connect the MongoDB Database with the Frontend of the project in Docker. The container will run on port 8081. Environment variables such as Username and Password of the MongoDB are passed to access the Database, along with the container name of the MongoDB in the Server Environment variable. The container will be running on the same network as the previous container.


Accessing the Frontend and Creating Databases
Next, open the following link in your browser: localhost:8081, and proceed to create two databases named my-db and user-accounts.

It’s essential to create these two databases as they will be required by the Frontend during runtime. Additionally, make sure to update the MongoDB URL specified in the server.js file, as MongoDB will be running using Docker instead of on the Local Machine.

[_config.yml]({{ site.baseurl }}/images/55.png)

Updating MongoDB URLs in the server.js File
Navigate to the server.js file within the project directory. Replace the values of mongoUrlLocal and mongoUrlDocker with the following MongoDB URL:
[_config.yml]({{ site.baseurl }}/images/66.png)
This step ensures that the server connects to the MongoDB database correctly. It replaces the previous URLs with the Docker-specific URL, allowing seamless integration with the MongoDB container running in Docker.

