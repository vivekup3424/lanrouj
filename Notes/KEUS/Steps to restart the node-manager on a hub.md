1. From the keus-iot-platform repo
```bash
cd tools/platform-node-starter/prod
./esbuild.mjd
scp ../../../storage/node-manager/node-manager-1.0.0.tar.gz root@<hub-ip>:/data/keus-iot-platform
```

1. ssh into the hub
```bash
cd /data/keus-iot-platform
```


Steps to recreating error malfunction
1. Register a device
2. Add an appliance to device
3. create group
4. add both appliances to group
5. create local scene
6. add step to scene
7. delete group