# Install IDS on a OpnSense firewall with ETPRO Telemetry ruleset

A short guide to install IDS on OPNsense. The ruleset ETPRO Telemetry only works on OpnSense. By using ETPRO Telemetry free version the user has to agree to send data to ProofPoint for research purpose. The guide will provide a real world production enviroment of IDS/IPS system

Prerequisit: Opnsense already installed <br>
Additional Documentation: https://docs.opnsense.org/manual/etpro_telemetry.html

Hardware CRC is checked disabled by default and should remain disabled as the technology is not supported by IPS <br>
[technologies ](https://docs.opnsense.org/manual/interfaces_settings.html)https://docs.opnsense.org/manual/interfaces_settings.html

# Setup

Order a free ET Pro Telementry edition: https://shop.opnsense.com/ to get the token 

<h4>Enable built in services</h4>

Go to Services -> Intruision Detection -> Administration <br>
  - make the following settings
    - Select advanced mode
    - Enable Enabled
    - Enable IPS mode
    - Enable Promiscous mode
    - Enable Enable syslog alerts
    - Change pattern matcher to Hyperscan (slightly more modern pattern matcher: https://docs.suricata.io/en/suricata-6.0.0/performance/hyperscan.html)
    - Detect Profile: Medium
    - Interface: LAN
    - Set home networks to LAN subnet

