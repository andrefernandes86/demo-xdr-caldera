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

__Starting the demo!
This demo script was created to demonstrate the following use case:
+ Attacker trying to get the control of an Windows Instance
+ Attacker is using Mitre Caldera as C&C Server
++ Using Mitre Caldera, the Attacker will generate one malicious payload (powershell). This malicious payload will generate a reverse connection between the Windows Instance and the C&C Server.
++ The Attacker, using the Mitre Caldera, will use the tools available on Mitre Caldera to start checking some conditions and extracting sensitive data from the Windows Computer



https://ps2exe.azurewebsites.net/

