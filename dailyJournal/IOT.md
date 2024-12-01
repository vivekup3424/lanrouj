2024-10-14

## BLE(Bluetooth low energy)
#### **What is BLE?**

- BLE, also called "Bluetooth Smart," is a wireless communication protocol developed by the Bluetooth Special Interest Group.
- It uses less energy and has a shorter range compared to traditional Bluetooth.

#### **How BLE Works:**

- BLE is divided into two main parts:
    - **Controller**: Handles physical and link-layer tasks (implemented in a System on Chip (SoC) with a radio).
    - **Host**: Manages the upper communication layers.
- BLE is **not compatible** with classic Bluetooth due to design differences.

#### **Differences Between BLE and Classic Bluetooth:**

1. **Data Streaming**:
    
    - Classic Bluetooth supports continuous data streaming.
    - BLE transfers **small packets** of data quickly (packet size is small, and speed is 1 Mbps).
2. **Connection Behavior**:
    
    - Classic Bluetooth stays **always connected**, even when idle.
    - BLE devices save energy by being in **sleep mode** and waking up only when needed to communicate.
3. **Device Types**:
    
    - BLE uses a **master-slave model**:
        - **Master**: Central device (e.g., a phone or PC).
        - **Slave**: Peripheral devices (e.g., fitness trackers, thermostats, or smartwatches) designed to be **power-efficient**.
4. **Channels and Bandwidth**:
    
    - Classic Bluetooth: **79 data channels** with a **1 MHz channel bandwidth**.
    - BLE: **40 data channels** with a **2 MHz channel bandwidth** (wider channels for faster transfers).
5. **Transmission Time**:
    
    - BLE can send the smallest packet in just **80 microseconds** (very fast compared to classic Bluetooth).
6. **Energy Efficiency**:
    
    - BLE supports low-duty cycles (devices are idle most of the time, waking up only briefly).
    - BLE is 2.5x more energy-efficient than competing protocols like Zigbee (transfers more data per unit of energy).
7. **IP Support**:
    
    - BLE supports communication over the Internet Protocol (IP), making it suitable for IoT applications.

#### **Example Use Case**:

- A smartphone (**master**) connects to a fitness tracker (**slave**).
- The tracker stays in **sleep mode** to save power and wakes up periodically to send data like heart rate or steps.

#### **Summary**:

- BLE is ideal for low-energy, low-bandwidth, and intermittent data transfers, making it widely used in IoT devices like fitness trackers, smartwatches, and home automation systems.
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
> The energy efficiency of _BLE is 2.5 times better than Zigbee_.

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

## OneM2M
OneM2M is an international standard for **Machine-to-Machine (M2M) communication** and the **Internet of Things (IoT)**. It provides a framework for enabling devices, networks, and applications to interoperate, regardless of manufacturer or platform, by defining a common architecture and set of protocols.

### Key Concepts of OneM2M

1. **Purpose**:
    
    - To create a common service layer that can be embedded in various hardware and software to enable seamless interoperability among IoT devices.
    - To ensure scalability, security, and interoperability in M2M and IoT deployments.
2. **Architecture**:
    
    - OneM2M defines a **Service Layer** that sits between the underlying communication networks and IoT applications. This layer provides common functionalities required for IoT operations.
3. **Components**:
    
    - **Application Entity (AE)**: Represents the application logic running on IoT devices or cloud systems (e.g., a temperature sensor application).
    - **Common Services Entity (CSE)**: Provides reusable IoT services such as data storage, device discovery, subscription, and notification.
    - **Network Services Entity (NSE)**: Interfaces with communication networks to provide connectivity for devices.
4. **Resources**:
    
    - OneM2M organizes data as a hierarchical structure of **resources** (e.g., sensors, applications). Each resource has a unique identifier and attributes that store information about its state or capabilities.
    - Examples of resources include containers (for data storage), contentInstances (actual data), and subscriptions (to receive notifications).
5. **Protocols**:
    
    - OneM2M is protocol-agnostic but supports various communication protocols like **HTTP**, **CoAP**, **MQTT**, and **WebSockets** for communication between devices, gateways, and servers.
6. **Domains of Application**:
    
    - Smart cities (e.g., street lighting, waste management)
    - Smart homes and buildings (e.g., HVAC systems, security)
    - Industrial IoT (e.g., manufacturing, logistics)
    - Healthcare (e.g., remote monitoring, wearable devices)

---

### How OneM2M Works

1. **Registration**:
    
    - Devices (or AEs) register with a **CSE**, which acts as the central hub for managing resources.
2. **Data Exchange**:
    
    - Applications (AEs) communicate via the CSE using standardized resource-based APIs. Data can be stored, retrieved, or updated.
3. **Subscriptions and Notifications**:
    
    - Applications can subscribe to specific events or data changes, and the CSE sends notifications when those events occur.
4. **Security**:
    
    - Includes mechanisms for authentication, authorization, and secure data transmission.

---

### Example: Smart Home with OneM2M

- **Setup**:
    - A smart home consists of sensors (temperature, motion), actuators (lights, thermostat), and a cloud server for managing these devices.
- **Flow**:
    1. Sensors and actuators register as AEs with the CSE.
    2. The CSE provides discovery services for finding available devices.
    3. Applications can subscribe to changes in sensor data (e.g., temperature updates).
    4. When a temperature threshold is exceeded, the CSE triggers an actuator (e.g., turning on a fan).

---

### Advantages of OneM2M

- **Interoperability**: Supports multiple devices and communication technologies.
- **Scalability**: Can handle a large number of devices in distributed environments.
- **Standardization**: Provides a common framework, reducing vendor lock-in.
- **Flexibility**: Supports a wide range of applications across industries.

By using OneM2M, IoT ecosystems can achieve unified and efficient communication, making it easier to deploy and scale solutions across various domains.

## Access Control Policies in OneM2M
**oneM2M resource type** _`<accessControlPolicy>`
## What are the access control policies in oneM2M?
```markdown

oneM2M defines <accessControlPolicy>  resource for defining and managing access control for oneM2M resources. These policies can be created under <CSEBase>,  <AE> , <remoteCSE> resources. These policies, when linked to a resource, are used for making access decision for that resource.
```

These policies contain _Access Control Rules_ which define

- **who** (via the attribute _accessControlOriginators_ or _acor_) is authorized to access the resources,
- **what** operations (via the attribute _accessControlOperations_ or _acop_) are allowed on resources, for example CREATE, RETRIEVE, DISCOVER,
- what attributes of resources can be accessed (via the _accessControlAttributes_ or _aca_), and
- under **which** conditions (via the attribute _accessControlContexts_ or _acco_) access is allowed for operating on oneM2M resources, for example for time, location, IP address, and limits.
### Privileges
Each _Access Control Rule_ contain _privileges_ and _selfPrivileges_ attributes as depicted in the figure below (for simplicity only who and what is shown):

[![AccessControlPolicies-Privileges and selfPrivileges](https://recipes.onem2m.org/basics/images/oneM2M-ACP-priv-selfPriv.png)
Figure 1: AccessControlPolicies-Privileges and selfPrivileges

#### Privileges
- **privileges** in an `<accessControlPolicy>` resource define the _Access Control Rules_ for resources other than **accessControlPolicy** resource.
#### Self privileges 
- **selfPrivileges** in an `<accessControlPolicy>` resource define the _Access Control Rules_ for the `<accessControlPolicy>` resource itself.
- This is normally used for protection from unauthorized modification of the access control policy.
- modification of access control policy has been prevented here

### Access Control Policy linking

`<accessControlPolicy>` resources can be linked to other oneM2M resources using the _accessControlPolicyIDs_ (ACPI) attribute in those other resources. This is depicted in figure below:

[![Resource linking with Access Control Policy](https://recipes.onem2m.org/basics/images/oneM2M-ACP-linking.png)](https://recipes.onem2m.org/basics/images/oneM2M-ACP-linking.png)

Figure 2: Resource linking with Access Control Policy

## Access Control Policy checks

How access control policies are checked is depicted in the figure below:

[![Access Control Policy check](https://recipes.onem2m.org/basics/images/oneM2M-ACP.png)](https://recipes.onem2m.org/basics/images/oneM2M-ACP.png)

Figure 3: Access Control Policy check

When a request to a resource is sent then the following sequence occurs at the CSE:

1. Get the ACPI attribute associated with the targeted resource.
2. Find the `<accessControlPolicy>` (ACP) resource(s) corresponding to this ACPI attribute.
3. Check if the originator is present in the _accessControlOriginators_ of any of _Access Control Ruls_ (ACR) in the ACP resource(s).
4. Check if the request operation is present in the _accessControlOperations_ of the ACR.
5. When both the conditions are matched then access to the resource is granted to the originator and for the operation requested.
6. When any of the conditions do not matched then resource access is not granted to the originator, and an error response is given to the originator with status code "4103 (ORIGINATOR_HAS_NO_PRIVILEGE)".

![[Pasted image 20241113103231.png]]
- The check is applied at the receiver's end and is verified in access control originator's list in the ACP resource
- the access control R at the ACP includes all the resources rules corresponding to which checks are applied.
- when any of the conditions do not match then resources is not granted to the originator and an error is given to the originaot with the status code 4103. i.e. originator_has_no_previlege

## Ocean (Open Connectivity for IOT)

![[Pasted image 20241128184650.png]]
This slide explains **OCEAN from KETI**, a platform providing open-source tools and implementations for the OneM2M standard. Let me simplify it for you:

---

### **Key Highlights**

1. **What is OCEAN?**
    
    - OCEAN (Open Connectivity for IoT) is an initiative by KETI (Korea Electronics Technology Institute) to offer open-source software for building IoT systems using the **OneM2M standard**.
    - It provides tools to help developers create servers, gateways, and device platforms that follow OneM2M protocols.
2. **Mobius Server Platform**:
    
    - Mobius is an **open-source server platform** built for OneM2M.
    - It is **commercialized and certified**, meaning it meets official standards for deployment in real-world systems.
    - Mobius allows different devices (both OneM2M and non-OneM2M) to connect and interact with IoT applications.
3. **Tools Provided by OCEAN**:
    
    - **OneM2M Resource Browser**: A tool to explore and manage OneM2M resources (like sensors, devices, or data).
    - **Conformance Testing Tool**: A tool to test if your IoT solutions meet OneM2M standards.
4. **Licensing**:
    
    - The platform uses the **BSD 3-Clause License**, which is a permissive open-source license. It allows redistribution and use in both **source** and **binary forms**, even for commercial purposes, with minimal restrictions.
5. **Integration with IoT Devices and Applications**:
    
    - The system supports both **OneM2M-compatible devices** and devices using other protocols, ensuring flexibility.
    - It helps IoT developers integrate various devices, applications, and backend systems across different domains.
6. **Where to Access**:
    
    - Developers can access tools, resources, and documentation from the OCEAN website: [http://developers.iotocean.org](http://developers.iotocean.org).

---

### **Simplified Example**

Imagine you are building a smart home system:

- **Devices**: Your home has sensors (temperature, light, etc.) and actuators (fans, smart lights, etc.).
- **Problem**: Some devices follow OneM2M standards, while others use older or different protocols.
- **Solution**: Mobius acts as a central platform where all devices can connect and interact. It translates different device languages into a unified format, so your smart home app works seamlessly.

---

### **Why is This Important?**

- It provides **free tools** to help developers work with IoT systems.
- It ensures compatibility between devices from different manufacturers.
- It simplifies building scalable and interoperable IoT solutions.

Would you like to dive deeper into any specific part?
## Smart City
### What is Smart Transport in Cities?

Smart transport refers to the integration of advanced technologies like sensors, data analysis, and intelligent systems to improve transportation systems. It focuses on reducing traffic congestion, enhancing safety, and offering more efficient and accessible travel options.

---

### **Key Features of Smart Transport with Examples:**

#### **1. Reducing Traffic Congestion**

- **How It Works**: Uses tools like GPS, accelerometers, and cameras to monitor real-time traffic patterns.
- **Example**:
    - Google Maps collects real-time data from users' smartphones to show congestion and suggest alternate routes.
    - Cities implement AI-driven traffic systems that predict and manage congestion by diverting vehicles.
- **Impact**: Minimizes commute times, reduces fuel consumption, and improves road efficiency.

#### **2. Ensuring Safer Driving**

- **How It Works**: Sensors track driver behavior, detecting fatigue, distraction, or reckless driving. Systems provide alerts or recommendations for safer practices.
- **Example**:
    - Cars equipped with fatigue detection systems, such as Tesla, monitor drivers' eye movements and trigger alerts when signs of drowsiness are detected.
    - Usage-based insurance apps track driving behavior and incentivize safer habits with lower premiums.
- **Impact**: Reduces accident risks and promotes responsible driving.

#### **3. Smart Parking**

- **How It Works**: Parking spaces equipped with IoT sensors detect whether they are occupied or free. Users access parking availability via apps or dashboards.
- **Example**:
    - A driver uses an app like **ParkMobile** to find and reserve a parking spot in real time.
    - Sensors in mall parking lots indicate vacant spots with LED lights (green for available, red for occupied).
- **Impact**: Saves time and reduces the frustration of searching for parking spaces, improving urban traffic flow.

#### **4. Smart Traffic Lights**

- **How It Works**: Traffic signals adapt to real-time conditions using AI and IoT. They prioritize vehicles such as ambulances or buses during emergencies.
- **Example**:
    - Smart signals in cities like Singapore adjust green light timings based on the density of vehicles detected by cameras and sensors.
    - During emergencies, connected systems give ambulances a "green corridor" to reach hospitals faster.
- **Impact**: Reduces waiting times at intersections and improves emergency response times.

#### **5. Accident Detection**

- **How It Works**: Apps or vehicles use accelerometer data to detect sudden impacts, combined with sound recognition to identify accidents. Systems automatically notify emergency services with location and details.
- **Example**:
    - An app like **Life360** or in-built systems in cars like OnStar send crash alerts to first responders with GPS coordinates and severity metrics.
    - Smartphones detect crashes using gyroscope sensors and trigger automated SOS calls.
- **Impact**: Speeds up emergency response, potentially saving lives.

---

### **Practical Benefits of Smart Transport**

- **Environmental Impact**: Reduced fuel wastage and emissions due to optimized traffic flow.
- **Cost Efficiency**: Savings in fuel, insurance premiums, and time for users.
- **Safety Improvements**: Fewer accidents due to real-time monitoring and emergency responsiveness.
- **Urban Planning**: Data-driven insights for better infrastructure planning and resource allocation.

By combining these systems, cities aim to create a sustainable, efficient, and safer transport environment.