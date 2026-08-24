# Leave Warning

If missing _Clock-out_ registration can automatically be made according to the Employee [Time Schedule](../jobmanager-calculations/time-schedule.md).

Specifies how long the Employee must have been at work before the system warns about missing _Clock-out_ registration. This can help the Employee to make the missing _Clock-out_ registration.

This field works together with the field [Error handling](../other-setup/error-handling.md) on the [JobManager User Interface](../other-setup/jobmanager-user-interface.md) table. The system checks, when the employee opens a registration page, whether _X_ time has passed since _Clocked-in_.

*   **Error handling** = `Standard BC` or `Info box` asks the employee `Yes` or `No` whether a _Clock-out_ registration should be made.
    
*   **Error handling** = `Timer box` means that a _Clock-out_ registration is _always_ made, without any intervention from the employee.
    

## See also

[Registration Cockpit](../daily-use/registration-cockpit.md)  
[JobManager - Registration Client](../daily-use/jobmanager-registration-client.md)
