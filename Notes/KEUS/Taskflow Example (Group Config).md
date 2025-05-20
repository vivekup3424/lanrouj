---
tags:
  - taskflow
---

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

## Storing metadata in nats-header
We are storing
```json
{
  "taskflowExecutionContext": {
    "taskflow": {
      "id": "c3dec307-99f2-437e-9942-8f7128210ddc",
      "stageId": "6be74e3e-2861-44e3-b61f-39ca1aae6e5b",
      "createdAt": 1747656460737,
      "taskId": "7038abdc-4cc6-4026-8abf-316531b7e6c1",
      "taskInfo": {
        "id": "7038abdc-4cc6-4026-8abf-316531b7e6c1",
        "attempt": 0,
        "meta": {},
        "params": {
          "x": 2,
          "y": 3
        },
        "options": {
          "maxRetries": 3,
          "maxAge": 60000,
          "timeout": 60000,
          "retryDelay": 5000,
          "exactlyOnceTaskExecution": false,
          "continueOnTaskFailure": true
        },
        "status": "WAITING",
        "nestedActiveRunningTaskFlowIds": [],
        "nestedTaskflows": [],
        "name": "task1",
        "type": "ACTION",
        "taskDetails": {
          "serviceId": "planning-service",
          "actionName": "createBlueprint"
        }
      }
    }
  }
}
```

we are storing every information about taskflow's task in meta => storing it in nats header

### we are also storing previous stage response 
```json
{
  "taskflowExecutionContext": {
    "previousStageRes": [
      {
        "taskName": "task1",
        "response": null
      },
      {
        "taskName": "task2",
        "response": {
          "success": true,
          "data": "NOTIFIED USER"
        }
      }
    ],
    "taskflow": {
      "id": "c3dec307-99f2-437e-9942-8f7128210ddc",
      "stageId": "80360bd5-9e24-4275-bca9-72bd4209af98",
      "createdAt": 1747656460737,
      "taskId": "7d16d80f-9ca9-43ce-aa0e-4f81258191ca",
      "taskInfo": {
        "id": "7d16d80f-9ca9-43ce-aa0e-4f81258191ca",
        "attempt": 0,
        "meta": {},
        "params": {},
        "options": {
          "maxRetries": 3,
          "maxAge": 60000,
          "timeout": 60000,
          "retryDelay": 5000,
          "exactlyOnceTaskExecution": false,
          "continueOnTaskFailure": true
        },
        "status": "WAITING",
        "nestedActiveRunningTaskFlowIds": [],
        "nestedTaskflows": [],
        "name": "task3",
        "type": "ACTION",
        "taskDetails": {
          "actionName": "prepareFoundation",
          "serviceId": "construction-service"
        }
      }
    }
  }
}
```

### we are also storing the parent taskflow execution context in meta
```json
{
  "taskflowExecutionContext": {
    "taskflow": {
      "id": "451f3438-7552-4f1b-8068-efbda1eeb401",
      "stageId": "04995efd-5e6a-426c-8455-344216c53db4",
      "createdAt": 1747656479205,
      "taskId": "ff56cf65-676d-4f95-9bc4-82c8335c2e7e",
      "taskInfo": {
        "id": "ff56cf65-676d-4f95-9bc4-82c8335c2e7e",
        "attempt": 0,
        "meta": {
          "taskflowExecutionContext": {
            "previousStageRes": [
              {
                "taskName": "task1",
                "response": null
              },
              {
                "taskName": "task2",
                "response": {
                  "success": true,
                  "data": "NOTIFIED USER"
                }
              }
            ],
            "taskflow": {
              "id": "c3dec307-99f2-437e-9942-8f7128210ddc",
              "stageId": "80360bd5-9e24-4275-bca9-72bd4209af98",
              "createdAt": 1747656460737,
              "taskId": "82ace2f0-5d21-4691-8bba-9b63692a1f51",
              "taskInfo": {
                "id": "82ace2f0-5d21-4691-8bba-9b63692a1f51",
                "attempt": 0,
                "meta": {},
                "params": {},
                "options": {
                  "maxRetries": 3,
                  "maxAge": 60000,
                  "timeout": 60000,
                  "retryDelay": 5000,
                  "exactlyOnceTaskExecution": false,
                  "continueOnTaskFailure": true
                },
                "status": "WAITING",
                "nestedActiveRunningTaskFlowIds": [],
                "nestedTaskflows": [],
                "name": "task7",
                "type": "ACTION",
                "taskDetails": {
                  "actionName": "finishInteriors",
                  "serviceId": "construction-service"
                }
              }
            }
          }
        },
        "params": {
          "a": 5,
          "b": 6
        },
        "options": {},
        "status": "WAITING",
        "nestedActiveRunningTaskFlowIds": [],
        "nestedTaskflows": [],
        "name": "task2",
        "type": "ACTION",
        "taskDetails": {
          "actionName": "installBeds",
          "serviceId": "vendor-service"
        }
      }
    }
  }
}
```