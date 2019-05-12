# minecraft-bedrock
Run a bedrock server in a Docker container

This Dockerfile will download the Bedrock Server app and set it up, along with its dependencies.

If you run the container as is, the `worlds` directory will be created inside the container, which is unadvisable. It is highly recommended that you store your worlds outside the container using a mount. It is also likely that you will want to customize your `server.properties` file. The best way to do this is also using a `server.properties` file outside the container using a mount.

Here is a `docker run` command that will do that, assuming you have a `worlds` directory and `server.properties` file at `/minecraft`. (You should change the path to wherever your stuff is.)

    $ sudo docker run -d --name=minecraft\
        -v '/minecraft/worlds:/bedrock-server/worlds'\
        -v '/minecraft/server.properties:/bedrock-server/server.properties'\
        -v '/minecraft/permissions.json:/bedrock-server/permissions.json'\
        --network host\
        --restart=always\
        trancee/bedrock-server

If you wanted to use custom resource packs, a whitelist, or other things, you could also mount those paths as well. Separating the content from the sever executable means that you can safely destroy your Docker container without losing your world. This will come in handy when there are updates to the server app, and you want to redeploy the container.

Hopefully this is helpful to folks. Happy Minecrafting!

 -- nguyer
