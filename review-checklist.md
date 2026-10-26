# Code Review Checklist


| Category        | Result | Defect |
|------------------|--------|--------|
| Initialization   | Issue  | `sum` in `averageAttack()` is declared but never initialized before being used in an accumulation loop (Line 59). |
| Pointers         | Issue  | Multiple missing null-pointer checks after `findMonster()` (Lines 40, 54, 64); dangling reference returned from `getMonsterLabel()` (Line 56); mismatched `delete`/`delete[]` in `readBoss()` (Line 87); use-after-free in `defeatMonster()` (Line 66); memory leak for `bonus` pointer in `main()` (Line 98). |
| Arrays/Buffers   | Issue  | `spawnMonster()` has no bounds check against `MAX_MONSTERS`, allowing array overflow when a 6th monster is spawned (Lines 29–32, 97); fixed-size buffer `char name[10]` read via `std::cin >>` with no length limit, risking buffer overflow (Lines 80, 83). |
| Loops            | Issue  | Off-by-one error in `totalMonsterHealth()` loop condition `i <= monsterCount` causes out-of-bounds array access (Line 48). |
| Arithmetic       | Issue  | Signed/unsigned mismatch in `attackMonster()` makes the underflow check ineffective (Lines 41–42); possible division by zero in `averageAttack()` (Line 61); integer truncation before double conversion in `calculateDamage()` (Line 71). |
| Control Flow     | Issue  | Assignment (`=`) used instead of comparison (`==`) inside `if` condition in `findMonster()` (Line 35); `playerRank()` is missing a return statement for the `score <= 100` case, causing undefined behavior (Lines 74–77). |
| Function Calls   | Issue  | `attackMonster(99, 20)` is called with a non-existent monster ID, triggering a null-pointer dereference inside the function (Line 99); `getMonsterLabel()` call returns a dangling reference that is immediately used (Line 100). |
| Classes          | Issue  | No user-defined copy constructor/assignment operator in `Game`; default shallow copy of `Monster*` array leads to double-free when `game` and `copy` are both destructed (Line 107); `defeatMonster()` leaves a dangling pointer inside the `monsters[]` array, causing a second delete in the destructor. |
