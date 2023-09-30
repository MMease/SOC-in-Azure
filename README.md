
![AZ](https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/67beb882-e81e-44c9-9211-d99c577ce189)

<h1>Deploying Microsoft Sentinel</h1>

1. First you need to create a free Azure account (https://azure.microsoft.com/en-us/free/)
   - 200 Free Credits is associated with the account that expires in 30 days.

2. Using a github repository (Azure All in One), we will automate the deployment of resources.
   - Selct this link -> (https://github.com/Azure/Azure-Sentinel/tree/master/Tools/Sentinel-All-In-One)
   - Read section titled " What does All-in-One do? ". This shows what resources are being created from the repository.
   - Select " Deploy to Azure "
<img width="1230" alt="Step 2 - Deploy to Azure" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/79e70129-e0d5-4bca-920c-0bc5987e32ea">

<h2>Deployment and Settings</h2>

1. Select a location for your resources.
   - Keep in mind some resources are not available based on region
2. Give a name for the Resource group & Workspace.
   - Same name makes it easier to keep up with
3. Set daily ingest to 10 GBs.
<img width="727" alt="Step 3 - Set up deployment" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/430a76f8-d972-4906-9ac8-78fee12c7dac">

4. Go to settings
   - Enable "Enable Sentinel health diagnostics"
<img width="727" alt="Step 3a - Settings" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/999de589-8391-4c05-bad8-565109b10bb0">

5. Go to Content Hub Solutions
   - Select each dropdown bar and check every option 
<img width="727" alt="Step 3b - Content Hub Selection" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/313dd355-0a23-48d6-b1ef-acfdaba5f5b4">

6. Go to Data Connectors
   - Select each dropdown bar and check every option 
<img width="729" alt="Step 3c - Data Connectors" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/c5bd4c61-b9b3-40c2-86eb-0d59168371e4">

7. Go to Analytics Rules
   - Enable all severity levels
<img width="729" alt="Step 3d - Analytics Rules" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/016aef8f-d0a7-4620-8814-6e23ed25a0e9">

<h3>Diagnostic Settings</h3>

8. Go to your resource group and select your Workspace.
   - Once selected, find the diagnostic settings and turn on three things:
   - "Send to Log Analytics workspace" under Destination details, "allLogs" under Logs, and "AllMetrics" under Metrics
<img width="1036" alt="Step 4a - Diagnostics setup" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/15388a5b-785b-43bc-856d-172ec2745427">


<h4>Sentinel Review | UEBA Feature | Automation Playbook</h4>

9. Go to Sentinel and look for "Analytics"
   - After following the previous steps you will see alerts start to show
<img width="1466" alt="Step 5 - Microsoft Sentinel review" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/6b7c322b-ac2c-4314-9ef7-47fa3f92d4b3">

10. Next, we're going to Turn on the UEBA feature.
    - The User and Entity Behavior Analytics (UEBA) feature in Microsoft Sentinel provides advanced threat detection by analyzing and correlating user and entity behavior to identify potential security incidents.
<img width="755" alt="Step 5a - UEBA feature" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/f7279f36-2236-4812-bcf8-528b541e0cd0">

11.  Go to settings under Microsoft Sentinel.
    - Expand "Playbook permissions"
    - Select "Configure permissions" then select your Workspace.
<img width="1484" alt="Step 5b - Configure automation Playbooks" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/83c943b0-2964-4aa7-b1b5-f186c0dacae9">

<h5>Watchlist Setup</h5>

12. Go to "Watchlist" to then select "Add New"
    - After giving the watchlist a name. A resource file was uploaded with IP addresses.
    - Once created. We can see the logs created from the file.
<img width="1792" alt="Step 6 - Set up watchlist" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/00bf94f9-69be-4c00-85e2-906bf67cfb63">
<img width="1452" alt="Step 6a - Watchlist in logs" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/b8919290-4c75-4677-ae51-d0251e2dc14b">


<h5>Create a Rule to Detect Threats</h6>

13. A rule needs to be created to detect incoming threats.
    - First we will create a Scheduled Rule.
 <img width="1244" alt="Step 7 - Create Sceduled rule" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/dddc4f09-e363-4d5b-936e-b0c3ac2fa81e">

   - Next we will use KQL to tell what Sentinel to look for in the data.
   - Insert the following code:
    let TorNodes = (_GetWatchlist('Tor-ip-addresses')
      project | TorIP = IpAddress);
    SigninLogs
      | where IPAddress in (TorNodes)
      | where ResultType != 50126
      | project
          TimeGenerated.

<img width="862" alt="Step 7a - Rule Query" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/8f3f5e93-a611-4c91-9099-c4c039824b8c">

   - Next we will use Key:Value pairing for alert enhancements.
   - Also creating a query schedule for updates.
<img width="1159" alt="Step 7b - Alert Enhancement " src="https://github.com/MMease/SOC-in-Azure/assets/42321472/f525d97f-356c-448c-bc50-ba3d3b1051bd">
<img width="1137" alt="Step 7c - Alert Enhancement v2" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/532c1649-813f-4e0f-b5d5-d426b7ed6ed1">


   - Finally the incident settings that helps with similar alert groupings
<img width="1288" alt="Step 7d - Incident settings" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/14d7260e-fc31-47ef-91bb-46b4b2a05f03">

<h6>Active Directory</h6>

14. Turn off the default security settings by going to active directory
    - Then go to "properties" and select disabled.
    - You must give a reason to do so because this feature is extremly important for security reasons.
<img width="1790" alt="Step 8 - Active Directory" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/e44fba9a-b54e-4a1f-a5e9-39cae0e3c4cd">

   - We will create a new user to test our alerts
   - Then we will add the user to "Priviledged Admin Role"
   - To add roles, go to "Resource Group" > Select your workspace > then go to "Access control (IAM)"
   - Select "Contributer" and then you will have the option to add the created user.
<img width="662" alt="Step 8a - Create new user" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/97668ad5-313b-47e3-8917-a3405a8a08f9">
<img width="1634" alt="Step 8d - Adding Role" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/f2b2fdaf-408e-4901-bba0-c1cc53e79353">

<h7>Download a privacy browser</h7>

15. For this project i used brave.(https://brave.com)
   - Once downloaded, log into the created users account and change the password.
   - This will generate an alert due to the browser using VPN.
   - After the password is changed, switch to the regular browser and delete the diagnostic settings.
<img width="1157" alt="Step 9 - Change password in (Brave)" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/108d8d1f-b930-4fe8-a769-0b8186cc1c54">

<h8>Start the Event Managment and Remdiation process </h8>

16. You will see different incident Alerts on your sentinel dashboard.
   - They all vary from levels due to alert type
   - Clicking on the alert will reveal more detailed Information 
   - You can use this infromation to begin your remediation process.
<img width="1465" alt="Step 10 - Beginning SOC" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/cc4349bb-a7f8-4a25-ae05-1fea4814baeb">
<img width="1787" alt="Step 10a - Incident Full details" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/aa52eafd-9a24-4d9b-8cdd-63a0be603289">
<img width="1121" alt="Step 11 - Start Remediation process" src="https://github.com/MMease/SOC-in-Azure/assets/42321472/5389e2ad-a466-4ac3-8f58-c108aacfb3b2">

THIS LAB IS DONE. ENSURE ALL RESOURCES ARE DELETED TO AVOID COST ‼️‼️
