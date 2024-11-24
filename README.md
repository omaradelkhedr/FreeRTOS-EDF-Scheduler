# FreeRTOS EDF Scheduler Integration

This project integrates an **Earliest Deadline First (EDF)** scheduler into the FreeRTOS kernel. The EDF scheduler ensures tasks are executed based on their deadlines, optimizing real-time scheduling for time-sensitive systems.

![FreeRTOS](https://github.com/user-attachments/assets/aaf0ffcb-6e7e-4c9e-b5bb-f8bd763191cf)

## Features
- **Custom EDF Scheduler:** Implements scheduling based on task deadlines.
- **Trace Hooks:** Measure task execution times and calculate CPU utilization.
- **Periodic Task Management:** Includes examples of periodic tasks with different execution intervals.

---

## File Structure
1. **`FreeRTOSConfig.h`**:
   - Enables EDF scheduler via `configUSE_EDF_SCHEDULER`.
   - Implements hooks for task execution and CPU load monitoring.

2. **`main.c`**:
   - Demonstrates the use of the EDF scheduler with periodic tasks.
   - Configures hardware and timers for FreeRTOS.

3. **`tasks.c`**:
   - Introduces modifications for EDF scheduling.
   - Implements a new `xTaskPeriodicCreate` function for periodic task creation.
   - Adjusts task management functions to account for deadlines.

---

## Task Configuration

### EDF Scheduler
To enable the EDF scheduler, set the following in `FreeRTOSConfig.h`:
```c
#define configUSE_EDF_SCHEDULER 1
```
### Standard Scheduler
To use the standard scheduler instead of EDF, set the following in `FreeRTOSConfig.h`:
```
#define configUSE_EDF_SCHEDULER 0
```

## Example Tasks

The `main.c` file demonstrates three tasks with periodic execution:

- **Task 1**: Executes every 30ms.
- **Task 2**: Executes every 40ms.
- **Task 3**: Executes every 50ms.


## Timing and CPU Load

The trace hooks in `FreeRTOSConfig.h` capture task execution times and compute CPU utilization using the formula:

```c
cpuLoad = ((task1_totalTime + task2_totalTime + task3_totalTime) / (float)systemTime) * 100;
```

## Additional Information

### `tasks.c` Modifications
The `tasks.c` file includes critical changes to support EDF scheduling:

1. **Periodic Task Creation**:
   - Adds the function `xTaskPeriodicCreate` for defining periodic tasks.

2. **Deadline Management**:
   - Modifies task management to account for task deadlines.

3. **Ready Task Lists**:
   - Adjusts the ready task list to order tasks by their deadlines.


## Screenshots

1. **Runtime Analysis - CPU Load**:


![Runtime Analysis - CPU Load](https://github.com/user-attachments/assets/ffc53e2c-366e-41c5-8909-d801c76c88fb)



2. **Runtime Analysis - Logic Analyzer**:


![Runtime Analysis - Logic Analyzer](https://github.com/user-attachments/assets/1325fc76-a128-4154-997a-0b349f5790e8)



3. **Simso Simulation Result - CPU Load**:


![Simso Simulation Result - CPU Load](https://github.com/user-attachments/assets/1d87b946-3955-4dcd-9747-654b5dd14f23)



4. **Simso Simulation Result - Gantt**:


![Simso Simulation Result - Gantt](https://github.com/user-attachments/assets/f7f847de-d4cf-486c-a7ef-8ff8d9b3477a)
