# Time_Table_Generater_Ru-25-10465
# Timetable Generator (Java)

A console-based Java project that creates a clash-free timetable using **Greedy Graph Colouring**. If the greedy method needs more slots than are available, the program uses **Backtracking** to search for a valid assignment.

## Problem statement

Each subject is represented by a vertex in an undirected graph. A clash between two subjects is represented by an edge. Subjects connected by an edge must be assigned different time slots.

The program:
1. Reads subjects in the order entered.
2. Builds an adjacency-list representation of the clash graph.
3. Tries greedy graph colouring, assigning the lowest available slot to each subject.
4. If greedy colouring exceeds the available number of slots, tries backtracking.
5. Checks that both subjects exist before adding a clash edge.

## Concepts used

- **Graph:** Represents subjects and clashes.
- **Adjacency list:** Stores the neighbouring (clashing) subjects using `HashMap<String, ArrayList<String>>`.
- **Greedy algorithm:** Assigns the lowest slot that is not used by an already-coloured neighbour.
- **Backtracking:** Tries possible slot assignments and reverses a choice when it leads to a conflict.
- **Java collections:** `HashMap`, `ArrayList`, and `LinkedHashMap`.

## Requirements

- Java JDK 8 or later
- Command Prompt / Terminal or an IDE such as IntelliJ IDEA, Eclipse, or VS Code with Java support

## Project files

```text
TimetableGenerator/
├── TimetableGenerator.java
└── README.md
```

## How to compile and run

Open a terminal in the project folder and run:

```bash
javac TimetableGenerator.java
java TimetableGenerator
```

## Input format

Enter the information when prompted:

1. Subjects as comma-separated names.
2. Number of clashes.
3. Each clash as `Subject1-Subject2`.
4. Number of available time slots.

Subject names must match exactly (ignoring leading/trailing spaces).

## Sample test cases

### Test Case 1 — Normal input

**Input**
```text
DSA, DBMS, OS, CN
2
DSA-DBMS
DBMS-OS
3
```

**Expected result**
```text
Greedy colouring used.
Slot 1: DSA, OS, CN
Slot 2: DBMS
Slots used: 2
```

### Test Case 2 — Minimum input / no clashes

**Input**
```text
DSA
0
3
```

**Expected result**
```text
Greedy colouring used.
Slot 1: DSA
Slots used: 1
```

### Test Case 3 — Invalid clash

**Input**
```text
DSA, DBMS
1
DSA-AI
3
```

**Expected result (relevant message)**
```text
Subject AI not found. Clash not added.
```

The program then generates a timetable for the valid subjects and valid clashes.

### Test Case 4(a) — Greedy needs more slots, backtracking succeeds

**Input**
```text
DSA, CN, DBMS, OS
3
DSA-DBMS
DBMS-OS
OS-CN
2
```

**Expected result**
```text
Greedy needs 3 slots. Trying backtracking...
Backtracking solution found.
Slot 1: DSA, OS
Slot 2: CN, DBMS
Slots used: 2
```

### Test Case 4(b) — No valid timetable with one slot

Use the same subjects and clashes as Test Case 4(a), but enter `1` for available slots.

**Expected result**
```text
Greedy needs 3 slots. Trying backtracking...
No valid timetable with 1 slot.
```

## Algorithm overview

### Greedy colouring

For every subject in the order entered:
- Check the slots already assigned to its neighbouring subjects.
- Select the lowest-numbered slot not used by those neighbours.
- If no slot is available within the limit, greedy colouring fails.

### Backtracking

- Process subjects in their original input order.
- Try slots from `1` to the available slot count.
- Assign a slot only if none of the already-assigned neighbouring subjects uses it.
- If a later subject cannot be assigned, undo the previous assignment and try another slot.
- If every subject is assigned, a valid timetable has been found.

## Limitations

- This is a console application; it does not include a graphical user interface.
- The program treats subject names as exact text labels.
- Backtracking can take a long time for large graphs because it may explore many combinations.
- Greedy colouring is order-dependent and may use more slots than necessary; backtracking is used when the greedy result exceeds the supplied slot limit.

## Author

Harsh Wardhan Tiwari

## License

This project is prepared for academic and learning purposes.
