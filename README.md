# Aris OBC Zephyr project

## Requirements
To compile the code, Docker is required. I suggest using the [convenience script](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script) to install it:
```sh
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

## Setup
```sh
mkdir zephyrproject
cd zephyrproject
git clone git@github.com:sobkulir/aris-obc.git
cd aris-obc

# Build the docker image containing all Zephyr dependencies.
docker build -t zephyr .

# Run the image
docker run -it -v <zephyrproject>:/app zephyr
```

Now inside the container:
```sh
cd aris-obc
west init -l .
west update

# Build the application
west build -b qemu_cortex_m3 app
west build -t qemu_cortex_m3 app
```

The structure of Zephyr projects is a bit involved. For example there's a custom tool from Zephyr, `west`, for
managing multiple Git repositories in a single project.

## Extending
Project template is trimmed down version of the official [Example Application](https://github.com/zephyrproject-rtos/example-application). To add libraries or drivers, have a look there.
