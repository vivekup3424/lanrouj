## 2025-04-06

## 2025-07-01
So there are some pointers to be noted down
1. The siteId can have a combination of older gateways (pi-3) and newer gateways (pi-5)
2. the difference between pi-3 and pi-5 is in terms of hardware, hence the underlying packages like glibc, mongo driver, nats-server can differ
3. in order to ssh into an older hub we have to ssh with named users for example in the case of skhub site, we have
	![](Pasted%20image%2020250701162918.png)|
	1. ssh keus@10.1.4.239
	2. password = gateway2021
4. the shield website only shows the pi-3 hubs for now

> [!ERROR]
> I still don't know how to differentiate between pi3 and pi5

5. In pi3, our services run as pm2 services
   ![](Pasted%20image%2020250701163817.png)
6. this older pi3 system corresponds to the older code, and is being used in lot of clients homes
7. In pi5, our services are being managed by podman(Docker without daemon), hence pm2 only has pm2-remote-api running
   ![](Pasted%20image%2020250701164055.png)
8. 