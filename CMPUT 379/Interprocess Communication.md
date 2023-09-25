Cooperating processes need to exchange information, as well as synchronize with each other, to perform their collective task(s). The primitives like `wait()` can be used to synchronize the operation of cooperating processes, but they **do not convey information between processes**. 

Methods for effective sharing of information among cooperating processes are collectively known as **inter-process communication (IPC)**.
## IPC mechanisms
The following are IPC mechanisms can be used for IPC:
- Shared Memory (threads)
- Files
- Pipes
- Signals
- Shared Memory (processes) – later
- Message Passing – later
- Sockets – later