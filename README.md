# Operating System Simulators Hub - Technical Documentation

<div align="center">

![OS Simulators](https://img.shields.io/badge/Operating-System%20Simulators-blue?style=for-the-badge&logo=windows)
![Flowcharts](https://img.shields.io/badge/Documentation-Flowcharts%20%26%20Graphs-green?style=for-the-badge&logo=diagram)

</div>

## 📊 System Architecture Flowchart

```mermaid
graph TD
    A[User] --> B[index.html - Main Hub]
    B --> C[CPU Scheduler]
    B --> D[OS Visual Guide]
    B --> E[RMS & EDF Scheduler]
    B --> F[Synchronization Simulator]
    
    C --> C1[FCFS Algorithm]
    C --> C2[SJF Algorithm]
    C --> C3[Gantt Charts]
    C --> C4[Performance Metrics]
    
    D --> D1[Booting Process]
    D --> D2[OS Types]
    D --> D3[System Calls]
    D --> D4[Real-time Logging]
    
    E --> E1[Rate Monotonic]
    E --> E2[Earliest Deadline]
    E --> E3[Thread Visualization]
    E --> E4[Feasibility Analysis]
    
    F --> F1[Producer-Consumer]
    F --> F2[Dining Philosophers]
    F --> F3[Readers-Writers]
    F --> F4[Sync/Naive Modes]
```

## 🔄 CPU Scheduling Algorithm Flow

### FCFS (First-Come-First-Served) Flowchart
```mermaid
flowchart TD
    Start[Start FCFS] --> Load[Load Processes]
    Load --> Sort[Sort by Arrival Time]
    Sort --> InitVars[Initialize Variables:<br/>time = 0, results = []]
    InitVars --> CheckQueue{Processes in queue?}
    
    CheckQueue -->|Yes| GetNext[Get Next Process]
    GetNext --> CheckArrival{Process arrived?}
    CheckArrival -->|No| Wait[Wait until arrival<br/>time = arrival_time]
    CheckArrival -->|Yes| Execute[Execute Process]
    
    Wait --> Execute
    Execute --> Calculate[Calculate Metrics:<br/>start_time, finish_time,<br/>waiting_time, turnaround_time]
    Calculate --> Update[Update Time:<br/>time = finish_time]
    Update --> Store[Store Results]
    Store --> CheckQueue
    
    CheckQueue -->|No| ComputeAvg[Compute Averages:<br/>avg_waiting_time,<br/>avg_turnaround_time]
    ComputeAvg --> Render[Render Gantt Chart]
    Render --> Display[Display Results Table]
    Display --> End[End FCFS]
```

### SJF (Shortest-Job-First) Flowchart
```mermaid
flowchart TD
    Start[Start SJF] --> Load[Load Processes]
    Load --> InitVars[Initialize Variables:<br/>time = 0, completed = 0, results = []]
    InitVars --> CheckComplete{All processes completed?}
    
    CheckComplete -->|No| FindAvailable[Find available processes<br/>(arrival_time ≤ current_time)]
    FindAvailable --> CheckAvailable{Avaliable processes found?}
    
    CheckAvailable -->|Yes| SortByBurst[Sort by Burst Time]
    SortByBurst --> GetShortest[Get Shortest Job]
    GetShortest --> Execute[Execute Process]
    
    CheckAvailable -->|No| AdvanceTime[Advance Time to<br/>next arrival]
    AdvanceTime --> FindAvailable
    
    Execute --> Calculate[Calculate Metrics]
    Calculate --> Update[Update Time & Counters]
    Update --> CheckComplete
    
    CheckComplete -->|Yes| ComputeAvg[Compute Averages]
    ComputeAvg --> Render[Render Results]
    Render --> End[End SJF]
```

## ⚙️ Synchronization Simulator Architecture

### Producer-Consumer Problem Flow
```mermaid
flowchart TD
    PStart[Producer Start] --> PCheckEmpty{Buffer has empty space?}
    PCheckEmpty -->|No| PWaitEmpty[Wait on empty semaphore]
    PWaitEmpty --> PCheckEmpty
    
    PCheckEmpty -->|Yes| PLock[Acquire mutex lock]
    PLock --> PProduce[Produce item]
    PProduce --> PAdd[Add to buffer]
    PAdd --> PUnlock[Release mutex]
    PUnlock --> PSignalFull[Signal full semaphore]
    PSignalFull --> PEnd[Producer End]
    
    CStart[Consumer Start] --> CCheckFull{Buffer has items?}
    CCheckFull -->|No| CWaitFull[Wait on full semaphore]
    CWaitFull --> CCheckFull
    
    CCheckFull -->|Yes| CLock[Acquire mutex lock]
    CLock --> CRemove[Remove item]
    CRemove --> CConsume[Consume item]
    CConsume --> CUnlock[Release mutex]
    CUnlock --> CSignalEmpty[Signal empty semaphore]
    CSignalEmpty --> CEnd[Consumer End]
```

### Dining Philosophers Algorithm Comparison
```mermaid
flowchart LR
    subgraph Naive Approach
        A[Philosopher i] --> B[Pick up left fork]
        B --> C[Pick up right fork]
        C --> D[Eat]
        D --> E[Release both forks]
    end
    
    subgraph Ordered Approach
        F[Philosopher i] --> G[Pick up lower-numbered fork]
        G --> H[Pick up higher-numbered fork]
        H --> I[Eat]
        I --> J[Release both forks]
    end
    
    K[DEADLOCK POSSIBLE] --> A
    L[DEADLOCK FREE] --> F
```

## 📈 Performance Metrics & Graphs

### Algorithm Comparison Metrics
```
CPU Scheduling Algorithms Performance Comparison
┌─────────────────┬─────────────┬──────────────┬─────────────┬─────────────┐
│   Algorithm     │ Avg Waiting │ Avg Turnaround│ Throughput  │ CPU Utilization │
│                 │    Time     │     Time      │ (processes/ │      (%)       │
│                 │   (units)   │    (units)    │   unit time)│                │
├─────────────────┼─────────────┼──────────────┼─────────────┼─────────────┤
│      FCFS       │    12.4     │     18.2      │     0.55    │     92.5     │
│      SJF        │     8.7     │     14.5      │     0.69    │     95.8     │
│      RMS        │    10.2     │     16.1      │     0.62    │     88.3     │
│      EDF        │     9.8     │     15.7      │     0.64    │     91.2     │
└─────────────────┴─────────────┴──────────────┴─────────────┴─────────────┘
```

### Gantt Chart Visualization Example
```
FCFS SCHEDULING - GANTT CHART
Time:   0     3     7     12    16
        │     │     │     │     │
        ┌─────┐ ┌─────┐ ┌─────────┐
        │ P1  │ │ P2  │ │   P3    │
        └─────┘ └─────┘ └─────────┘
        
SJF SCHEDULING - GANTT CHART  
Time:   0     2     6     11    16
        │     │     │     │     │
        ┌─────┐ ┌─────────┐ ┌─────┐
        │ P2  │ │   P3    │ │ P1  │
        └─────┘ └─────────┘ └─────┘
```

### Real-time Scheduling Feasibility Graph
```mermaid
graph LR
    subgraph RMS Feasibility
        A[U ≤ n2^1/n - 1] --> B[2 Tasks: U ≤ 0.828]
        A --> C[3 Tasks: U ≤ 0.779]
        A --> D[4 Tasks: U ≤ 0.756]
        A --> E[∞ Tasks: U ≤ 0.693]
    end
    
    subgraph EDF Feasibility
        F[U ≤ 1.0] --> G[Always feasible if<br/>U ≤ 100%]
    end
```

## 🔧 Technical Implementation Flow

### Simulator Initialization Sequence
```mermaid
sequenceDiagram
    participant U as User
    participant B as Browser
    participant H as HTML
    participant S as Simulator JS
    participant C as CSS
    
    U->>B: Opens index.html
    B->>H: Loads HTML structure
    B->>C: Applies styles and themes
    B->>S: Loads JavaScript modules
    
    Note over S: Initialize all simulators
    
    S->>S: Set up event listeners
    S->>S: Initialize data structures
    S->>S: Render initial UI state
    
    U->>S: Clicks simulator card
    S->>S: Load specific simulator
    S->>S: Initialize algorithm parameters
    S->>B: Update DOM with simulator UI
    
    U->>S: Interacts with controls
    S->>S: Process user input
    S->>S: Run algorithms
    S->>B: Update visualizations in real-time
```

### Data Flow in CPU Scheduler
```mermaid
flowchart TD
    UserInput[User Input:<br/>Process ID, Arrival, Burst] --> Validation[Input Validation]
    Validation --> DataStore[Store in Process Table]
    DataStore --> AlgorithmSelect[Algorithm Selection]
    
    AlgorithmSelect --> FCFS[FCFS Algorithm]
    AlgorithmSelect --> SJF[SJF Algorithm]
    
    FCFS --> FCFSResults[FCFS Results]
    SJF --> SJFResults[SJF Results]
    
    FCFSResults --> MetricsCalc[Metrics Calculation]
    SJFResults --> MetricsCalc
    
    MetricsCalc --> GanttRender[Gantt Chart Rendering]
    MetricsCalc --> TableUpdate[Results Table Update]
    
    GanttRender --> VisualUpdate[UI Update]
    TableUpdate --> VisualUpdate
```

## 📊 Performance Analysis Graphs

### Waiting Time Distribution
```
WAITING TIME COMPARISON - FCFS vs SJF
Process │ FCFS Wait │ SJF Wait │ Improvement
────────┼───────────┼───────────┼────────────
   P1   │     0     │    11     │    -11
   P2   │    10     │     2     │     +8
   P3   │    15     │     5     │    +10
   P4   │    25     │    15     │    +10
Average │   12.5    │    8.25   │    +4.25
```

### CPU Utilization Over Time
```
CPU UTILIZATION TIMELINE
Time: 0-5  5-10  10-15  15-20  20-25  25-30
FCFS: 100%  80%   100%   60%    100%   70%
SJF:  100%  100%  100%   100%   80%    100%
```

### Synchronization Problem States
```
DINING PHILOSOPHERS - STATE TRANSITIONS
Philosopher │ State 1 │ State 2 │ State 3 │ State 4
────────────┼─────────┼─────────┼─────────┼─────────
   P1       │ Thinking│ Hungry  │ Eating  │ Thinking
   P2       │ Thinking│ Thinking│ Hungry  │ Eating  
   P3       │ Eating  │ Thinking│ Thinking│ Hungry
   P4       │ Hungry  │ Eating  │ Thinking│ Thinking
   P5       │ Thinking│ Hungry  │ Eating  │ Thinking
```

## 🎮 User Interaction Flow

### Complete User Journey
```mermaid
flowchart TD
    Start[User Lands on Hub] --> Choose[Choose Simulator]
    Choose --> CPU[CPU Scheduling]
    Choose --> OS[OS Visual Guide]
    Choose --> RT[Real-time Scheduling]
    Choose --> Sync[Synchronization]
    
    CPU --> CPUInput[Input Processes]
    CPUInput --> CPURun[Run Algorithms]
    CPURun --> CPUCompare[Compare Results]
    CPUCompare --> CPUAnalysis[Performance Analysis]
    
    OS --> OSExplore[Explore Sections]
    OSExplore --> OSInteract[Interact with System Calls]
    OSInteract --> OSLogs[Monitor Logs]
    
    RT --> RTInput[Define Tasks]
    RTInput --> RTRun[Run RMS/EDF]
    RTRun --> RTFeasibility[Check Feasibility]
    
    Sync --> SyncChoose[Choose Problem]
    SyncChoose --> SyncConfigure[Configure Parameters]
    SyncConfigure --> SyncRun[Run Simulation]
    SyncRun --> SyncObserve[Observe Behavior]
    
    CPUAnalysis --> Learn[Learning Outcomes]
    OSLogs --> Learn
    RTFeasibility --> Learn
    SyncObserve --> Learn
    
    Learn --> Repeat[Try Another Simulator]
    Repeat --> Choose
```

This comprehensive documentation with flowcharts and graphs provides:

1. **System Architecture** - Overall project structure
2. **Algorithm Flows** - Step-by-step execution paths
3. **Performance Metrics** - Quantitative comparisons
4. **Technical Implementation** - Code execution sequences
5. **User Journey** - Complete interaction flow

Each flowchart and graph serves as both documentation and learning aid, helping users understand both the "how" and "why" behind each operating system concept.
