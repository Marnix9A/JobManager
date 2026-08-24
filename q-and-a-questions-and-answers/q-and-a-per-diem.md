# Q&A (Per Diem)

Per Diem setup in JobManager.

Create a new IPC category "Per Diem"

In this category you create 3 new triggers (for each Per Diem), for use in registration.

Examples could be:

*   LodgingMealsDay(Daily)
*   LodgingMealsStart(Start)
*   LodgingMealsStop(Stop)

Create a new Registration add-on "Lodging and Meals"

and fill in the triggers Start, Stop and Day in the new section Automation.

Min/max duration is for the system to se how far the calculation can be back and forth in time.

### Calculation options

_1\. Per Diem every day - uses Start/Stop and Daily trigger_

_2\. Per Diem last day - uses Start/Stop trigger_

to be set up at Allocation, nothing (times is calculatid last day), Daily (time is calculated each day) _Job (for projects) allocates the time for each job during the day_

It is also possible to set up a Pay type to payment in salary.
