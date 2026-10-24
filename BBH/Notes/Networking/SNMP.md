
Simple Network Management Protocol (SNMP) was designed to help collect information about different devices on the network. It lets you know about various network events, from a server with a faulty disk to a printer out of ink. Consequently, SNMP can hold a trove of information for the attacker. One simple tool to query servers related to SNMP is snmpcheck. You can find it on the AttackBox at the /opt/snmpcheck/ directory; the syntax is quite simple: /opt/snmpcheck/snmpcheck.rb 10.49.150.167 -c COMMUNITY_STRING.

If you would like to install snmpcheck on your local Linux box, consider the following commands.
```cmd
git clone https://gitlab.com/kalilinux/packages/snmpcheck.git
cd snmpcheck/
gem install snmp
chmod +x snmpcheck-1.9.rb
```
