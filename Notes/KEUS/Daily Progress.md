## 2025-01-29
Today I am learning about Docker Networking and alongside I am also going to prepare notes on Docker in my Obsidian system.
After reading some parts about Docker Network, I installed Neo4j on my ubuntu wsl and I am planning on learning more about them later on.

For now I have been given the task of understanding the clean architecture code of platform agent by Akhil and recommend if there are any changes necessary

Here is how I will do this
	1. Read about [[Clean Code Architecture]]

## 2025-02-11
1. Complete the workflow diagram of Rules Engine Service, add examples on it
2. Write some code to checkout into some branch of keus-iot-platform and get all the plugins with their directory name from it.
3. For the above requirement, I need to write a bash script to list out all the remote branch names, get some branch name in input, checkout into that branch and then list all directories of that branch.
4. I have also created a demo ui for this
## 2025-02-13
1. Today I will think of edge cases in rules execution of rules engine, and the case of circular dependency.
2. Presented the workflow of Rules Engine along with its database presentation to Akhil and Ashwik
3. Now I have to think of good terms for defining different things in Rules Engine.
Query = 
`I have a rules engine which monitor for state of some devices (like for TV their play state (playing or paused), volume state (0-100),  These states would be responsible creating conditions for rule execution (to determine whether a rule, need to be executed or not), (What should be call these states in json-rules-engine they are called facts, in ui terms they are called starters or triggers because they are responsible for starting of execution of some rule), now I have a set of Routines, each rountine contains some set of things / actions that it needs to do, then there would a delay, then we will go the another rountine in the set I have decided on this below diagram for the execution, but writing the last step as trigger makes it more confusing as triggers should be the begining of flow execution because it triggers something Please help me containing some correct inituitive name  (PS :- I can't use actioon because we are using Moleculer, hence methods of services are called action, hence this can make the whole thing more confusing.)
`

## 2025-02-17
1. reading the source code of json-rules-engine in order to fully levarage it, and see wherever I can optimise my own rules engine service using this.
2. For now I have understood about Facts, things required when creating a new instance of them, and how the fact's value is calculated at runtime
3. I read a little bit about Almanac, but I still haven't understood about how can I make use of this for our own convenience.
4. In our case the valueOrMethod passed into the Fact constructor would the action of the service responsible for getting the present value of the fact using the params as the  context, now how do I pass this params as context that I need to think about.
## 2025-02-21
Today I am gonna present the demo for the rules-engine, along with three working automations.

The demo was good, now I need to sit with Akhil and Rohit and decide upon milestones about how to make this plugin go faster in production.
I atleast want this plugin to go in production before my internship is over.


## 2025-02-25
- Designed and coded to implmentation to avoid execution of circular loops in rules-engine

## 2025-02-27
- Today's I am only gonna work on handling success and failures in moleculer channels, 
- and how to custom options in each moleculer channels

## 2025-03-21
- I am back at this thing, after such a long time
- Tired of typing

## 2025-04-09
- I have written the code to move mongodb outside of dev-container
- Need to work on that PR for fact_task_in_manifest, need to create a validator for the manifest
	- For now waiting for Sai to finalise the manifest
	- After that change the naming of some function and add extensive verbose error handling-
- For now let's work on the adding the functionality of stop-node in the dev-container itself, so that when the dev-container, stop-node also get's triggered

## 2025-04-10
- test the run plugin of hydra cli

## 2025-04-22

> [!TODO]
> - [x] Setup the keus-iot-gateway repo
> - [ ] Code review for dev-gateway-restructure
> - [ ] Understand how the notifications work currently on the gateway side
> - [ ] Understand how code and how to work in branch `feat/device-and-appliance-flows`

> [!Done]
> - Saw the video of Balaji explaining the code and workflow

2025-05-06
- the older approach of installing plugin in dev was checking for both backend and service like this 
```ts
                let location = `${pluginInfo.installLocation}/${['service', 'backend'].find(
                    f => fs.existsSync(`${pluginInfo.installLocation}/${f}`)
                )}/`;
                let pluginImports = await import(`${location}`);
```

I think I can make use of something like this in manifest_refactoring branch


## 2025-05-22
1. Need to take KT for cameras-plugin
2. Optimise the camera's motion detection and recording to reduce 5%
3. write a function to have the recording do object recognition
4. test the system on "ssh keus@10.1.4.148  "
	1. with password - keus123
5. clean up the logs (no error logs, no log from ffmpeg ,opencv.... )
	1. no logs on terminal from other sources except the print statements which I write
6. reduce the cpu, as much as possible keeping accuracy of recordings and motion detection high enough
7. reduce the length of video recording at the end to 2 seconds when no motion detected
8. divide the recoding video into chunks of 1 minutes
9. store the recordings such that if motion is detected from time t to s,
	1. then recording file should contain video from t-5 to s+5 seconds
10. keep the accuracy high, but cpu consumption extremly low
11. as plugin
	1. addCamera //add the data of camera  and start monitoring with my plugin
	2. deleteCamera //remove the recordings for that ca+
	3. getDetectio(cameraId[ ])
	4. store the data for camera in mongodb
	5. data of camera contains :-
		1. CameraId,
		2. rtsp URI
	6. Requirements :-

## 2025-05-26
1. Today I am going to finish coding the motion-detection service, everything is work fine here with max use of 4% cpu
2. Next tommorow I design the api server, and then I will write the plugin tommorrow itself.
## 2025-05-27
1. make the code modular
2. make other variables like min_area, threshold, skip_frames as constant, but take the fps from camera source
3. expose the functionality as an api with 
   localhost, port - 8083
	1. addCamera(camera-id, rtsp-url) - starts monitoring and saves the recording
	2. deleteCamera(camera-id) - stops the monitoring
4. make the python program multithreaded with different thread responsible for monitoring of different cameras
5. make a thread responsible for cleanup jobs to remove recording directories older than three days
6. save the recording in different directory for each camera, each recording saved into a respective directory name after the date on which the recording takes place
7. the motion detection is working fine, but the recordings are breaking when I play them, so my requirements are
8. use the prebuffer from opencv to add the footage of 5 seconds before the ffmpeg recording starts
9. save the recording with ffmpeg cli command with suitable codec to preserve video and audio
10. after motion stops and no motion is detected again for 5 seconds stop the recording
11. store the recordings in form of chunks of 60 seconds each
12. since opencv prebuffer frames don't have any audio, then you think about it how to concat
   opencv prebuffer video + ffmpeg recording containing audio

## 2025-05-30
### 1. Why the heck are we doing gateway rework?
- performance (everything was going into one system) - (every service was running on same system)
- developer ease (adding new devices into the gateway code was hacky) (we are building the solution from bottom-up by creating an sdk)
- missing featues in gateway code
- so there was an urgent requirements of finishing up the placeholder functionality in taskflow, I am making ai code for now,
	- this is a very bad habit I've developed

## 2025-06-02
#### Taskflow Placeholder Resolver
- the taskflow placeholder design has changed now
- we are using {{stageName}}, {{stageName.taskName}}, {{stageName.taskName.property}}, {{stageName.taskName.property.subproperty.subsubproper...}} for using placeholders
- stageName, taskName, propertyNames can only be containing a to z, A to Z, 0-9, _


## 2025-06-04
### NVR Plugin
- Wrote the clean code architecture for the motion-detection plugin, have not tested it, will do it soon
- Now I am quite dissatisfied with code wriiten by vscode-agent (sonnect 4.0) for the rasa chatbot for smart home automation
	- hence I will try to read the documentation of rasa myself, and code it out myself
	- my most important problem that arose from using vscode agent
	- was that generated rasa bot was not functioning well, and it was also not doing any conversations
	- so I will try to start writing the code again step-by-step (with smaller example creating conversational-ai)

## 2025-06-11
### Common modules removal for inter and intra plugin builds
1. Working on common modules, thinking about way to reduce the bundle size of plugins by placing their common modules in a common dependency
2. Need to test whether this approach is working on different plugins, and for different hubs.

## 2025-06-30
1. Today I am working on creating a authorization service with
   ![](Pasted%20image%2020250630173153.png)

this is very similar to the way AWS is creating IAM.
need to update my resume with these details.

## 2025-07-10
- [x] read about "reading logs from fluentbit"
- [x] read about filtering logs from fluentd
- [x] send http messages for these filtered logs
- [x] get the demo for tomorrow working


## 2025-07-11
- [ ] load test the data consumption pipeline from fluentbits instances to fluentd
- [ ] read more about integrating google assistant and rasa bot
There is a log collection pipeline from fluentbit instances to fluentd instance
I want to load test what happens inside the fluentd instance
For this I am going to use docker compose

***I am taking a detour and exploring the google assistant integration with rasa*** 
https://rasa.com/blog/going-beyond-hey-google-building-a-rasa-powered-google-assistant/
for this  ==*Actions On Google*== (*console.actions.google.com*) is a useful resource

They are telling me to use ngrok for some reason, I don't know what this is

- [ ] *this ngrok utility sounds very useful, need to learn more about this*

## Learning of today's research
1. Google was exposing conversational actions on "Actions on Google" console. there was a tutorial in rasa 
	showcasing this, but this has been deprecated so we can not use those steps
	![[Pasted image 20250711162146.png|600]]
	
	https://developers.google.com/assistant/ca-sunset
	https://developers.google.com/assistant/ca-sunset/faq
	
	![[Pasted image 20250711162501.png|600]] 

2. We can create custom connectors for assistant like google assistant 
	1. these connectors will act like webhook
	2. but if assistant themselves can't call these webhooks the they are of no use.
3. The next alternative was Google Developer Console
	1. But these are coupled with Google Home Devices
	2. They are trying to build on device layer
	![[Pasted image 20250711164026.png|600]]



Systemctl is used to start platform-agent

## 2025-07-15
Tasks for today are
1. systemctl 
2. pm2 
3. podman 
4Pheonix runs the new platform on Pi5 and custom Yokto based OS 
- Also called media hub by few people Raspbian runs monolith on Pi3 with raspbian OS 
- also called gateway in general Platform Agent Usecases: Phoenix Usecases: - 
	- os update Raspbian Usecases: - migrate database from monolith to plugin architecture
	- switch between old and new deployments Common Usecases: - health check and restart baseline services 
	- deploy & start baseline services 
	- deploy and manage logs agent 
	- deploy and manage nats 
	- self Update 
	- node metrics 
	- backups 

1] Deploy and manage logs agent - Vivek 
- understand the flow 
- create flow diagram 
- first time bootup 
- installation 
- update 
- health check and ressuruction

## 2025-07-29
1. Picking up a new project today
2. cleanup the workspace yml
3. understand the difference between lib, package and tool
4. assets, are we using them ??
5. repo clean >> dev experience

Read about timeseries database of mongodb
themattman/mongodb-timeseries

## 2025-07-31
- [x] Need to see what NatsLeafConfigManager is doing  in node-manager/server/src what we need to change there


## 2025-08-04
I will need to read more about
```typescript
    private static async startMolecularNatsGateway(broker: Moleculer.ServiceBroker, nodeConfig: INode) {
        await broker.call('molecular_nats_gateway.ConfigureGateway', {
            host: CoreConstants.nats.serverHost,
            port: CoreConstants.nats.serverPort,
            token: CoreConstants.nats.token
        });
        await broker.call('molecular_nats_gateway.StartProvider', {
            rpcEndpoint: `${nodeConfig.siteId}-${nodeConfig.nodeId}`
        });
        await broker.call('molecular_nats_gateway.StartProvider', {
            rpcEndpoint: `${nodeConfig.siteId}-KIOTP`
        });
    }
```
inside the start after-registration-flow.ts, and see what this one is doing

1. revert the nats config file to use the nats.manager.conf file, and in the case of 
2. site-manager is not able to sync nodes that are disconnected, it is not able to remove it, also remove services from worker node is not getting synced with the site-manager database


## 2025-08-20
1. Work on making node-manager stable in the node_manager_stable branch
2. Need to focus on install plugin using taskflow async jobs, with states()
3. States = downloading_source,downloading_image, installing, installed
4. For plugin uninstall remove image, delete downloads, uninstalll with states
5. plugin update - (current uninstall plugin then install plugin)
	1. alternative way 
	2. after plugin install, remove artifacts (tar files)
6. Node_Configuration.Add_Service with states, and these states would be visible in node collection using event listener then update node collection
7. Actions like install uninstall plugins should emit events for respective states of exection(emit events on NatsRealTime)
	1. Add 4 tasks like download artifact, install plugin, update nodedb, sync node with site manager (add more tasks if required)
8. after registration flow cleanup
9. Discuss with Akhil about better pm2 setup for interservices and interplugins, basically better flow for pi3
10. Remove plugin_core_ui , plugin_ui_service.ts from container.
11. libs/utilities, kiotp-realtime-js, moleculer-nats-gateway  packages/types => change the entry point with typescript files (read their package.json)
	1. for reference read the package.json of hydra/core

2025-08-21
1. Add environment filed in node registration body
2. three nats serverhost ips based on the environment, create a new nats.ts file for moleculer_nats_gateway, and load up remote's url based on the environment (production, developement, or staging)
3. remove the code fo making common modules from esbuild, since it only build node-manager
4. add a node-path pointing to new common modules during start.mjs of node-manager
5. replace `NODE_PATH=/keus-iot-platform/common_modules/node_modules node ./index.js`
6. with NODE_PATH=/keus-iot-platform/common-modules/node_modules node ./index.js
7. Vdbuilding common


## 2025-08-22
1. Create template will be done by shield (so assume that templates for hubs are already created)
2. Get template
3. Install template all in hub-setup.js

Some more KT for the next week

## 2025-09-19
19th September 2025
KT for elasticsearch
1. Elasticsearch uses lucene


## 2025-09-22
1. how to attach a microphone on a raspberry pi 5?
2. I am testing my voice agent on raspberry pi 5, I am learning about everything how to install drivers on linux without package installer
3. `lsusb` is used to get the list of devices attached to the motherboard


## 2025-09-23
runMigrationFlow(older mongodb uri)

## 2025-09-29
Tasks
 - [x] conditionally stop old services only zigbee ones, and start new ones
	 - [x] what those services
 - [x] what are the cases we need to handle during migration for main amd mini hub
 - [x] how much delay is acceptable during migration of main hub and mini hub

## 2025-10-03
1. For the gateway migration,
2. Written the code to cleanup the zigbee chip in the step3 (infosync)
3. Merged the PR of zigbee-migration changes into dev_gateway_restructure

## 2025-10-06
Things we have done to make the gateway-migration work
1. installing sshpass in developer's laptop
2. Adding ip to known_hosts for sshpass to work
3. When building node-manager, if podman-remote-api is not build beforehand its throwing error
	1. In the node-manager's source code, wherever we are importing podman-remote-api from deploy subdirectory, I've replaced it with src subdirectory
	2. so we don't need to compil e the typescript files in src to generate the deploy subdirectory
4. Also in node-manager, in the taskflow service's taskflow-manager was throwing typescript error in emitEvent
	1. it was expecting taskflowId in this params, but that was not garuanteed , no it replaced the emitEvent function signature
	2. in the kiotp-realtime-js source code, I replaced the 
		1. `let bucketLister: Lister<KvStatus> = kvManager?.list();`
		2. with `let bucketLister: Lister<KvStatus> = kvManager!.list();`
		3. since it was throwing typescript error

>[!TODO]
> multinode is working correctly in mini, the services are not getting installed
> also plugin is also not getting installed

When I checked the leafnode connection in manager's nats, it is alright, the mini is getting connected as a leaf-node

WipeZNP
1. Its taking 

## 2025-10-07
1. Add a trycatch in getNodeConfig of node-configuration, also added the isWorkerNode flag in responses of this handler
2. Changing the ISiteNodeInfo interface to include  isWorkerNode and managerIp field
3. Merged the PR for above code in dev_gateway_restructure branch

## 2025-10-08
1. Working on a poc to have inbox working in util from hydra-core directly

## 2025-10-09
1. Tested the cleverrap push notification on iOS tablet keus app, we are able to send custom images and sounds for notifications
2. Tested the shield api for sending notification with android and iOS app, we are able to send notifications to multiple devices at once using the shield api

#### Observations on push notification on iOS via Clevertap
1. When tablet falls below 10% battery, the tablet gets into battery saver modes, then all the notifications get throttled hence we might on these notifications
2. Sometimes when we send a push notification request to clevertap api, it might return a `dispatch failed` error (this is observered when sending notifications directly from clevertap dashboard)
3. There are too many motion detection notifications coming to the tablet, like 2-3 notification per second
	1. We can have a internal settings for notifications, so that users can select to which kind of notitications to receive

## 2025-10-15
1. Merged the PR for these below todos of event-buffer service
	1. implement service schema using service ids from node manager constants
	2. named "default.bufferService.dead.queue" as the dead letter queue for event buffer service
	3. add expiry for events in event-buffer service
2.  Working on load testing the Pi3-Raspian OS with new platform and older platform running together, will continue this tommorrow

## 2025-10-16
1. Identify the bug in plugin installation where on installing plugin, it was getting installed in either worker node or manager node
2. Fixed this bug, and I will raise a PR for this tomorrow
3. Published all devices to shield, will start load testing tomorrow
4. I am able to install device on hub either from template or by mentioning plugin-id in shield

## 2025-10-17
Curretly noting down information on Skhub-main for Pi3 Load test
When nothing new is added, and the hub is functioning normally
![[Pasted image 20251017122129.png]]

1. On average when the older gateway is running, the idle cpu usage is 13% 
2. memory usage is 680 MB our of 970MB, 
3. and its also swap usage is 366 MB out of 1024 MB
Two process that most intensive this time is hub_request_manager and device_manager
Tailscaled also sometimes use 17% cpu usage

### After starting the new platform along with the older platform
Simple commands like `pm2 ls` take 5 seconds to respond on pi3
1. The cpu usage has increased to 25% on average in all the four cores
2. Memory is still averaging around 680 MB our of 970 MB total
3. Swap has increased to 920 MB out of 1024 MB
While idling
![[Pasted image 20251017141708.png]]

Hub-Request Manager = 9% CPU and 14% Memory
Node Manager = 2.7% and 3.6 % memory
Mongodb in crun is using 5.0% CPU

![[Pasted image 20251017142345.png]]
#### Some errors encountered while installing plugins

1. ```json
   23|kiotp_node_manager_server  | [2025-10-17T07:39:13.220Z] WARN  manager/BROKER: Request 'v1.plugin_core.savePluginToDatabase' is timed out. { requestID: '79c694cb-5588-400b-8a69-7a456cbd44f8', nodeID: 'manager_plugin_core_1', timeout: 30000 }    
   ```
This error is intermittent, since it is due to timeout, retrying to install the plugin fixes this issue.

*While installing plugin, the cpu increases to avg of 50% on all four cores, then it reverts back to normal*

2.
```json
23|kiotp_node_manager_server  | [2025-10-17T07:47:22.797Z] ERROR manager/BROKER: error in channel handler--- Error: Plugin download/pull failed: Error: Plugin not found
```
 this error is coming for plugins like 
 1. kiotp.plugins.default.device.lightscv6.plugin
 2. kiotp.plugins.default.device.lightscv3.plugin
 3. kiotp.plugins.default.device.ContactSensor.plugin
 4. kiotp.plugins.default.device.KZGC.plugin

3.
```json
23|kiotp_node_manager_server  | [2025-10-17T08:00:06.473Z] WARN  manager/BROKER: Log the error: Error: StartPlugin failed: Package subpath './src/contracts/zigbee-coordinator-service' is not defined by "exports" in /data/keus-iot-platform/common-modules/node_modules/@keus-automation/hydra-core/package.json
```
1. Doorlock plugin (kiotp.plugins.default.device.plugin)

### Now the next step is to test on a hub, after removing the older services or on a fresh hub
Now while idling on the new platform
![[Pasted image 20251017144445.png]]
Cpu is averaging to 7% on all 4 cores
Memory is 587MB
And swap has decreased to 229 MB 

stats for node-manager CPU = 2% and Memory = 9% (the memory comsumption has increased because we have more free memory)

| Process         | CPU | Memory |
| --------------- | --- | ------ |
| Node-Manager    | 2   | 9      |
| ZCS             | 0.7 | 7.8    |
| Platform-Agent  | 1.9 | 3.4    |
| Mongodb in Crun | 3.2 | 6.4    |

call "1.0.0.kiotp.plugins.default.device.zigbeedimmable.plugin.service.ZigbeeDimmableDevicePlugin.identify" '{"deviceId":"68fa0d8542538ec8f965a077","ieeeAddr":"0x00124b0030cfe5c0","isActive":true}'
take deviceId from id, and ieeeAddr from zigbee.firmware for a device

## 2025-10-22
#### Steps to add and identify a device
1.  inside `/keus-iot-platform/packages/plugins-default/core/home-automation/backend/src/appliance/tools` 
2. run repl.ts 
3. How to add a device - we can't add a device

![[Pasted image 20251023144526.png|600]]


After starting new mongodb
![[Pasted image 20251023144659.png|600]]


## 2025-10-23

Identify call for ir-blaster

call "1.0.0.kiotp.plugins.default.device.irblaster.plugin.service.IRBlasterDevicePlugin.identify" '{"deviceId":"68fb198e0aeb0a6cb10f80ff","ieeeAddr":"0x00124b0030cfe5c0","isActive":true}'

call "1.0.0.kiotp.plugins.default.device.zigbeedimmable.plugin.service.ZigbeeDimmableDevicePlugin.identify" '{"deviceId":"68fb4562266d89a071bb1b7a","ieeeAddr":"0x00124b0030cfe5c0","isActive":true}'

kiotp.plugins.default.device.acfan.plugin.service.ACFanDevicePlugin
call "1.0.0.kiotp.plugins.default.device.acfan.plugin.service.ACFanDevicePlugin.identify" '{"deviceId":"68fb4562266d89a071bb1b7b","ieeeAddr":"0x00124b0030d4526f","isActive":false}'

1.0.0.kiotp.plugins.default.device.plugin.embeddedSwitch.service.EmbeddedSwitchDevicePlugin
call "1.0.0.kiotp.plugins.default.device.embeddedSwitch.plugin.service.EmbeddedSwitchDevicePlugin.identify" '{"deviceId":"68fb70a12ed8318798f801d4", "ieeeAddr": "0x00124b0026c46093", "isActive":true}'

call "1.0.0.kiotp.plugins.default.device.embeddedSwitch.plugin.service.EmbeddedSwitchDevicePlugin.identify" '{"deviceId":"68fb70a12ed8318798f801d5", "ieeeAddr": "0x00124b0031f6add5", "isActive":true}'

### Relationship between steps
1. Step1 (Downloading artifacts) - independent
2. Step2 (Preparing Backup) - independent
3. Step3 (Stopping old platform services) - dependent (Step2 needs to finished before this)
4. Step4 (Mongodb Start) - dependent (Step1 need to download mongodb, crun and create directories)
5. Step5 (Mongodb Data Migration) - dependent (dependents on Step4 and Step2 to get data for migration)
6. Step6 (Platform Services Initialization) - dependent (dependent on Step1 to get the code of all services)
7. Step7 (Register Node) - dependent (depends on Step6 to start node-manager)
8. Step8 (Zigbee Coordinator Service startup) - dependent (depends on Step7 to get nodeId)
9. Step9 (Install plugins) - dependent (depends on Step7 to start a node)

| Step No. | Step Name                          | Type        | Dependencies                                |
| -------- | ---------------------------------- | ----------- | ------------------------------------------- |
| Step1    | Downloading artifacts              | Independent | —                                           |
| Step2    | Preparing Backup                   | Independent | —                                           |
| Step3    | Stopping old platform services     | Dependent   | Step2                                       |
| Step4    | Mongodb Start                      | Dependent   | Step1 (download mongodb, crun, create dirs) |
| Step5    | Mongodb Data Migration             | Dependent   | Step4, Step2                                |
| Step6    | Platform Services Initialization   | Dependent   | Step1                                       |
| Step7    | Register Node                      | Dependent   | Step6                                       |
| Step8    | Zigbee Coordinator Service startup | Dependent   | Step7                                       |
| Step9    | Install plugins                    | Dependent   | Step7                                       |
|          |                                    |             |                                             |

More observations:
1. On adding 15 available plugins in the 

update state:  
call "1.0.0.kiotp.plugins.default.core.service.ApplianceService.appliance.updateState" '{"applianceId": "68fb70a12ed8318798f801dd", "applianceState": {"onOffState": {"onState":false}, "brightnessState": {"brightnessPercent": 0}}, "sourceType" :2}'

Update:-
1. Updated the migration script 
2. Added 4 devices in the stage hub with new platform service

![[Pasted image 20251024182936.png]]



Create schedule
call "1.0.0.kiotp.plugins.default.core.service.ScheduleService.schedule.create" '{"name":"bright00", "type": "REPEATING", "startDate": "2025-10-24", "startTime": "19:04", "endDate": "2025-10-24", "endTime": "19:06", "repeat": {"MON": true, "TUE": true, "WED": true, "THU": true, "FRI": false, "SAT": true, "SUN": true},"actionInfo": {"mainType": "APPLIANCE", "subType": "DIMMER", "identifier": {"id": "68fb70a12ed8318798f801dd"}, "state": {"onOffState": {"onState":true}, "brightnessState": {"brightnessPercent": 0}}}, "roomId": "YS3d0HzvQB", "sectionId":"Default", "isEnabled": true, "isForceExecute": true, "isForceExecute": true,"requestId":"1234","isInternal": false, "sourceType" :2}'


## 2025-10-27
1. Test if the voice-agent is working on a node or not, consequently I setup the voice-agent on a Pi5 RaspbianOS
2. Reading about livekit python server sdk and how to use it in our voice-agent
3. when running `python agent.py console` command its throwing error that PortAudio library is not installed on your system.\
	1. PortAudio is a cross-platform audio I/O library that provides a simple API for recording and playing sound on your computer.
	2. It is required by livekit agent

We now know your webcam **works perfectly at the OS and driver level**, but **not at the browser/web layer**.  

## 2025-10-28
1. call "1.0.0.kiotp.plugins.default.core.service.ScheduleService.schedule.create" '{"name":"beta", "type": "REPEATING", "startDate": "2025-10-28", "startTime": "12:35", "endDate": "2025-10-28", "endTime": "12:37", "repeat": {"MON": true, "TUE": true, "WED": true, "THU": true, "FRI": false, "SAT": true, "SUN": true},"actionInfo": {"mainType": "APPLIANCE", "subType": "DIMMER", "identifier": {"id": "68fb70a12ed8318798f801dd"}, "state": {"onOffState": {"onState":true}, "brightnessState": {"brightnessPercent": 100}}}, "roomId": "YS3d0HzvQB", "sectionId":"Default", "isEnabled": true, "isForceExecute": true, "isForceExecute": true,"requestId":"1234","isInternal": false, "sourceType" :2}'

Identify call for zigbeedimmable
call "1.0.0.kiotp.plugins.default.device.zigbeedimmable.plugin.service.ZigbeeDimmableDevicePlugin.identify" '{"deviceId":"68fb70a12ed8318798f801d2","ieeeAddr":"0x00124b0030cfe5c0","isActive":true}'

for schedules, endDate and endTime are not mandatory

1. Creating groups
2. Executing groups
3. **UpdateGroupState**: call "1.0.0.kiotp.plugins.default.core.service.GroupService.group.updateState" '{"groupId": "69008d7bd7433c2611c033fd", "groupState": {"onOffState": {"onState":true}, "brightnessState": {"brightnessPercent": 100}}, "requestId":"1234", "sourceType":2}'
4. **UpdateGroupProperties**: call "1.0.0.kiotp.plugins.default.core.service.GroupService.group.updateProperties" '{"groupId": "69009b253f76fa36e1d02e45", "groupProperties": {"onOffProperties": {}, "brightnessProperties": {"minValue": 5, "maxValue":10,"fadeUpTime": 0,"fadeDownTime": 0,"fadeOffTime":0,"fadeRate": 0}}, "requestId":"1234", "sourceType" :2}'
5. **RemoveStepFromScene**: call "1.0.0.kiotp.plugins.default.core.service.SceneService.scene.removeStep" '{"sceneId":"69009d3bbaca0a2ba5930127", "stepId": "69009d3bbaca0a2ba593012a", "requestId":"1234", "isForceDelete" : false, "sourceType":2}'
6. **AddStepToScene**: call "1.0.0.kiotp.plugins.default.core.service.SceneService.scene.addStep" '{"sceneId": "6901fbf77304385a3db4d558" , "stepType":"GROUP", "stepInfo": {"id": "6901f8c8294e64bf834f3225", "state": {"onOffState": {"onState":true}, "brightnessState": {"brightnessPercent": 5}},"delay": 0}, "requestId":"1234", "roomId": "nuwQiIf0td", "sourceType": 2}' '{"token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiJkZW1vX3VzZXIiLCJ1c2VyTmFtZSI6IkRlbW8gVXNlciIsInNpdGVJZCI6IjgxMGVmNDY4MDAwMDAwMDAwMDAwMDAwMCIsIm5vZGVJZCI6Im1hbmFnZXIiLCJpYXQiOjE3NjE2NTg0ODIsImV4cCI6MTc5MzE5NDQ4MiwiaXNzIjoiODEwZWY0NjgwMDAwMDAwMDAwMDAwMDAwIn0.LPKPoP9H4RldmR41GFHkPZ5vp3Tm820XT7iFJFmAO6o"}'
7. **ExecuteLocalScene**: call "1.0.0.kiotp.plugins.default.core.service.SceneService.scene.executeLocal" '{"sceneId": "6901fcac7304385a3db4d56c", "activitySourceInfo": {"userName": "Demo User", "userPhone": "demo_user", "timestamp": "-", "sourceType": 2}, "roomId": "nuwQiIf0td"}' '{"token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiJkZW1vX3VzZXIiLCJ1c2VyTmFtZSI6IkRlbW8gVXNlciIsInNpdGVJZCI6IjgxMGVmNDY4MDAwMDAwMDAwMDAwMDAwMCIsIm5vZGVJZCI6Im1hbmFnZXIiLCJpYXQiOjE3NjE2NTg0ODIsImV4cCI6MTc5MzE5NDQ4MiwiaXNzIjoiODEwZWY0NjgwMDAwMDAwMDAwMDAwMDAwIn0.LPKPoP9H4RldmR41GFHkPZ5vp3Tm820XT7iFJFmAO6o"}'

Rasa bot prompts
8. I am using open-source rasa bot with a openai compatible format.
9. This are the data in domain.yml for rasa bot 
	```  utter_goodbye:
      - text: "Goodbye! Have a wonderful day!"
    - text: "See you later! Let me know if you need anything!"
    - text: "Bye! Your home is in good hands!"
	```
10.  I want search for these sentences in on_conversation_item_added, and when these are detected, we will stop the agent



ExecuteLocalScene: call "1.0.0.kiotp.plugins.default.core.service.SceneService.scene.executeLocal" '{"sceneId": "6901da926b6f2653781349d9", "activitySourceInfo": {"userName": "Vishnu", "userPhone": "[+919008673313](tel:+919008673313)", "timestamp": "-", "sourceType": 2}}'

call "1.0.0.kiotp.plugins.default.core.service.SceneService.scene.createLocal" '{"name":"forty two percent", "type": "CUSTOM", "roomId": "nuwQiIf0td", "sectionId":"Default", "icon":1, "requestId":"1234", "sourceType":2}' '{"token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiJkZW1vX3VzZXIiLCJ1c2VyTmFtZSI6IkRlbW8gVXNlciIsInNpdGVJZCI6IjgxMGVmNDY4MDAwMDAwMDAwMDAwMDAwMCIsIm5vZGVJZCI6Im1hbmFnZXIiLCJpYXQiOjE3NjE2NTg0ODIsImV4cCI6MTc5MzE5NDQ4MiwiaXNzIjoiODEwZWY0NjgwMDAwMDAwMDAwMDAwMDAwIn0.LPKPoP9H4RldmR41GFHkPZ5vp3Tm820XT7iFJFmAO6o"}'

 call "1.0.0.kiotp.plugins.default.core.service.SceneService.scene.createLocal"  '{"name":"forty two percent", "type": "CUSTOM", "roomId": "nuwQiIf0td", "sectionId":"Default", "icon":1, "requestId":"1234", "sourceType":2}',

call "1.0.0.kiotp.plugins.default.core.service.SceneService.scene.addStep" '{"sceneId": "69009d3bbaca0a2ba5930127", "stepType":"GROUP", "stepInfo": {"id": "69009d3bbaca0a2ba5930120", "state": {"onOffState": {"onState":true}, "brightnessState": {"brightnessPercent": 100}},"delay": 0}, "requestId":"1234", "sourceType": 2}'

call "1.0.0.kiotp.plugins.default.core.service.SceneService.scene.addStep" '{"sceneId": "6901fcaa7304385a3db4d55c", "stepType":"GROUP", "stepInfo": {"id": "6901f8c8294e64bf834f3225", "state": {"onOffState": {"onState":true}, "brightnessState": {"brightnessPercent": 50}},"delay": 0}, "requestId":"1234", "roomId" : "nuwQiIf0td", "sourceType": 2}' '{"token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiJkZW1vX3VzZXIiLCJ1c2VyTmFtZSI6IkRlbW8gVXNlciIsInNpdGVJZCI6IjgxMGVmNDY4MDAwMDAwMDAwMDAwMDAwMCIsIm5vZGVJZCI6Im1hbmFnZXIiLCJpYXQiOjE3NjE2NTg0ODIsImV4cCI6MTc5MzE5NDQ4MiwiaXNzIjoiODEwZWY0NjgwMDAwMDAwMDAwMDAwMDAwIn0.LPKPoP9H4RldmR41GFHkPZ5vp3Tm820XT7iFJFmAO6o"}'

## 2025-10-30


## 2025-10-31
1. Do a backup, push it to cloud
2. Reset the os of hub (reflash)
3. restore the backup df

## 2025-11-03
1. Add a custom tokenizer to replace all non-alphanumeric characters with whitespace (I don't I should do this for now)
see the scenes like "all off", "ac on", "Ac off", "bright", "Relax",  "day", "night", "party",  "reading", "movie", "coffee", "rain", "romantic", "cool" are the preconfigured scenes hence I want to add some diverse examples for them, but there can be some custome scenes create by user, for that I need to have a execute_scene intent

as such I want you to read the training_data_format documentation and then suggest if I can improve my nlu data in anyway to make it more accurate for general conversation where grammatical mistakes can occur since I am using text from a SST service

1. Normalizing scenes: Instead of a separate intent per preconfigured scene, use one intent execute_preconfigured_scene with an entity scene_name (values: all_off, ac_on, ac_off, bright, relax, day, night, party, reading, movie, coffee, rain, romantic, cool). Then keep execute_scene for user-created scenes (entity scene_id or scene_name). This reduces overlap and confusion (e.g. “I want bright” vs “execute bright scene”). If you keep current per‑scene intents, add more noisy variants to each.
2. Add synonyms for scene names and common ASR mis-hearings (bright/right, night/knight, relax/relaxed, party/parti, coffee/cafi, romantic/romantics, cool/kewl).
3. Add lookup tables for rooms and scene names to help RegexFeaturizer.
4. Add a regex for scene ids (e.g. scene123) to help execute_scene.
5. Add filler / disfluency forms (“uh”, “um”, “like”, “please”, “could you”, “can you maybe”) and casual grammar errors (“i m”, “im”, “gud night”, “nite”, “turn off evrything”).
6. Include casing / spacing / number variants (“work station 2”, “workstation two”, “Work Station to”).
7. Add examples with missing punctuation and extra words (“hey can you maybe turn on the ac please”).
8. Consider adding a general fallback intent (out_of_scope) plus more greet / thank / goodbye noise to reduce false positives.
9. If you keep multiple scene intents, ensure at least 15‑20 varied examples each (currently ok but add ASR noise).
10. Add synonyms instead of stuffing mis-hearings directly; keeps example list cleaner and improves normalization.

I need to do this "Include casing / spacing / number variants (“work station 2”, “workstation two”, “Work Station to”)."
see user's room can be anything, I can add all the room names in the NLU, so I am thinking that in the NLU example I keep generic room names, and when we people 


reading the rooms name from the rooms.json file for now

bugs I am having for now
1. When saying goodbye, its utter "Hello I am your smart home assistant" - 

## 2025-11-04
1. updated the migration logic to start platform-agent as a systemctl service, in the new platform
2. for now I am using taking the binary from /keus-iot-platform/app/platform-agent/binary after building it
+918247781785

## 2025-11-05
1. reduce the number of actions "execute_contextual_scene" and "execute_scene" into one single scene
2. since I am running "action_execute_scene" for all intents like ac_on, ac_off, rain_mood, romantic_mood, the "action_execute_scene" first get the room entity from the tracker if its available, I will suggest to add some more example in preconfigured scenes intent to have some example where room is mentioned in the end like "I want to relax" can be one example where we are fetching the room from the slot, and "I want to relax in workstation", can override the slot with the room = "WorkStation", so we can include both examples

call "1.0.0.kiotp.plugins.default.device.zigbeedimmable.plugin.service.ZigbeeDimmableDevicePlugin.identify" '{"deviceId":"690b0e62ab93be03b81e168d","ieeeAddr":"0x00124b0031f8f251","isActive":255}'
take deviceId from id, and ieeeAddr from zigbee.firmware for a device

curl -X POST "http://100.82.115.91:3939/v1/migration_service/migration.get_site_details" \
  -H "Authorization: Bearer QEXdDJ59xGaJ68Jy2EB_pSSz5N2tvqtjFz-7JvrlksHcK2QKLmZECuGY2X9bnaZ8FTWTPpM" \
  -H "Content-Type: application/json" \
  -d '{
    "siteId": "Keus-b535bad3-94a1-4a95-926b-2d619d246651",
    "includeFullDetails": true
  }'


## Things to tell rasa to do
1. hey keus
2. execute relax scene in workstation
3. I am home
4. I am going away (context from previous room is stored)
5. I am in workstation two
6. Good morning

## Improving the things in the rasa bot
I have an home assistant setup, where when a wake-word is detected, I start an livekit agent which will function as a intelligent home assistant for automation, now there is a problem with current setup

when we say the wake word, then only the agent is started as a new process and after a while we can say commands to it  
is does not function like Amazon Alexz, like when we say "Alexa, turn on the lights" it turns on the light  
I want this setup to be alexa, tell me what should I do, lets discuss the approache first

is there a way to store audio recording of the first converation after the wake word got detected for somtime and pass it to the agent.py console, when it starts , so that it can give the illusion that the agent (home assistant) is already listening
### **Approach 1: Audio Buffering (Recommended - Most Alexa-like)**

**How it works:**

- Continue recording audio AFTER wake word detection
- Buffer this audio while the agent starts
- Once agent is ready, inject the buffered audio as if it was live input
- This gives the illusion the agent was already listening

**Pros:**

- Most natural Alexa-like experience
- Handles "Hey Keus, turn on the lights" in one smooth command
- No perceptible delay for the user

**Cons:**

- Need to buffer audio for 2-5 seconds
- Slightly more complex implementation
- Need to inject audio into LiveKit agent when it starts

**Implementation:**

- Modify [wake_word.py](vscode-file://vscode-app/snap/code/211/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html) to continue recording for 3-5 seconds after detection
- Save audio to a temporary WAV file or buffer
- Pass this audio file path to [agent.py](vscode-file://vscode-app/snap/code/211/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html)
- In [agent.py](vscode-file://vscode-app/snap/code/211/usr/share/code/resources/app/out/vs/code/electron-browser/workbench/workbench.html), play this buffered audio into the LiveKit room immediately after connection

**My doubts in this implementation**
1. in my current implementation, I am just running `agent.py console` in a new process, and when that ends, I start the wake_word detection program again
2. is there a way to pass audio directly as a first input in livekit agent in console mode
3. things are simpler in my current implementation since I am running a livekit server to manager anything
4. is there is no way of adding audio into livekit console, tell me if I can do this using some other feature or way in livekit (perhaps by having a local livekit server and a room)


## Second Attempt
**Things that I have done, and am sure that they work** 
1. in the agent.py, there is a instruction field I can use so when I transcribe the audio buffer and pass as a cli flag to generate the first response, perhaps this can give the illusion that agent was listening => this approach is working is working fine, but there is an added latency because of sending the audio to deepgram, and taking transciption from it
2. need to think of a better approach
3. 