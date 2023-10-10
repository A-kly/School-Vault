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

# Open()
```c
#include <sys/stat.h>
#include <fcntl.h>
int open(const char *path, int oflags, mode_t mode);
/* Open a file
- Parameter:
- Oflags - O_RDONLY, O_WRONLY,O_RDWR, O_APPEND, O_CREAT, etc.
- mode - S_IRUSR, S_IWUSR, S_IXUSR, etc.
- Return Value:
- -1 - error
- Others - file descriptor */
```

# Close()
```c
#include <unistd.h>
int close(int fildes);
/* Close a file
-  Parameter:
-  Fildes - The file descriptor to be closed
-  Return Value:
-  -1 - error
-  0 - success */
```

# Write and read
