# Code Hooks

JobManager offers a range of _Hooks_, which can be used as desired.

A _Hook_ is a call to a _Codeunit_. This call is triggered many places in the JobManager module.

This table provides the ability to change which _Codeunits_ to run.

Using this option **avoids** changes to JobManager objects, making updating JobManager versions much easier.

The lines in this table is [automatically created](../general-setup/jobmanager-foundation-setup-guide.md).

_Hooks_ kan be used in combination with [Custom Fields](./custom-fields.md) or [Custom signing functions](./custom-signing-functions.md).

**As of NAV 2016 it's recommended to use _Events_.** All _Hooks_ are also available as _Events_ in NAV 2016. In addition, there are even more _Events_ available. Codeunit _6182705 JobManNavEnventPublisher_ has a complete list of _Events_.

If JobManager is installed as an _Extension_ on **Dynamics Business Central** only the **Events** could be used. The _Hooks_ are obsolete!

**The installation package for JobManager contains some examples.**

**Also see [here](./code-customization.md)!**

[Ref. Object Type](./ref-object-type-2.md)  
[Ref. Object ID](./ref-object-id-2.md)  
[Ref. Object Name](./ref-object-name-2.md)  
[Key](./key.md)  
[Key 2](./key-2.md)  
[Key 3](./key-3.md)  
[Active](./active.md)  
[Run Object Type](./run-object-type.md)  
[Run Object ID](./run-object-id.md)  
[Run Object Name](./run-object-name.md)  

## See also

[JobManager Foundation Setup Guide](../general-setup/jobmanager-foundation-setup-guide.md)  
[Code customization](./code-customization.md)
