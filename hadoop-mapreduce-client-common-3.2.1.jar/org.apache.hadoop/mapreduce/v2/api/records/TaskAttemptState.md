# TaskAttemptState

```java
package org.apache.hadoop.mapreduce.v2.api.records;

public enum TaskAttemptState {
  NEW, 
  STARTING, 
  RUNNING, 
  COMMIT_PENDING,  
  SUCCEEDED,
  FAILED,
  KILLED
}
```