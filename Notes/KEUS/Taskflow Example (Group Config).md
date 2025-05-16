There is a service for configuring of a group containing 10 devices
So we need to send one message to each device, 
Now each of this channel we start

Example Taskflow

```typescript
const taskflowObj: ITaskflow.TaskFlowSchema<Record<any, any>> = {
    options: {
        maxAge: 60 * 1000,
        timeout: 60 * 1000,
        retryDelay: 5 * 1000,
        continueOnTaskFailure: true,
        exactlyOnceTaskExecution: false,
    },
    context: {
        description: "This is a taskflow for configuring a group",
    },
    stages: [
        {
            name: "createGroup",
            tasks: [
                {
                    name: "createGroup",
                    params:{
                        groupId: "sdvn78",
                        groupType: "room",
                        groupName: "bed-room",
                    },
                    type: ITaskflow.TaskType.ACTION,
                    taskDetails:{
                        serviceId: "group-core",
                        actionName: "createGroup",
                    }
                }
            ]
        },
        {
            name: 'addApplianceToGroups',
            tasks: [
                {
                    name: "addApplianceAlpha",
                    params: {
                        groupId: "sdvn78",
                        applianceId: "vions56x",
                    },
                    type: ITaskflow.TaskType.ACTION,
                    taskDetails: {
                        serviceId: "appliance-core",
                        actionName: "AddApplianceToGroup",
                    },
                    options: {
                        maxRetries: 3
                    }
                },
                {
                    name: "addApplianceBeta",
                    params: {
                        groupId: "sdvn78",
                        applianceId: "viosds6456x",
                    },
                    type: ITaskflow.TaskType.ACTION,
                    taskDetails: {
                        serviceId: "appliance-core",
                        actionName: "AddApplianceToGroup",
                    },
                    options: {
                        maxRetries: 3
                    }
                },
            ]
        },
    ],
};
```

## Response for Taskflow Produce
```typescript
  return {
	success: true,
	data: {
	  taskflowId: taskflowId,
	  eventSubscription: MolecularNatsGatewayEventEmitter.getEventsEndpoint(taskflowId, true)
	}
  }
```

## Event monitoring during processing of a taskflow
The `subscribeToTaskflowEvents` method of taskflow allows you to monitor taskflow events in real-time. This is essential for tracking the progress and status of your taskflows.

Or you can make use of `eventSubscription` returned during taskflow produce to get real-time updates on taskflow

emiting event for task's status updates
```typescript
await MolecularNatsGatewayEventEmitter.emitEvent({
	eventType: ITaskflowEvent.EventType.TASK,
	data: {
		taskflowId,
		attempt: task.attempt,
		stageId: stageId,
		taskId: taskId,
		taskStatus: task.status,
		taskResponse: task.response,
		taskflowObject: updateTaskflowRes.taskflow,
	}
});
```

emitting event for stage's status updates
```typescript
await MolecularNatsGatewayEventEmitter.emitEvent({
	eventType: ITaskflowEvent.EventType.STAGE,
	data: {
		taskflowId,
		stageId: stageId,
		stageStatus: updateTaskflowRes.taskflow.stages[stageId].status,
		taskflowObject: updateTaskflowRes.taskflow,
	}
});
```

emitting event for taskflow's status updates
```typescript
await MolecularNatsGatewayEventEmitter.emitEvent({
	eventType: ITaskflowEvent.EventType.TASKFLOW,
	data: {
		taskflowId,
		taskflowStatus: updatedTaskflow.taskflow.status,
		taskflowObject: updatedTaskflow.taskflow,
	}
});
```


## Actions you can perform for a specific taskflow
### Getting Taskflow Details
- Retrieve the current state of a taskflow using the `getTaskflowDetails` method. 
- This is useful for checking the status of a taskflow at any point in time.
- This will return you the whole taskflow tree, containing the responses, status and attempt number of each task
- This will also returns all the details of the nested taskflows

```typescript
const taskflowDetails = await taskflow.getTaskflowDetails("your-taskflow-id");
console.log("Taskflow details:", taskflowDetails);
```

### Cancelling a taskflow
Cancel an ongoing taskflow using the `cancelTaskflow` method. This is useful when you need to stop a taskflow that's no longer needed or has encountered issues.

```typescript
const cancelResult = await taskflow.cancelTaskflow("your-taskflow-id");
console.log("Taskflow canceled:", cancelResult);
```

### Retrying a taskflow
Retry a failed taskflow using the `retryTaskflow` method.

```typescript
async retryTaskflow(taskflowId: string, stagesInfo?: string[], tasksInfo?: ITaskflow.TaskInfo[]): Promise<ITFRetryTaskflowAction.Response> 
```

For now, we can 
1. Retry the execution of all tasks (using the `exactlyOnceExecution: false`  in taskflow object's options)
```typescript
taskflow.retryTaskflow("your-taskflow-id") 
```
2. Retry specific stages
```typescript
// Retry all tasks in the specified stages
taskflow.retryTaskflow("your-taskflow-id", [
  { stageId: "stage-id-1" },
  { stageId: "stage-id-2" }
])
```
3. Retry only the failed tasks (  `exactlyOnceExecution: false`)
```typescript
taskflow.retryTaskflow("your-taskflow-id") 
``` 
4. Retry specific tasks, using their stage-id and task-id and passing them as array in the second parameter
StageId is for the stage containing the corresponding task.
```typescript
// Retry specific tasks within specific stages

taskflow.retryTaskflow("your-taskflow-id", [
  { stageId: "stage-id-1", taskIds: ["task-id-1", "task-id-2"] },
  { stageId: "stage-id-2", taskIds: ["task-id-3"] }
])
```

