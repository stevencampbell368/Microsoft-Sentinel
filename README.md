<h1>Microsoft Sentinel: Authentication Logins & Threat Detection</h1>

 </h2>

<h2>Description</h2>
During my Cybersecurity internship at LOG(N) Pacific, I am leveraging the authentication logs within our environment, which are generated by other interns and some threat actors on the internet. In this project, I am creating world map visualisation workbooks in Microsoft Sentinel, based on originating IP addresses. These visualisations provide a clear overview of network activity for various scenarios, such as successful logins, failed authentication attempts, and unusual login patterns. This experience is allowing me to further enhance my KQL skills, refining queries to extract valuable insights and strengthen security monitoring within Microsoft Sentinel.
</p>
The following workbooks were created to analyse and monitor different authentication scenarios effectively.
 
<br />


<h2>Use Case: Establishing a Baseline for Successful Logins</h2>

<b>Scenario:</b> As a Security Operations Centre (SOC) Analyst, I wanted to establish a baseline for normal login activity across the organisation by identifying successful authentication logins. This is crucial for detecting anomalies that may indicate compromised accounts or policy violations. By monitoring successful logins, I can identify changes in login patterns and ensure employees are accessing systems from expected locations using valid credentials.

The aim is to detect abnormal behaviours, such as logins from unexpected locations or devices, which could signal potential security risks. This baseline also supports proactive measures, like flagging unusual login patterns for further investigation.

<p align="center">
<img src="https://imgur.com/42PWvUb.png" height="65%" width="65%" alt=""/>
</p>

<b>Query Breakdown:</b> 

This query is designed to analyse successful login events, providing insights into user login activity based on location and frequency.

<p align="center">
<img src="https://imgur.com/bly2u5c.png" height="65%" width="65%" alt=""/>
</p>

- <b>SigninLogs:</b> This is where all login activity is stored, including details of each login attempt.
- <b>Where ResultType == 0:</b> This filters the data to show only successful logins, as ResultType == 0 indicates a successful login.
- <b>Summarize LoginCount = count():</b> Counts the number of successful logins for each user, grouped by their login location (e.g., city, country).
- <b>Project:</b> The project operator is used to select and display specific columns from the query results, (e.g., Identity, Latitude, Longitude, City, Country, and LoginCount for each login event.
<br />

<b>Recommended Actions:</b> 
</p>

Monitor Regular Login Patterns
- Establish a baseline of normal login activity (e.g., time of day, location, and frequency).
- Identify typical login locations for each user.

</p>

Set Up Anomaly Detection Alerts
- Configure alerts for logins from unusual locations or devices.
- Use behavioral analytics to detect deviations from established login patterns.

<br />


<h2>Use Case: Identifying Unsuccessful Authentication Logins</h2>

<b>Scenario:</b> I wanted to track unsuccessful authentication logins across the organisation to help identify potential security threats, such as brute force attacks or compromised credentials. Monitoring these failed logins is important to detect unusual activity early, allowing for timely investigation and prevention of unauthorised access.

By tracking patterns of failed logins, this query helps the organisation stay proactive in securing sensitive data and maintaining overall security.

<p align="center">
<img src="https://imgur.com/YzawmmM.png" height="65%" width="65%" alt=""/>
</p>

<b>Query Breakdown:</b> 

This query is designed to analyse unsuccessful login events, helping to identify and investigate potential security threats based on failed login attempts.

<p align="center">
<img src="https://imgur.com/omOfr3w.png" height="65%" width="65%" alt=""/>
</p>

- <b>SigninLogs:</b> This is where all login activity is stored, including both successful and unsuccessful login attempts.
- <b>Where ResultType != 0:</b>  Filters the data to show only unsuccessful logins, as any result other than 0 indicates a failed login attempt.
- <b>Summarize LoginCount = count():</b> Counts the number of failed login attempts for each user, grouped by their login location (e.g., city, country).
- <b>Project:</b> The project operator selects and displays specific columns from the query results (e.g., Identity, Latitude, Longitude, City, Country, and LoginCount for each failed login event).
<br />


<b>Recommended Actions:</b> 
</p>

Investigate Frequent Failed Logins
- Identify users or IP addresses with multiple failed logins.
- Determine if failed attempts originate from internal or external networks.
</p>

Implement Account Lockout Policies
- Enforce temporary account lockouts after a set number of failed attempts.
- Configure adaptive authentication to challenge high-risk logins.
</p> 
  
Enable Multi-Factor Authentication (MFA)
- Require MFA for all users, especially for remote and privileged access.
- Implement passwordless authentication methods (e.g., biometrics) to enhance security and reduce reliance on passwords.

<br />



<h2>Use Case: Identifying Unauthorised Login Attempts Outside Gloucester and London Offices</h2>

<b>Scenario:</b> A cybersecurity consulting firm and managed services provider based in Gloucester, UK, with an additional office in London, UK, allows flexible work arrangements but enforces strict location-based access controls. While there is no formal on-site work policy, logging in from outside the UK is restricted to prevent unauthorised access, data breaches, and compliance violations.

By detecting logins from unexpected international locations, the firm ensures that only authorised users access company systems, reducing the risk of security threats and potential policy violations. 

The goal is to flag and investigate any login attempts originating from outside the UK to maintain security and compliance.

<p align="center">
<img src="https://imgur.com/4K70i2z.png" height="65%" width="65%" alt=""/>
</p>

<b>Query Breakdown:</b> 

This query identifies and flags successful login attempts from locations outside the company's designated offices in London and Gloucester.

<p align="center">
<img src="https://imgur.com/fc2XDGG.png" height="65%" width="65%" alt=""/>
<br />

- <b>SigninLogs:</b> This table stores all login activity, including both successful and unsuccessful login attempts.
- <b>Where ResultType == 0:</b> Filters the data to include only successful logins, focusing on valid login events.
- <b>Extend City = tostring(LocationDetails["city"]):</b> Creates a new column to extract the city from the login location details.
- <b>Where City !in ("London", "Gloucester"):</b> Excludes logins from London and Gloucester, identifying logins from any other locations.
- <b>Summarize LoginCount = count():</b> Counts the number of successful logins from unauthorised locations.
- <b>Project:</b> The project operator selects and displays specific columns (e.g., Identity, Latitude, Longitude, City, Country, and LoginCount for each login event from unauthorised locations).
<br />

<b>Recommended Actions:</b> 
</p>

Enforce Geolocation-Based Access Controls
- Block login attempts from outside Gloucester and London.
- Use Conditional Access policies to restrict logins by location.

</p>

Monitor & Investigate Unauthorised Logins
- Flag login attempts from outside designated office locations.
- Verify with the user if travel was authorised or expected.
</p> 
  
Alert IT & Security Teams
- Generate real-time alerts for logins from unauthorised locations.
- Investigate any anomalies to determine potential threats.

<br />







<h2>Use Case: Identifying High-Risk Failed Authentication Attempts</h2>

<b>Scenario:</b> In a cybersecurity consulting and managed services firm, monitoring failed authentication attempts is vital for detecting potential security threats like brute force attacks or credential stuffing. Identifying users with more than five failed logins helps spot suspicious activity early and take preventative measures.

<p align="center">
<img src="https://imgur.com/agmROQY.png" height="65%" width="65%" alt=""/>
</p>


<b>Query Breakdown:</b>

This query focuses on failed login attempts and flags users with excessive failures, indicating potential malicious attempts to access sensitive systems.

<p align="center">
<img src="https://imgur.com/tTYm4UK.png" height="65%" width="65%" alt=""/>
</p>

- <b>SigninLogs:</b> This table stores all login activity, including both successful and unsuccessful login attempts.
- <b>Where ResultType != 0:</b>  Filters the data to show only unsuccessful logins, as any result other than 0 indicates a failed login attempt.
- <b>Summarize LoginCount = count():</b> Counts the number of failed login attempts for each user, grouped by their login location (e.g., city, country).
- <b>Where LoginCount > 5:</b>  Filters the results to show only users who have had more than five failed login attempts, flagging those with unusually high numbers.
- <b>Project:</b> The project operator selects and displays specific columns from the query results, such as Identity (user), Latitude, Longitude, City, Country, and LoginCount.
<br />

<b>Recommended Actions:</b> 
</p>

Flag & Investigate High-Failure Accounts
- Identify users with repeated failed logins (>5 attempts).
- Determine if login attempts originate from different locations or devices.

</p>

Automate Account Lockout for High-Failure Attempts
- Lock accounts after multiple failed login attempts.
- Verify with the user if travel was authorised or expected.
</p> 
  
Monitor for Brute Force or Credential Stuffing Attacks
- Detect patterns of rapid, repeated login failures.
- Cross-reference login failures with threat intelligence feeds.

<br />





By creating these use cases and scenarios, I successfully developed a comprehensive set of world map visualisation workbooks using Microsoft Sentinel, which allows for the visualisation of authentication events, including successful logins, failed attempts, and abnormal login patterns. This enhances my ability to monitor and respond to network activity effectively. Additionally, I’ve added KQL to my query toolbelt, enabling me to explore and experiment with different aspects of the data to improve security monitoring and analysis.


</p>


<h2>Languages Used</h2>

- <b>KQL (Kusto Query Language):</b> Used to query and analyse authentication logs within Microsoft Sentinel to extract meaningful insights. 
- <b>JSON: </b> Used for formatting and parsing data within workbooks for map visualisation.
    

<h2>Environments Used </h2>

- <b>Microsoft Sentinel:</b> Security information and event management (SIEM) platform for collecting, analysing, and visualising authentication logs and security events.
- <b>Azure:</b> Cloud platform used to integrate and manage resources for the authentication log data.
- <b>Azure Log Analytics:</b> Used for testing and refining KQL queries, helping to ensure accurate data collection and analysis.

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
