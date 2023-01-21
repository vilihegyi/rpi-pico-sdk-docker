# Raspberry Pi Pico C/C++ SDK Docker

Docker container for the Raspberry Pi Pico C/C++ SDK.

# Install required packages

Ubuntu:
```
sudo apt-get install docker docker.io minicom
```

# Build and run the docker container from Dockerfile
```
docker build . --tag vilihegyi/rpi-pico-sdk:latest
docker run -d -it --name pico-sdk --mount type=bind,source=${PWD}/test_project,target=/home/dev vilihegyi/rpi-pico-sdk:latest
```

# Set up Visual Studio Code

Open Visual Studio Code, install the given extensions from `.vscode/extensions.json`. Once done, click on the bottom left corner and select the `Open Folder in Container...` option.

This opens up the application inside the container.

# Compile the sample application
In the Visual studio command run the following:

```
mkdir build
cd build
cmake .. -DPICO_BOARD=pico_w ..
make -j$(nproc)
```

Once done, we should have a `sample.uf2` file that is ready to copy on the RPi Pico W.

To copy the file, mount the RPi Pico W and run the following command from a Terminal that is open in the build folder (not from VS code):
```
cp ./sample.uf2 /media/$USER/RPI-RP2/
```

This will copy the file on to the development board and also do a reboot.

Now to connect to the output, we run the following in the Terminal:
```
sudo minicom -b 115200 -o -D /dev/ttyACM0
```

In case the above gives an error or empty output, please check the ports with the `ps -a` command.

Have fun and happy development!
