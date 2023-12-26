**Dirty Cow**

Copy on write

https://www.cs.toronto.edu/~arnold/427/18s/427_18S/indepth/dirty-cow/index.html

* copy on write mechanism
* racecondition vulnerabilty of mmapping and the perfrom operations in madvise in the threads.

Methodology:
1) create private copy of the read only file
2) write to a private copy

My understanding:
Basically the dirty cow allows you to provide the write privileges for the read only files. so that way you can interact with root also.

interacts with the memory

**Dirty pipe**
linux kernel vulnerability that allows the ability of non-privileged users to overwrite read-only files.

* allows apps to manipulate linux pipes so that the application can insert its data into page of memory.

https://dirtypipe.cm4all.com/