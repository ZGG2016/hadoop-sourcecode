# TaskEvent

```java
package org.apache.hadoop.mapreduce.v2.app.job.event;

import org.apache.hadoop.yarn.event.AbstractEvent;
import org.apache.hadoop.mapreduce.v2.api.records.TaskId;

/**
 * 封装了与任务相关的事件。
 * this class encapsulates task related events.
 *
 */
public class TaskEvent extends AbstractEvent<TaskEventType> {

  private TaskId taskID;

  public TaskEvent(TaskId taskID, TaskEventType type) {
    super(type);
    this.taskID = taskID;
  }

  public TaskId getTaskID() {
    return taskID;
  }
}

```