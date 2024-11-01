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
- run example program performing this technique, as we can see it suspends the debug process x64dbg
![x64dbg debugger suspended](6e78f4aab8de049609c41c5588f70124.png)
- Solution: patch function SuspendThread so that the debugger wont be suspended
- Steps:
  1. open x62dbg and open example malware file
  2. F9 to jump to execution EntryPoint
  3. Within intermodular calls search for SuspendThread and select the SuspendThread entry
  4. On part of code that calls the SuspendThread API, fill it with NOPs. Memory 0004011AB-00401B0 are set to 90 hex or (No Operation)
  5. Now if we attempt to continue execution of the malware, prints out "Debugger found...! Suspending" while it is still finding the debugger we are now skipping the part of the malware execution that suspends the debugger
  6. Temp fix, now we need to export than import our patch for future use
  7. Repeat path steps but before rerunning, view the patch file and save it
  8. Re debug malware and import patch
![Patch applied](patch.png)
  9. As we can see without going through entire patching process we have still patched the malware
![Patch applied](2adb65eb552a957b2d52c88edd672cf3.png)
