1)  Explain the importance of regular system updates and patching in a linux environment?
		* Recent Vulnerability
		* Stability
		Regular system updates help us to patch the recent vulnerabilities that over came into network. It gives the stability of the usage, that some libraries won't properly work for the recent releases. So it would help us to resolve that kind of issues.
2) How you would Secure SSH access on a Linux Server?
		* RBAC (Role Based Access control)
		* Not providing root access user
		* Saving the SSH private in public
		* Regularly reviewing the SSH logs 
		RBAC - provides role based access control over the machines. even a unprivileged user won't access a sensitive files.
		Providing root access to the ssh is should be avoided and encourage admin to create a RBAC to a user.
		SSH private key shouldn't be kept inside publicly.
		Regularly reviewing the ssh logs will help us to detect the suspicious activities.
3) Purpose of SELinux (Security Enhanced Linux) and how it enhances system.
		SELinux is a MAC (mandatory access control), enforces the security of using access policies, restricting the actions of users and process of elevated privileges.
		* limit the impact of security breaches.
4) Role of iptables in linux security and setup some basic firewall?
		* IP filter in the linux kernel.
		`iptable -A INPUT -p tcp --dport 22 -j DROP`
5) How to monitor and analyse system logs for security incidents?
		/var/log is the main log directory to store all the logs of services.
		to analyse the log we can use `sort, awk, grep` commands.
6) Explain the concept of file permissions in linux and how they contribute to security ?
		basically the file permissions will provides a security to which user can which types of file and what are the permissions can be given to the user.
		It does have `read, write and execute` permissions.
		we can provides the file permissions using chmod +rwx or 777
		and we can provide the access of user chown to provide the privileges of the user
7) How would you handle the suspected security breach on linux server?
		In this case I would first isolate the environment and take snapshot of the environment.
		Analyze the system logs for any malicious activities.
		Conduct a thorough security audit.
		Follow IR procedures.
		Notifying the relevant parties and escalating to higher authorities.
		Then applying the patches for the breach.
8) How do you you check listening ports on a linux server?
		`netstat -tulp`
9) limit the 