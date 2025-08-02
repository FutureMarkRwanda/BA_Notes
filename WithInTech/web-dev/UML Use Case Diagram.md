# UML Use Case Diagram: Online Doctor Appointment Booking System

```
Actors:
[Patient]   [Doctor]   [Admin]

Use Cases:
[View Doctors] ---- [Patient]
[Book Appointment] ---- [Patient]
[Reschedule] ---- [Patient]
[Cancel] ---- [Patient]
[Accept/Decline Appointment] ---- [Doctor]
[Update Availability] ---- [Doctor]
[Manage Doctors] ---- [Admin]
[Manage Users] ---- [Admin]
[View Stats] ---- [Admin]

System:
+---------------------+
| Booking System      |
| - View Doctors      |
| - Book Appointment  |
| - Reschedule        |
| - Cancel            |
| - Accept/Decline    |
| - Update Availability|
| - Manage Doctors    |
| - Manage Users      |
| - View Stats        |
+---------------------+
```

**Instructions**: Create a UML diagram in Draw.io with actors (stick figures) on the left, use cases (ovals) inside a system boundary box, and lines connecting actors to use cases. Label all elements clearly. Export as an image for insertion.