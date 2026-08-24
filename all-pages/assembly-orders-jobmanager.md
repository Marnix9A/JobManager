# Assembly Orders (JobManager)

This page extends the standard page _Assembly Orders_.

This page adds extra information about status for each _Assembly Order_.

The lines may take the following colors:

| Color | Description |
| :-- | :-- |
| Gray | No associated _Assembly Lines_ of type **Resource**. |
| Green | Ready for posting **(1)**. |
| Orange | _Status_ for Assembly Order is **Open**. |
| Black | If non of above applies. |

**(1)** Ready for posting applies if:

*   [JobManager Jobs](../general-setup/jobmanager-job.md) are created for this Assempbly Order.
*   All [JobManager Jobs](../general-setup/jobmanager-job.md) are reported as [Finished](../general-setup/finished.md).
*   All [Stamp Events](../all-tables/stamp-events.md) are processed.
*   All [Stamp Journal Lines](../all-tables/stamp-journal-lines-2.md) are [Calculated and Approved](./time-calculation-and-approval.md).
