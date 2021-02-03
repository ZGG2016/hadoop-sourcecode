# TaskEventType

```java
package org.apache.hadoop.mapreduce.v2.app.job.event;

/**
 * 任务处理得时间类型
 * Event types handled by Task.
 */
public enum TaskEventType {

  //Producer:Client, Job
  T_KILL,

  //Producer:Job
  T_SCHEDULE,
  T_RECOVER,

  //Producer:Speculator
  T_ADD_SPEC_ATTEMPT,

  //Producer:TaskAttempt
  T_ATTEMPT_LAUNCHED,
  T_ATTEMPT_COMMIT_PENDING,
  T_ATTEMPT_FAILED,
  T_ATTEMPT_SUCCEEDED,
  T_ATTEMPT_KILLED
}

```