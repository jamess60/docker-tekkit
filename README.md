# James_S60 - Docker Tekkit 

## Intro

Whilst there are a couple of pre-existing Tekkit containers, they have lacked updates for many years and are themselves based on deprecated base images. This project provides a basic Tekkit server based on a modern day (and crucially still maintained) OpenJDK image. 

## How to deploy

1. Clone this repository to your docker host 

2. Create a directory to contain the Minecraft server data 

3. Extract the contents of tekkit.zip to the directory created in step 2

4. Add the following to your docker compose:

   ```yaml
    services:
   
        tekkit:
            container_name: tekkit
            image: jamess60/docker-tekkit:latest
            restart: unless-stopped
            volumes: 
                - /path/to/extracted/tekkit/zip:/tekkit
            ports:
                - "25565:25565"
            deploy:
                resources:
                    limits:
                        cpus: '2'
                        memory: 4G
   
   ```

   If you wish to change the port (or any other server settings), you can do so by editing the server.properties file and restarting the container. If changing the port, you need to update the ports section of the docker compose too. There are no environment variables for this container. You may mish to tweak the resource limits (CPU cores and ram limit) to your liking. Ensure the docker compose ram limit is AT LEAST 4GB. 



## Notes

- All this container really does is start "Tekkit.jar", so theoretically you could mount ANY modpack/minecraft server directory to /tekkit, rename the jar to Tekkit.jar and it should run. 
- Whats the motivation behind tekkit.zip? - Due to the way Minecraft generatively/dynamically spits out data and the way Docker handles volume mounts, its the simplest/easiest/most reliable way to handle a single editable dir. 
- Bugs or feature suggestions? - Please raise a git issue :) 
