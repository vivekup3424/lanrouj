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
> - [ ] Setup the keus-iot-gateway repo
> - [ ] Code review for dev-gateway-restructure
> - [ ] Understand how the notifications work currently on the gateway side
> - [ ] Understand how code and how to work in branch `feat/device-and-appliance-flows`

> [!Done]
> - Nothing
