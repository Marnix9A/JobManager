# Post to NAV/BC

This section describes how the lines in [Stamp Events](../all-tables/stamp-events.md) can be automatically posted in NAV/BC. Alternative the can be [posted manually](../all-pages/stamp-events.md).

**Semi-automatic**

On most [JobManager Role Centers](../other-setup/role-center.md) is a function _Post to NAV/BC_.

This posts all lines in Stamp Events which stands as _Waiting_.

**Fully automatic**

Codeunit _6182771 JobManNavPost_ is to be added to the Job Queue. Specify the same Job Queue Category as indicated [here](./job-queue-category-code.md).

At _JobManager Setup_ there is a function _Make Job Queue Entry_ which automatically creates this in the Job Queue.

## See also

[Stamp Events](../all-pages/stamp-events.md)  
[Q&A (Post to NAV/BC)](../q-and-a-questions-and-answers/q-and-a-post-to-nav-bc.md)  
[Pre-Pay (Time Calculation)](./pre-pay-time-calculation.md)
