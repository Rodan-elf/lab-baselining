Okay so i found out that : 

1. the presence of a user named “adm1n” (line 696) instead of “admin” on a windows xp workstation (users > adm1n, ghunter, gparker, fbonilla) >> I’m pretty sure that “adm1n” is a naming tactic to blend into normal system while maintaining unauthorized access.

2. a different MD5 hash for the process “svhost.exe” (line 1606) on a windows 10 workstation (users > admin, hgraham) f0f10baa7c0183cbf175e3116bddf27c instead of d1c56374fff0243832b8696d133b7861 >> given your hint, this indicates the process is compromised.

3. on workstation windows 7 (users > admin, cnewton) in addition to port 135/TCP, the port 23/TCP is open (line 1659) which is suspicious bcs all the other workstations are listening only on port 135/TCP. Port 23/TCP > Telnet >> unencrypted, insecure remote access protocol.

Here’s my reflexion path : 

first, i recognized that baselining is about finding the anomalies. so i decided to divide the data in 3 groups. users, processes, ports. 

for users, i scanned through the lists of employee usernames looking for anything that didn’t fit the standard naming > first initial + last name (hgraham). My eyes hit on adm1n instead of admin.

for processes, thanks to your hint i didn’t need to look up these hashes on virustotal but i just needed to look for inconsistencies. so to find the compromised process i simply copied the hash of each process and did cmd+f to find the exact same text in the file. that’s how I found out that for the process svchost.exe one MD5 hash was different from the others.

for ports, this was the easiest one, i saw 135/TCP was standard on every workstation so the moment i spotted 23/TCP on that single windows 7 machine, i flagged it. then i searched on my notes what port 23 means and found out telnet was a vulnerability and an indicator of compromise (or misconfig)
