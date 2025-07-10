G## 2025-01-29
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
- the taskflow placeholder design has changed now
- we are using {{stageName}}, {{stageName.taskName}}, {{stageName.taskName.property}}, {{stageName.taskName.property.subproperty.subsubproper...}} for using placeholders
- stageName, taskName, propertyNames can only be containing a to z, A to Z, 0-9, _


## 2025-06-04
- Wrote the clean code architecture for the motion-detection plugin, have not tested it, will do it soon
- Now I am quite dissatisfied with code wriiten by vscode-agent (sonnect 4.0) for the rasa chatbot for smart home automation
	- hence I will try to read the documentation of rasa myself, and code it out myself
	- my most important problem that arose from using vscode agent
	- was that generated rasa bot was not functioning well, and it was also not doing any conversations
	- so I will try to start writing the code again step-by-step (with smaller example creating conversational-ai)

## 2025-06-11
1. Working on common modules, thinking about way to reduce the bundle size of plugins by placing their common modules in a common dependency
2. Need to test whether this approach is working on different plugins, and for different hubs.

## 2025-06-30
1. Today I am working on creating a authorization service with
   ![](Pasted%20image%2020250630173153.png)

this is very similar to the way AWS is creating IAM.
need to update my resume with these details.

## 2025-07-10
- [ ] read about "reading logs from fluentbit"
- [ ] read about filtering logs from fluentd
- [ ] send http messages for these filtered logs
- [ ] get the demo for tomorrow working
