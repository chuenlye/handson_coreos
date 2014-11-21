# fleet-specific Options
四つscheduing policiesを指定できる：(units fileの `[X-Fleet]`部分)

| Option Name | Description |
|---------------|-------------|
| `X-ConditionMachineID` | Require the unit be scheduled to the machine identified by the given string. |
| `X-ConditionMachineOf` | Limit eligible machines to the one that hosts a specific unit. |
| `X-ConditionMachineMetadata` | Limit eligible machines to those with this specific metadata. |
| `X-Conflicts` | Prevent a unit from being collocated with other units using glob-matching on the other unit names. |

Machine Metadata: anything you can set it in fleet's config. e.g. machine's region, rack location, disk speed or anything else you can think of.

できること：

fleet allows you to define flexible architectures for running your services:

    * Deploy a single container anywhere on the cluster
    * Deploy multiple copies of the same container
    * Ensure that containers are deployed together on the same machine
    * Forbid specific services from co-habitation
    * Maintain N containers of a service, re-deploying on failure
    * Deploy containers on machines matching specific metadata

Four unit file in this handson:

    - app1.service: using X-ConditionMachineID
    - app2.service: using X-ConditionMachineOf
    - app3.service: using X-Conflicts
    - app4.service: using X-ConditionMachineMetadata

Test:

    $ fleetctl start app{1,2,3}.service
    Job app1.service launched on ba04d7eb.../10.240.194.107
    Job app2.service launched on ba04d7eb.../10.240.194.107
    Job app3.service launched on 34aa3ef6.../10.240.152.191

    $ fleetctl list-units
    UNIT            STATE       LOAD    ACTIVE  SUB DESC        MACHINE
    app1.service        launched    loaded  active  running app1        ba04d7eb.../10.240.194.107
    app2.service        launched    loaded  active  running app2        ba04d7eb.../10.240.194.107
    app3.service        launched    loaded  active  running app3        34aa3ef6.../10.240.152.191

**NOTES** on test of app4.service(X-ConditionMachineMetadata): 

At first, you must configure metadata in fleet's config when startup instance or runtime.
TODO
