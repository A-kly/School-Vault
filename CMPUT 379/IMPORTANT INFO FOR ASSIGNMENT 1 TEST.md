# fork()
```c
#include <sys/types.h>
#include <unistd.h>
pid_t fork(void);
	/* Create a new process
	- Return Value:
	- -1 - creation of a child process was unsuccessful
	- 0 - Returned to the newly created child process
	- >0 - Returned to parent or caller. The value contains process ID
	of newly created child process */
```

# wait()
```c
#include <sys/types.h>
#include <sys/wait.h>
pid_t wait(int *status);
/* Wait until one of its children terminates
-  Return Value:
-  Terminated process ID - success
-  0 or -1 - error */
```