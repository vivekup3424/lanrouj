2024-10-14

BLE(Bluetooth low energy)

1. limited range
2. low power
3. low energy E > P

There are two types of power
1. Static Power (flowing thru system when it is idle)
2. Dynamic Power

Difference between Bluetooth and Bluetooth Low Energy
The main difference lies in what way of transmission is adopted
by either of the communication mediums,
> [!NOTE]
> BLE doesn't support data streaming

Bluetooth has a half duplex connection.

In case of a master and slave, the master is the central device 
connecting two various slaves, and the slaves have to be power 
efficient...

As soon as data arrives at the slaves end, the slaves wakeup
and receive packets from the master.

Bluetooth supports 79 data channels, with 1MHz channel between
and datarate approx of 1 million symbols per second

BLE supports 40 data channels, with 2MHz channel between
and datarate approx of 1 million symbols per second
with duty cycle requirement of 80microseconds.


### In the IOT system
controller -> physical layer + radio
Host -> upper layer installed

??System on Chip?? Search about what does this do??

## Low Power WAN
1. Narrowband IoT (low power communication)
2. devices supporting larger range
3. could've large number of devices
4. lower energy requirement
5. If I use SigFox, LoRaWAN
6. Date rate is from 0.3kbps to 50kbps, 
7. range is 2-5 kilometers

## SigFox:- 
This uses free sections of radio spectrum to transmit its data,
and instead of 4G network, SigFox focuses on using very long waves
thus the range can increase to a thousands of kilometers, and because of this
energy for transmission is significantly lower (less than 0.1% of contemporary
phone based networks)

It can only transmit 12bytes per message, and a device is limited to 140 messages
per day. Making it restrictive for the applications in which it could be used.

2024-10-21
Applications of IOT
so on and so forth, please read from the text material which
Saumya would provide