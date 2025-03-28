<h1>Azure Honeypot Security Project</h1>

<h2>Overview</h2>
This project demonstrates the setup and monitoring of a honeypot using Microsoft Azure. The goal is to deploy a Windows 10 virtual machine as a decoy system, configure logging and monitoring with Azure Sentinel, and analyze attack data using KQL queries. This project showcases skills in cloud security, SIEM integration, and threat intelligence analysis.

<h2>Project Objectives</h2>
<li>Deploy an Azure Virtual Machine (VM) to act as a honeypot.</li>
<li>Configure network security to allow inbound traffic for threat monitoring.</li>
<li>Set up log forwarding to Azure Sentinel for security event analysis</li>
<li>Utilize KQL queries to detect and analyze malicious login attempts.</li>
<li>Enrich logs with geolocation data for better threat intelligence.</li>
<li>Visualize attack patterns using an interactive map in Azure Sentinel.</li>

<h2>Setup Azure Subscription</h2>
1. Create an Azure Subscription
   <li>Use a paid Azure subscription or join a Cyber Range.</li>
   <li>Access the Azure portal at https://portal.azure.com.</li>

<h2>Deploy the Honeypot (Azure Virtual Machine)</h2>
1. Create a Windows 10 VM
   <li> Go to Azure Portal > Virtual Machines > Create a new VM.</li>
   <li> Select an appropriate VM size based on cost and resource availability.</li>
   <li>Configure username and password.</li><br>
2. Modify Network Security Group (NSG) Settings
   <li>Allow all inbound traffic to attract potential attackers.</li><br>
3. Disable Windows Firewall
   <li>Log into the VM and disable the firewall using `wf.msc`.</li>

<h2>Monitor Unauthorized Access Attempts</h2>
1. Simulate Brute Force Attacks
   <li>Attempt 3 failed logins using a fake username (e.g., "employee").</li>
   <li>Check security logs via Event Viewer.</li>
   <li>Identify Event ID 4625 (failed login attempts).</li>

<h2> Log Forwarding and KQL Querying</h2>
1. Setup Log Analytics Workspace (LAW)<br>
2. Integrate Azure Sentinel<br>
3. Enable Windows Security Events via AMA Connector<br>
4. Run KQL Queries to Inspect Failed Login Attempts<br>
   <code>kql
   SecurityEvent
   | where EventId == 4625</code>
   

<h2>Log Enrichment with Geolocation Data</h2>
1. Create a Sentinel Watchlist for IP Geolocation
   <li>Import `geoip-summarized.csv` containing IP-to-location mappings.</li>
   <li>Define `geoip` as the watchlist name.</li><br>
2. Run KQL Query to Enrich Logs with Geolocation Data<br>
   
  <code>let GeoIPDB_FULL = _GetWatchlist("geoip");
   let WindowsEvents = SecurityEvent
     | where IpAddress == <attacker IP address>
     | where EventID == 4625
     | order by TimeGenerated desc
     | evaluate ipv4_lookup(GeoIPDB_FULL, IpAddress, network);
  WindowsEvents </code>
   

<h2>Attack Map Visualization</h2>
1. Create a Workbook in Sentinel
   <li> Remove pre-populated elements.</li>
   <li>Add a new Query element.</li>
   <li>Paste the JSON from `map.json` to visualize attack sources.</li>

<h2>Conclusion</h2>
This project demonstrates the process of setting up a honeypot in Azure, monitoring attack attempts, enriching logs with geolocation data, and visualizing threats in Sentinel. It highlights proficiency in:
<li>Azure Security Operations</li>
<li>SIEM & Log Analytics</li>
<li>KQL Querying for Threat Detection</li>
<li>Cloud Security Monitoring</li>

