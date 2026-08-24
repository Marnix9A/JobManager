# Event

| Event | Posting in NAV |
| :-- | :-- |
| Stamp | No posting. Indicates that it is a log of the registration. |
| Output Journal | Posting through Output Journal. |
| Production Journal | Posting through Production Journal. |
| Job Journal | Posting through Job Journal |
| Service Line | Posting direct as Service Line. |

Lines are [posted menually](../all-pages/stamp-events.md) or [automatically with Job Queue](../daily-use/post-to-nav-bc.md).

Postings can be traced back from NAV to JobManager:

*   They will have reference to the original _Stamp Journal_. [See how](./sequence-8.md).
*   If posted through **Journals** they will further have reference to the original _Stamp Event_. [See how](./sequence-10.md).
