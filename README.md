# Experiment No. 3: Program to Implement Banker's Algorithm

```
Name : Namachivayam T
Reg No : 212223060179
```
## Aim

To write and execute a Python program to implement the Banker's Algorithm for deadlock avoidance and determine whether the system is in a safe state by finding a safe sequence of process execution.

## Algorithm

1. Start.

2. Read the number of processes `n` and the number of resource types `m`.

3. Input the following:

   * Allocation Matrix
   * Maximum Need Matrix
   * Available Resources Vector

4. Calculate the Need Matrix using:

   `Need = Maximum − Allocation`

5. Initialize:

   * `Work = Available`
   * `Finish[i] = False` for all processes.

6. Search for a process `Pi` such that:

   * `Finish[i] == False`
   * `Need[i] <= Work`

7. If such a process is found:

   * Add the process to the Safe Sequence.

   * Update:

     `Work = Work + Allocation[i]`

   * Set `Finish[i] = True`.

8. Repeat Steps 6 and 7 until all processes are marked as finished or no suitable process is found.

9. If all processes are finished:

   * Display the Safe Sequence.
   * Print `"System is in a SAFE state."`

10. Otherwise:

    * Print `"System is in an UNSAFE state."`

11. Stop.

## Procedure for Executing the Python Program

* Open a Python programming environment such as IDLE, VS Code, PyCharm, or Google Colab.
* Create a new Python source file.
* Type or paste the Banker's Algorithm program into the editor.
* Save the file with the extension `.py` (e.g., `bankers.py`).
* Run the program.
* Enter the number of processes and resource types.
* Enter the Available Resource Vector.
* Enter the Maximum Matrix.
* Enter the Allocation Matrix.
* Observe the Need Matrix, Safe Sequence, and system state displayed on the screen.
* Verify whether the system is in a Safe or Unsafe State based on the generated safe sequence.

## Program

```python
# Program to implement Banker's Algorithm

n = int(input("Enter number of processes: "))
m = int(input("Enter number of resources: "))

print("\nEnter Available resources:")
available = list(map(int, input().split()))

print("\nEnter Max matrix:")
max_matrix = []

for i in range(n):
    row = list(map(int, input(f"P{i}: ").split()))
    max_matrix.append(row)

print("\nEnter Allocation matrix:")
allocation = []

for i in range(n):
    row = list(map(int, input(f"P{i}: ").split()))
    allocation.append(row)

need = []

for i in range(n):
    row = []
    for j in range(m):
        row.append(max_matrix[i][j] - allocation[i][j])
    need.append(row)

print("\nNeed Matrix:")

for row in need:
    print(row)

work = available.copy()
finish = [False] * n
safe_sequence = []

while len(safe_sequence) < n:
    found = False

    for i in range(n):
        if not finish[i]:
            if all(need[i][j] <= work[j] for j in range(m)):
                for j in range(m):
                    work[j] += allocation[i][j]

                finish[i] = True
                safe_sequence.append(i)
                found = True

    if not found:
        break

if len(safe_sequence) == n:
    print("\nSystem is in a SAFE state.")
    print("Safe Sequence:", end=" ")

    for i in safe_sequence:
        print(f"P{i}", end=" ")

    print()
else:
    print("\nSystem is in an UNSAFE state.")
```

## Output

<img width="472" height="567" alt="image" src="https://github.com/user-attachments/assets/659f48ab-990e-41a1-83b1-fa3018f7a5b2" />

## Result

Thus, the Python program to implement the Banker's Algorithm was executed successfully, and the system state was determined. If a safe sequence existed, the system was found to be in a Safe State; otherwise, it was identified as being in an Unsafe State.
