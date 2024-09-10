# Day-10-Ingesting-Sysmon-and-Windows-Defender-Logs-into-Elasticsearch

Monitoring your Windows environment is crucial for maintaining security and performance. In this guide, we’ll walk through the process of ingesting Sysmon and Windows Defender logs into Elasticsearch, allowing for powerful analysis and visualization of your system’s events.

## Step 1: Configuring Integrations in Elastic GUI

1. **Navigate to the Elastic GUI** and locate the **“Add integration”** button.

2. In the search bar, type **“Custom Windows Event logs”** and select it.

3. Click **“Add custom Windows event logs”** on the next screen.

4. Provide a name for the integration (e.g., “Sysmon Logs”) and a description (e.g., “Collect logs from Sysmon”).

5. For the channel name, you’ll need to reference your Windows server:
   - Open **Event Viewer** on your Windows server.
   - Navigate to **Application and Services Logs > Microsoft > Windows > Sysmon > Operational**.
   - Right-click and select **Properties**.
   - Copy the full name provided — this is your channel name.
   - Paste this into the Elastic GUI.

6. When prompted, select your existing Windows Server as the host for these integrations.

![insert image here](image.jpg)
### Channel Name for Sysmon

7. Repeat the process for Windows Defender:
   - Create a new integration named **“Windows Defender Logs”** with an appropriate description.
   - Locate the **Windows Defender > Operational** log in Event Viewer.
   - Copy the full name from Properties and paste into Elastic.
     
![insert image here](image.jpg)
### Channel Name for Windows Defender

8. For Windows Defender, utilize the advanced options:
   - In the **Event ID** field, specify: 1116, 1117, 5001
     - **1116**: Antimalware platform detected malware or potentially unwanted software.
     - **1117**: Antimalware platform took action to protect your system.
     - **5001**: Real-time protection is disabled.

9. When prompted, select your existing Windows Server as the host for these integrations.

## Step 2: Configuring Firewall Rules

To ensure Elasticsearch can receive logs:

1. Log into your **Vultr** account.
2. Navigate to the **Networking** tab and select **Firewall settings**.
3. Add a new rule:
   - **Protocol**: TCP
   - **Port**: 9200
   - **Source**: Anywhere

## Step 3: Verifying Log Ingestion

1. In the Elastic GUI, click the **hamburger icon** and select **“Discover”**.
2. In the search bar, enter: `winlog.event_id: 1`.
   - You should now see relevant logs appearing.
     
  ![insert image here](image.jpg)
  
  ![insert image here](image.jpg)


3. To specifically check Windows Defender real-time protection status:
   - Search for: `winlog.event_id: 5001`.
   - This will display logs related to real-time protection being disabled.
     
   ![insert image here](image.jpg)

By following these steps, you’ve successfully set up log ingestion for Sysmon and Windows Defender into Elasticsearch. This setup provides a powerful foundation for monitoring and analyzing your Windows environment, enhancing your ability to detect and respond to potential security threats.

Remember to regularly review and analyze these logs to maintain a strong security posture for your systems.
