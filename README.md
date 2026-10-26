# DormsSystem

A Java console application for managing student dormitories, developed for the Advanced Topics in Object-Oriented Programming and Java course at Ruppin Academic Center.

The system connects student registration, room allocation, payments, and maintenance through a menu with 14 actions. It uses inheritance, polymorphism, interfaces, Java collections, and object serialization.

[Watch the demonstration on LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7520112939966603264/).

## Features

- Register local and international students, assign rooms, and manage a waiting list.
- Inspect room occupancy, transfer students between rooms, and process checkout.
- Record rent payments, advance the simulated billing month, and apply late fees.
- Report maintenance issues, queue requests, dispatch available workers with matching skills, and mark jobs complete.
- Add or remove staff members, add rooms, and update room prices.
- Search students by name prefix and display a building map or financial report.
- Save application data on exit and restore it on the next run.

## Build and run

Requires **JDK 17 or newer**, including the `javac` compiler. No third-party libraries or build tool are required.

Open a terminal in the repository folder and compile:

```bash
javac -encoding UTF-8 --release 17 -d out src/module-info.java src/dorms/*.java
```

Start the application:

```bash
java -cp out dorms.Main
```

You can also open the source folder in a Java IDE configured for Java 17 and run `dorms.Main`.

On first launch, the application creates eight empty rooms across two buildings and three example staff members. The example staff details are demonstration values supplied in the code. The saved session from the original ZIP is excluded, so the public version starts fresh.

Choose **14. Exit System** to save and close normally. Data is stored in `DormsData.ser` in the working directory and loaded the next time the program runs from that directory. The file is ignored by Git.

Monthly billing is an explicit menu action, not an automatic calendar task. Payment dates and identifiers follow the original course-project implementation.

## Main menu

| Option | Action |
| --- | --- |
| 1 | Register a student and assign a room or join the waitlist |
| 2 | Inspect rooms and residents |
| 3 | View and assign waitlisted students |
| 4 | Report, dispatch, and complete maintenance requests |
| 5 | Manage staff |
| 6 | Display the building map or financial report |
| 7 | Advance the simulated month and apply billing updates |
| 8 | Search for students by name prefix |
| 9 | Transfer a student to another room |
| 10 | Checkout / remove a resident |
| 11 | Process a student's payments |
| 12 | Add a dorm room |
| 13 | Update room pricing |
| 14 | Save and exit |

## Maintenance workflow

A new issue enters a FIFO queue. Dispatch examines the oldest request and looks for an available worker with the required job title. Once assigned, the worker becomes unavailable and the request moves to the active jobs list. Marking the job fixed closes the request and makes the worker available again.

The initial example workers cover plumbing, electrical work, and general repairs.

## Design and files

| File | Role |
| --- | --- |
| `Main.java` | Menus, collection management, billing, and persistence |
| `Person.java` | Abstract base class for people |
| `Student.java` | Student profile, assigned room, and payment history |
| `InternationalStudent.java` | Student specialization with passport and visa fields |
| `StaffMember.java` | Worker role and availability |
| `Room.java` | Room capacity, residents, and pricing |
| `MaintenanceRequest.java` | Maintenance status, worker assignment, and charges |
| `Payment.java` | Payment status, amount, and late fees |
| `Payable.java` | Common payment behavior interface |
| `InputValidator.java` | Console input validation |
| `src/module-info.java` | Java module declaration |

The classes are in the `dorms` package under `src/dorms/`. Rooms use a `TreeMap` for sorted access, dynamic lists use `LinkedList`, and maintenance dispatch uses a `Queue`.

## Verification

The prepared source compiled successfully for Java 17. An automated console walkthrough checked student registration and room assignment, maintenance reporting / dispatch / completion, monthly billing and late fees, payment, room transfer, name search, saving, and loading the saved data in a second run.

Only submission ID numbers were removed from the source comments for publication. Application logic is unchanged. Compiled classes, IDE settings, and the original saved session are excluded.

Developed by Rayan Suan.
