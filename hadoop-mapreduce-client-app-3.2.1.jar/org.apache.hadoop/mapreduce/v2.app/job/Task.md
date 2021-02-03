# Task

```java
package org.apache.hadoop.mapreduce.v2.app.job;

import java.util.Map;

import org.apache.hadoop.mapreduce.Counters;
import org.apache.hadoop.mapreduce.v2.api.records.TaskAttemptId;
import org.apache.hadoop.mapreduce.v2.api.records.TaskId;
import org.apache.hadoop.mapreduce.v2.api.records.TaskReport;
import org.apache.hadoop.mapreduce.v2.api.records.TaskState;
import org.apache.hadoop.mapreduce.v2.api.records.TaskType;

/**
 * 任务的仅读视图
 * Read only view of Task.
 */
public interface Task {
  TaskId getID();
  TaskReport getReport();
  TaskState getState();
  Counters getCounters();
  float getProgress();
  TaskType getType();
  Map<TaskAttemptId, TaskAttempt> getAttempts();
  TaskAttempt getAttempt(TaskAttemptId attemptID);

  /**
   * 任务是否到达了最终的状态
   * Has Task reached the final state or not.
   */
  boolean isFinished();

  /**
   * taskAttempt 的输出是否可以提交。
   * Can the output of the taskAttempt be committed. Note that once the task
   * gives a go for a commit, further canCommit requests from any other attempts
   * should return false.
   * 
   * @param taskAttemptID
   * @return whether the attempt's output can be committed or not.
   */
  boolean canCommit(TaskAttemptId taskAttemptID);

  
}

```