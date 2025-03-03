<h1>Building a SIEM</h1>

 </h2>

<h2>Description</h2>
In this task, I set up a home lab for Elastic Stack Security Information and Event Management (SIEM) using the Elastic Web portal and a Kali Linux VM, generated security events on the Kali VM, set up an agent to forward data to the SIEM, and queried and analysed the logs in the SIEM.
<br />


<h2>Part 1: Setting Up the Environment</h2>
<br />


<p>1. The first step involved logging into the Elastic cloud instance by signing up for a free account at [Elastic Cloud](https://cloud.elastic.co/). This provided access to the necessary tools for setting up and managing a SIEM.</p>


<p>2. Next, the Kali Linux VM was downloaded from the official Kali website. This VM is pre-configured with various tools used for penetration testing and security research.</p>


<p>3. A new VM was then created in VirtualBox using the downloaded Kali VM file. VirtualBox is a free and open-source hosted hypervisor for x86 virtualization.</p>

<p>4. The VM was started, and the on-screen prompts were followed to complete the Kali installation. This included setting up the system language, region, and user credentials.</p>

<p>5. Finally, the Kali VM was logged into using the default credentials (username: kali, password: kali) to begin the configuration and integration process.</p>

<p align="center">
<img src="https://imgur.com/PrC1z8D.png" height="65%" width="65%" alt=""/>
</p>

<b>Configuring the Elastic Agent</b>

<p>1.Navigated to the Integrations page in the Elastic SIEM by clicking on the Kibana main menu and selecting "Integrations" at the bottom.</p>

<p>2. Searched for "Elastic Defend" and clicked on it to open the integration page. Followed the provided instructions to install the Elastic Agent on the Kali VM. This involved downloading the agent and running installation commands on the VM.</p>

<p>3. Verification of the agent installation was done by running the command: `sudo systemctl status elastic-agent.service`. This command checks the status of the agent to ensure it is running properly and able to collect and forward logs to the SIEM.</p>

<p align="center">
<img src="https://imgur.com/Q0Tex1H.png" height="65%" width="65%" alt=""/>
</p>


<h2>Part 2: Generating and Analyzing Security Events</h2>

<b>Generating Security Events</b>

<p>1. Security events were generated using Nmap (Network Mapper) on the Kali VM to simulate network scans. Nmap is a tool used for network discovery and security auditing. Commands such as `nmap -sP 192.168.1.0/24` were executed to perform network scans and generate logs.</p>

<p align="center">
<img src="https://imgur.com/kiCBUz7.png" height="65%" width="65%" alt=""/>
</p>

<b>Querying Security Events in Elastic SIEM</b>

<p>1. The Elastic SIEM interface was opened, and the search bar at the top of the screen was used.</p>
 
<p>2. The search query `process.args: "nmap"` was entered to filter logs related to Nmap scans. This query searches for events where the action matches "nmap"</p>

<p>3. The "Search" button was clicked to execute the search query. The results of the search query were displayed in a table format below the search bar.</p>

<p>4. The three dots next to each event in the results were clicked to view more details. This provided detailed information about each security event, including timestamps, source, and destination IP addresses, and more.</p>

<p align="center">
<img src="https://imgur.com/srHkWjQ.png" height="65%" width="65%" alt=""/>
</p>


<h2>Part 3: Visualizing and Monitoring Events</h2>

<b>Creating a Dashboard</b>

<p>1. Navigated to the Elastic web portal and clicked on the menu icon at the top-left corner.</p>

<p>2. Under "Analytics," selected "Dashboards" and clicked on "Create dashboard" to start a new dashboard.</p>

<p>3. A new visualization was added by clicking "Create Visualization" and selecting "Area" or "Line" as the visualization type to represent the data graphically.</p>

<p>4. The metrics were configured to show the count of events over time by selecting "Count" as the vertical field and "Timestamp" as the horizontal field. This setup allowed for tracking the number of security events over a specific time period.</p>

<p>5. The visualization was saved by clicking on the "Save" button and added to the dashboard. This provided a visual representation of security events for easier monitoring and analysis.</p>

<p align="center">
<img src="https://imgur.com/WPSju6A.png" height="65%" width="65%" alt=""/>
</p>

<b>Creating Alerts</b>

<p>1. Navigated to the "Security" section by clicking on the menu icon and then selecting "Alerts."</p>

<p>2. Clicked on "Manage rules" at the top right of the Alerts page and then clicked on "Create new rule" to define a new alert.</p>

<p>3. The "Custom query" option was selected under the "Define rule" section, and the query `process.args: "nmap"` was entered to detect Nmap scan events.</p>

<p>4. The rule was named "Nmap Detection" and provided with a description for clarity. The severity level was also set to prioritize the alert based on its importance.</p>

<p>5. The action to be taken when the rule is triggered was configured, such as sending an email notification, creating a Slack message, or triggering a custom webhook. This ensures that appropriate actions are taken when a security event is detected.</p>

<p>6. Finally, the "Create and enable rule" button was clicked to finalize the creation of the alert. The rule was now active and monitored the logs for Nmap scan events.</p>

<p align="center">
<img src="https://imgur.com/iJCyiSJ.png" height="65%" width="65%" alt=""/>
</p>






<p>By following these steps, I successfully created a fully functional SIEM environment using the Elastic Stack, capable of generating, forwarding, analyzing, and visualizing security events, thereby enhancing my ability to monitor and respond to potential security threats effectively.</p>



<h2>Languages Used</h2>

- <b>Python:</b> Used for scripting and automating tasks within the SIEM environment. 
- <b>Bash: </b> Used for running commands and managing files on the Kali Linux VM.

<h2>Environments Used </h2>

- <b>Elastic Cloud:</b> SIEM platform for collecting, analyzing, and visualizing security events.
- <b>VirtualBox:</b> Virtualization software for running the Kali Linux VM.
- <b>Kali Linux:</b> Operating system used for penetration testing and security auditing.


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
