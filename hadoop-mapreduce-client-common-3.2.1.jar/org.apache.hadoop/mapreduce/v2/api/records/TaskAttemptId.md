# TaskAttemptId

```java
package org.apache.hadoop.mapreduce.v2.api.records;

/**
 * TaskAttemptId 表示一个任务尝试的唯一标识。
 * 每个任务尝试都是一个特定的Map或Reduce任务实例，这个任务实例由它的TaskId标识。
 * <p>
 * <code>TaskAttemptId</code> represents the unique identifier for a task
 * attempt. Each task attempt is one particular instance of a Map or Reduce Task
 * identified by its TaskId.
 * </p>
 * 
 * TaskAttemptId 由两部分组成。
 * 第一部分是这个TaskAttemptId所属的TaskId
 * 第二部分是这个任务尝试的序号
 *
 * <p>
 * TaskAttemptId consists of 2 parts. First part is the <code>TaskId</code>,
 * that this <code>TaskAttemptId</code> belongs to. Second part is the task
 * attempt number.
 * </p>
 */
public abstract class TaskAttemptId implements Comparable<TaskAttemptId> {
  /**
   * @return the associated TaskId.
   */
  public abstract TaskId getTaskId();

  /**
   * @return the attempt id.
   */
  public abstract int getId();

  public abstract void setTaskId(TaskId taskId);

  public abstract void setId(int id);

  protected static final String TASKATTEMPT = "attempt";

  @Override
  public int hashCode() {
    final int prime = 31;
    int result = 1;
    result = prime * result + getId();
    result =
        prime * result + ((getTaskId() == null) ? 0 : getTaskId().hashCode());
    return result;
  }

  @Override
  public boolean equals(Object obj) {
    if (this == obj)
      return true;
    if (obj == null)
      return false;
    if (getClass() != obj.getClass())
      return false;
    TaskAttemptId other = (TaskAttemptId) obj;
    if (getId() != other.getId())
      return false;
    if (!getTaskId().equals(other.getTaskId()))
      return false;
    return true;
  }

  @Override
  public String toString() {
    StringBuilder builder = new StringBuilder(TASKATTEMPT);
    TaskId taskId = getTaskId();
    builder.append("_").append(
        taskId.getJobId().getAppId().getClusterTimestamp());
    builder.append("_").append(
        JobId.jobIdFormat.get().format(
            getTaskId().getJobId().getAppId().getId()));
    builder.append("_");
    builder.append(taskId.getTaskType() == TaskType.MAP ? "m" : "r");
    builder.append("_")
        .append(TaskId.taskIdFormat.get().format(taskId.getId()));
    builder.append("_");
    builder.append(getId());
    return builder.toString();
  }

  @Override
  public int compareTo(TaskAttemptId other) {
    int taskIdComp = this.getTaskId().compareTo(other.getTaskId());
    if (taskIdComp == 0) {
      return this.getId() - other.getId();
    } else {
      return taskIdComp;
    }
  }
}
```