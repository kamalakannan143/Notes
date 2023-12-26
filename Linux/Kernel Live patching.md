#### Diff b/w patch and update

| Patch | Update|
|---|--|
|a partial snippet of the code|minor version of package which contains bug fixes, new features and performance improvement|

Live patching could be used for any patch for the running kernel including regular bug fixes and the enhancements.
#### Two Spaces of Linux System Operations:
1) userspace - all the services and applications operate
2) namespace - core system operations are

Diff b/w userspace and the namespace

|userspace| namespace|
|---|----|
|part of computer memory where user processes run| In linux kernel it provides isolation for the resources|
|distinct from a kernelspace| own instace of glabal resources such as `n/w interface process IDs and mount points`|
|includes applications, libraries and user level processes| contributes to the process and resource isolation in the OS|
|when program executes a command the code runs in userspace. User processes interact with the kernel through system calls but run in userspace. | n/w namespace isolates n/w related resources, enabling diff processes to have their own n/w stack|

Linux admins will do the kernel live patching using **ftrace**. It will the route from obsolete function to the replacement function.

Ksplice - first build tool for the kernel live patch (sold to oracle and completely changed to closed-source tool)
Kpatch from redhat and kgraft SUSE linux