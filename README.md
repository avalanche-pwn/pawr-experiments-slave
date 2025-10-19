# Slave module for PAwR related bachelor thesis

For now this is mostly  based on the [PAwR sample](https://github.com/zephyrproject-rtos/zephyr/tree/main/samples/bluetooth/periodic_sync_rsp)
located in zephyr repository.

You can also flash [pawr-experiments-master module](https://github.com/avalanche-pwn/pawr-experiments-master)
so that to which boards flashed with slave module can connect.

The master board will have turn on led1, while the slave boards will use led2.

Any code in this repository was tested on nRF54L15-dk board. It might
theoretically be possible to also run this on other boards from nRF54 family.

### Workspace initialization

In general unless you happen to have exactly the same ubuntu and library
versions as the nordic semiconductor developer who wrote the nordic sdk, you're
gonna have a hard time compiling this on your host distro. I recommend using
docker.

```shell
# Make workspace directory
mkdir workspace
cd workspace
# Enter docker container
sudo docker run -ti --privileged -v /dev:/dev -v $PWD:/workspace -e ACCEPT_JLINK_LICENSE=1 -e BOARD=nrf54l15dk/nrf54l15/cpuapp ghcr.io/nrfconnect/sdk-nrf-toolchain:v3.1.1  bash
# Note that the BOARD env variable is provided to make building easier.
# You can ommit it and later provide it to west build command via -b flag.
west init -m https://github.com/avalanche-pwn/pawr-experiments-slave.git pawr-experiments-slave
# update nRF Connect SDK modules
cd pawr-experiments-slave
west update
```

### Building and running

To build the application, run the following command:

```shell
cd pawr-experiments-slave
west build app
# By default $BOARD target will be used. You can override it with -b {board/name}
```

To flash the board use:
```shell
west flash
```
