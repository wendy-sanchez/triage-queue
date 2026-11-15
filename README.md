# Triage Queue — Priority Queue Manager

A lightweight Python command-line application that manages a hospital triage waiting queue using priority levels and FIFO ordering.

Patients are attended according to their triage level: critical patients first, followed by urgent and standard patients. Within the same priority level, patients are served in their order of arrival.

This project was developed as part of an educational assignment at **4Geeks Academy**.

## Features

- **Patient registration:** Add patients with a name, triage level, and arrival timestamp.
- **Priority-based scheduling:** Critical (1), urgent (2), and standard (3) patients are handled in the correct order.
- **FIFO ordering:** Patients with the same triage level are served in arrival order.
- **Next patient lookup:** Inspect the next patient without removing them from the queue.
- **Queue management:** Display all waiting patients in their expected service order.
- **Queue statistics:** Count waiting patients by triage level.
- **Input validation:** Reject invalid triage levels and handle empty patient names.
- **Interactive CLI:** Operate the queue through a terminal menu.

## How It Works

The application uses three independent `collections.deque` instances, one for each triage level.

```python
self._queues = {
    1: deque(),  # Critical
    2: deque(),  # Urgent
    3: deque(),  # Standard
}
```

This structure provides:

| Operation | Time complexity |
|---|---:|
| Enqueue | O(1) |
| Dequeue | O(1) |
| Peek | O(1) |
| List queue | O(n) |
| Statistics | O(1) |

Priority is maintained by checking the queues in order (1 → 2 → 3). FIFO ordering is preserved naturally within each individual queue.

## Requirements

- Python 3.11 or newer.
- No external Python dependencies.

The application uses Python standard-library modules, including `collections.deque`, `dataclasses`, `datetime`, and `sys`.

## Getting Started

Run the application from the project directory:

```bash
python3 triage_queue.py
```

On Windows, you can also use:

```bash
python triage_queue.py
```

## Available Operations

The interactive menu provides five options:

1. Add a new patient.
2. Call the next patient.
3. View the current queue.
4. View queue statistics.
5. Exit the application.

## Project Structure

```text
triage-queue/
├── triage_queue.py   # Patient model, priority queue, and CLI
├── DESIGN.md         # Data structure decisions and concurrency analysis
└── README.md         # Project documentation
```

## Design Considerations

The `DESIGN.md` document explains the choice of three separate deques and compares this approach with:

- A single ordered deque.
- A priority queue implemented with `heapq`.
- Three standard Python lists.

It also discusses concurrency risks and the use of `threading.Lock` as a possible synchronization strategy for a future multi-worker implementation.

**Concurrency protection is not implemented in the current application.** The program currently runs as a single-threaded command-line application.

## Scope and Limitations

This is an educational simulation of a priority-based waiting queue, not a production hospital information system.

- Patient data is held in memory and is not persisted.
- There is no graphical interface or database integration.
- There is no multi-user or concurrent processing support.
- Triage levels are simplified for the exercise and do not implement a complete clinical assessment protocol.

---

**Developer Wendy Sanchez**
