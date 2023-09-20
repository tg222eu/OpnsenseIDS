# Install IDS on a OpnSense firewall with ETPRO Telemetry ruleset

A short guide to install IDS on OPNsense. The ruleset ETPRO Telemetry only works on OpnSense. By using ETPRO Telemetry free version the user has to agree to send data to ProofPoint for research purpose. The guide will provide a real world production enviroment of IDS/IPS system <br>

Prerequisit: Opnsense already installed <br><br>
Additional Documentation: <br> https://docs.opnsense.org/manual/etpro_telemetry.html <br> https://docs.opnsense.org/manual/etpro_telemetry.html

Hardware CRC is checked disabled by default and should remain disabled as the technology is not supported by IPS <br>
[technologies ](https://docs.opnsense.org/manual/interfaces_settings.html)https://docs.opnsense.org/manual/interfaces_settings.html

# Setup

<h4>Enable built in services</h4>

Go to Services -> Intruision Detection -> Administration <br>
  - make the following setting
    - Select advanced mode
    - Enable Enabled
    - Enable IPS mode
    - Enable Promiscous mode
    - Enable Enable syslog alerts
    - Change pattern matcher to Hyperscan (slightly more modern pattern matcher: https://docs.suricata.io/en/suricata-6.0.0/performance/hyperscan.html)
    - Detect Profile: Medium
    - Interface: LAN
    - Set home networks to LAN subnet

<h4>ET Pro Telementry</h4

Order a free ET Pro Telementry edition in link below to get the token. Will be used later on. The order might take some time to process, in my case around 10 min
https://shop.opnsense.com/

- The documentation says OPNsense 19.1 or higher is required for ET PRO Telementry, but it required the latest firmware update otherwise it wont install the plugin
    - Go to System ‣ Firmware ‣ Updates
    - press “Check for updates” in the upper right corner.
    - open the tab “Plugins” and search for os-etpro-telemetry
    - when found, click on the [+] sign on the right to install the plugin
<br><br>

- To download the rulesets automatically on a daily bases, you can add a schedule for this task.
    - Go to Services ‣ Intrusion Detection ‣ Administration
    - Click on the “Schedule” tab
    - A popup for the update task appears, enable it using the checkbox on top, and click “save changes”
<br><br>

- Register token and download ruleset
  - Go to Services ‣ Intrusion Detection ‣ Administration
  - Click on the “Download” tab
  - Enable all categories you would like to monitor in the “ET telemetry” section
  - paste the token code you received via email in et_telemetry.token
  - Press save to persist your token code
  - Press Download & Update rules to fetch the current ruleset

> NOTE:  
> If et_telemetry.token is missing then the plugin installation of os-etpro-telemetry was likely not successful

You can enable a schedule for daily update of the ruleset by going to Services -> Intrusion Detection -> Administration -> Schedule <BR>
Hit enable and then save
<br><br>
To check if everything went correct you can add a widget in dashboard and check for status at Lobby -> Dashboard -> Add widget -> Select "Telemetry status"

