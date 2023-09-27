
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


