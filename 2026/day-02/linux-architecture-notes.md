Architecture of Linux :
•	Hardware : The physical component where OS is installed.
•	Kernel : The heart of Linux. It directly talks to hardware(CPU, memory, disk, etc) and manages processes, memory, devices. Kernel controls everything that is happening in the system.
•	Shell : Interactive way to talk to kernel using commands.
•	Applications : Applications are programs that run in user space. For example: chrome, VS Code, Docker.
•	System Utilities : System utilities are the command line tools that help you interact with the system and perform tasks. They run in user space and use the kernel to do actual work. For example : ls, cp, top
Processes in Linux
Processes are instances of running programs. A process is a program that is currently running in the system. When you run any program or application in Linux, it becomes a process. For ex. if you do ping ww.google.com then ping process is created. It keeps sending requests → process keeps running. It shows replies continuously.
Process states
•	Running : Active process. Process is executing.
•	sleeping : Idle process. Waiting for something like input/output.
•	Stopped : Process paused by signal SIGSTOP (Ctrl+Z, Ctrl+C). It can be resumed by a SIGCONT signal.
•	Zombie : The process has terminated, but its entry in the process table still exists because its parent process has not yet read its exit status.
systemd (init / PID 1)
•	systemd is the first process that starts when Linux boots (PID = 1) 
•	It is responsible for managing system services 
•	It can start, stop, restart, and monitor services 
•	Helps in troubleshooting using logs and service status 
 Example :
systemctl status nginx

5 Commands used daily
 ls : list files and directories 
cd : change directory 
pwd : show current directory path 
cat : view file content  
systemctl status : check service status
