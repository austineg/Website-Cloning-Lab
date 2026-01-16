Website cloning works by using kali linux platform to generate tools for the cloning. The tools are deployed by first typing the command "setoolkit" in the kali terminal



![WhatsApp Image 2026-01-15 at 5 33 31 AM](https://github.com/user-attachments/assets/24a2da0b-9f76-43bc-9b30-2cde27712263)



from here you navigate from "website Attack vectors" to "credential harvester attack method" to "site cloner" then you identify the host IP network, for example, i am using 10.6.6.1, once that is used, it prompt you on the url to clone.



![WhatsApp Image 2026-01-15 at 5 40 46 AM](https://github.com/user-attachments/assets/99338c37-4618-4f53-aee7-8fb1f6334d7e)



Once the targeted url is identify, it tells you the port the site is running on

Ater then, you open a text editor on your kali and create and save a simple html file that can redirect the clone website to the original website



![WhatsApp Image 2026-01-15 at 5 50 43 AM](https://github.com/user-attachments/assets/0f6b94cb-0d84-495c-8735-b2d0657df983)



Once the html file is saved as "site.html" double cliked it to display the clone website on your web browser


![WhatsApp Image 2026-01-15 at 5 54 08 AM](https://github.com/user-attachments/assets/eeb9835d-914e-4185-9478-aa197ca70d65)



This is the clone website:


![WhatsApp Image 2026-01-15 at 6 00 19 AM](https://github.com/user-attachments/assets/ac2fa191-6b96-4223-b46d-866908be92d8)



So now when you go to the kali machine, it displays the GET response of the clone website with its status code


![WhatsApp Image 2026-01-15 at 6 02 33 AM](https://github.com/user-attachments/assets/418dd770-7f85-41aa-b390-0cd4fd19f198)



When you login with your username and password like this:


![WhatsApp Image 2026-01-15 at 6 08 12 AM](https://github.com/user-attachments/assets/cf904f12-b33b-43a0-9ec9-21a583ead70e)



It redirect you to the original website


![WhatsApp Image 2026-01-15 at 6 09 01 AM](https://github.com/user-attachments/assets/80b2ada6-6b59-480f-b817-7845115eff13)



then when you go to your kali machine, you see the login credential such as the (username, password and the user_token) that was used to access the original website, from here you got to know the user login credential into the original website protal



![WhatsApp Image 2026-01-15 at 6 09 27 AM](https://github.com/user-attachments/assets/34587bbe-5d8a-438c-b705-4f13148575f0)




About SMB Vulnerability Scanning:
SMB (Server Message Block) is a network protocol used mainly in Windows environments for: File sharing, Printer sharing, Accessing shared folders,Windows domain communication
It usually runs on: TCP port 445 (modern SMB) and TCP ports 139 / NetBIOS (older SMB).
Enum4linux and Enumeration are pair tools used for the SMB service.

How does it work:
Let say, there are to host on a network, HostA(Laptop) and HostB(Printer) communicating together, you want to infiltrate as a MIMA



![WhatsApp Image 2026-01-15 at 6 54 26 AM](https://github.com/user-attachments/assets/af76477f-9f28-4005-b2bf-a34ebfbeb4c6)



First, you run nmap(nmap -sN) on 172.17.0.0/24 network to know the hosts that are UP in the network and the SMB PORTs
the -sN command is used to avoid detection by IDS/IPS network device that detects any SYN traffic so as to bypass the simple ACLs.



![WhatsApp Image 2026-01-15 at 6 45 40 AM](https://github.com/user-attachments/assets/38742835-0a27-4633-9062-1f226bef9fd2)



Then run the enumeration tool(enum4linux) to enumerate users in the network(172.17.0.2)
enum4linux -U 172.17.0.2



![WhatsApp Image 2026-01-15 at 7 13 56 AM](https://github.com/user-attachments/assets/74fbd104-b8f9-4433-a39e-9ec63c1295d1)



![WhatsApp Image 2026-01-15 at 7 23 03 AM](https://github.com/user-attachments/assets/72c258a0-623c-47b6-8fbb-270b0dd4eb70)



![WhatsApp Image 2026-01-15 at 7 16 48 AM](https://github.com/user-attachments/assets/b33bf780-52c0-4e6d-945f-d932c921b6d2)




Next enumerate the shared resource on the network(172.17.0.2)
enum4linux -S 172.17.0.2
You are basically asking 172.17.0.2:
“What shared folders do you have?”
What you get back
You get only the NAMES of shared folders, for example:
Public
Shared
IPC$
print$.....
You do NOT see the files inside them.



![WhatsApp Image 2026-01-15 at 7 37 24 AM](https://github.com/user-attachments/assets/7072601b-75a7-47f7-a0e0-f1e07546bb92)



....the dollar sign means the share name does not show up when someone casually browses the network but if you know the name you can still access it with permission.
the C$ means hidden share of the C drive
ADMIN$ used for remote administration
IP$ used for system communication
print$ printer driver files

Enum4linux -Sv 172.17.0.2 which mean give me more detail info about the share name



![WhatsApp Image 2026-01-16 at 12 03 50 AM](https://github.com/user-attachments/assets/173ae968-079e-4abd-990e-ba96cdc87e9e)



Enum4linux -P 172.17.0.2, this is asking the target machine(172.17.0.2) what password policy rules is use.
Password policy is the rules for passwords, such as:
Minimum password length
Password complexity (uppercase, numbers, symbols)
How many wrong attempts are allowed
Password expiration time


![WhatsApp Image 2026-01-16 at 12 18 39 AM](https://github.com/user-attachments/assets/048ce2ea-d78f-4988-be7c-b308e1870381)



enum4linux -a 172.17.0.2, this perform full SMB enumeration on the target machine(172.17.0.2)

Pls note, In reconnaisance, attackers first check your network to know which hosts are alive by using the command: nmap -sn 10.6.6.0/24, before carring out lateral movement


![WhatsApp Image 2026-01-16 at 1 51 56 AM](https://github.com/user-attachments/assets/1321957a-975b-4afb-a3ee-f8ffdd3af319)






