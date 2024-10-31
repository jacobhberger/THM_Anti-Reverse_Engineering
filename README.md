# THM_Anti-Reverse_Engineering
TryHackMe Anti-Reverse Engineering Box

Learning Objectives
- Learn why malware authors use anti-reverse engineering techniques
- Learn about different anti-reverse engineering techniques
- Learn the techniques on how to circumvent anti-reverse engineering using various tools
- Learn how anti-reverse engineering techniques are implemented by reading the source code

======================
What I Did and Learned
======================
Anti-Debugging Overview
- malware authors use anti debugging measures
-   checkig for presence of debuggers (such as windows API func IsDebuggerPresent
-   malware may try and tamper with debugger registers, alter the execution of code so debugger does not function correctly
-   self modifying code

Anti-Debugging Using Suspend Thread
- windows API functions used to pause execution of a thread in a process
- malware may use this to stop the execution of the debugger at all
