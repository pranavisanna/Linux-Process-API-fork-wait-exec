# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls
#include <stdio.h> #include <stdlib.h> #include <unistd.h> #include <sys/wait.h>

int main(void) { pid_t pid = fork();
```
if (pid < 0) {
    perror("fork failed");
    return 1;
}

if (pid == 0) {
    printf("I am child, my PID is %d\n", getpid());
    printf("My parent PID is %d\n", getppid());
    sleep(2);
} else {
    printf("I am parent, my PID is %d\n", getpid());
    wait(NULL);
}

return 0;
}
```
##OUTPUT
<img width="535" height="720" alt="image" src="https://github.com/user-attachments/assets/d131b78b-3d86-4df2-b58e-49d991f2d10f" />


## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family
#include <stdio.h> #include <stdlib.h> #include <sys/types.h> #include <sys/wait.h> #include <unistd.h>

int main(void) { int status; pid_t pid;
printf("Running ps with execl\n");
fflush(stdout);

pid = fork();
```
if (pid < 0) {
    perror("fork failed");
    return 1;
}

if (pid == 0) {
    execl("/bin/ps", "ps", "-f", (char *)NULL);
    perror("execl failed");
    exit(1);
}

waitpid(pid, &status, 0);

if (WIFEXITED(status)) {
    printf("Child exited with status: %d\n",
           WEXITSTATUS(status));
}

printf("Running ps with execlp (without full path)\n");
fflush(stdout);

pid = fork();

if (pid < 0) {
    perror("fork failed");
    return 1;
}

if (pid == 0) {
    execlp("ps", "ps", "-f", (char *)NULL);
    perror("execlp failed");
    exit(1);
}

waitpid(pid, &status, 0);

if (WIFEXITED(status)) {
    printf("Child exited for execlp with status: %d\n",
           WEXITSTATUS(status));
}

printf("Done.\n");
return 0;
}
```
##OUTPUT

<img width="618" height="583" alt="image" src="https://github.com/user-attachments/assets/519b72b4-28f7-41e2-ae15-1f417432b20e" />

# RESULT:
The programs are executed successfully.
