# File Polling and File System Concepts.

## Questions Related to File Poller Service

1. **How did you implement the file polling mechanism in your project?**  
    
2. **How do you schedule file polling at regular intervals?**  
3. **How do you read and validate files from an FTP server using Java?**  
4. **Which libraries or technologies did you use to connect and interact with the FTP server?**  
5. **How do you handle errors during file polling or validation?** (e.g., if the file is corrupted or missing)
6. **How do you ensure that the same file is not processed twice?**
7. **How is the polling frequency configured and retrieved from the database dynamically?**
8. **What were some challenges you faced while building the file poller service? How did you solve them?**
    - There were several significant challenges we encountered while developing the file polling service:
    - First, we faced issues with **concurrent file processing** when large batches arrived simultaneously. Multiple instances of our poller would attempt to process the same files, causing duplication and data integrity problems. I implemented a **file locking mechanism** using atomic file operations where we'd create a temporary marker file during processing, allowing other instances to detect and skip files already being handled.
    - Third, performance degradation occurred when processing extremely large files or when the target directories contained thousands of files. I optimized this by implementing a batching strategy that processed files in configurable chunks and introduced file filtering based on timestamps to prioritize newer files.

9. Why Spring Batch is better for File Polling?
   
    This Spring Batch approach is significantly more efficient than the previous implementations for several reasons:

    1. **Resource Management**:
    - Spring Batch maintains a database of job executions, preventing duplicate processing
    - Built-in connection pooling and transaction management

    2. **Concurrency Control**:
    - Spring Batch handles job synchronization via its JobRepository
    - Prevents multiple instances from processing the same files

    3. **Scalability**:
    - Easy to scale by adding multithreaded steps or partitioning
    - Can be configured for both vertical (within a server) and horizontal (across servers) scaling

    4. **Error Handling**:
    - Comprehensive error handling with retry, skip, and restart policies
    - Failed items don't cause entire batch to fail
    - Automatic restart from point of failure

    5. **Performance Optimizations**:
    - Chunk-based processing to manage memory usage
    - Transaction boundaries at the chunk level for efficiency
    - Configurable commit intervals

    6. **Monitoring & Management**:
    - Built-in metrics for job execution time, success rates, etc.
    - Integration with Spring Boot Actuator for monitoring
    - Job execution history and restart capability

    For even better performance, you could add:

    ```java
    @Bean
    public TaskExecutor taskExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(5);
        executor.setMaxPoolSize(10);
        executor.setQueueCapacity(25);
        return executor;
    }

    // And in the step definition:
    .taskExecutor(taskExecutor())
    .throttleLimit(8)  // Limit concurrent threads
    ```