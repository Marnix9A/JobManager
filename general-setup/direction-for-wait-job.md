# Direction for Wait Job

This field determines _which_ nearby job should be used for [Min Time Wait Job](./min-time-wait-job.md) functionality.

**Previous** changes the _gap_ to the same as the job registration _before_ the _gap_. Except if the _gap_ is just after Clock-In, then the _following_ registration is used.

**Next** changes the _gap_ to the same as the job registration _following_ the _gap_. Except if the _gap_ is just before Clock-Out, then the registration _before_ is used.

## See also

[Time Calculation and Approval](../all-pages/time-calculation-and-approval.md)
