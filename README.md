# **Protecting Open Ports with UFW** 

## **Background**

### **Ports**
- A **port** is a communication endpoint that allows a computer or program to connect to the Internet.
- If a computer program needs to communicate across a network, the computer will bind the program to a specific port.
- Open ports can pose security vulnerabilities, as attackers can send malicious data across them and potentially infect computers connected to a network.
- Closed ports aren't bound to a service, and cannot receive data.
- Public servers must open port 80 and 443 (HTTP and HTTPS, respectively), which means that they have to filter malicious users from genuine users.

### **Firewalls**
- A **firewall** is a device or software that filters packets that enter and leave a network. These can be used to identify suspicious traffic, log information, and drop potentially malicious packets before they reach a server.
- Firewall rules can be configured to allow only certain kinds of packets into a network.
- On Linux, the default firewall program is Uncomplicated Firewall (or UFW).
- While UFW isn't difficult to understand, it's utility should not be understated, as it can be the difference between a secure network and a compromised one.
- A secure firewall policy should deny all incoming and outgoing packets by default. Then, network admins can operate by opening only ports that they know. 

## **Objective**
- We will use UFW to configure a firewall that denies traffic from certain protocols and allows traffic from others.
- Use `ufw --help` to get a quick, simple overview of different arguments you can use with UFW.
- Picture:

## **Process**
- In Ubuntu, open a Firefox browser and navigate to any http:// website.
- Launch the terminal, and verify the status of your firewall (active/inactive) with `sudo ufw status`. If it's inactive, enable it using `sudo ufw enable`. Now, turn on logging with `sudo ufw logging on`. Now, you can check /var/log for files starting with UFW (i.e. `sudo ls /var/log/ufw*`). You'll be able to see values such as the date, time, hostname, and source/destination IP's and ports associated with your logged events.
- Now run `sudo ufw status verbose` to verify that these commands worked. You'll see a handy little table that displays the UFW status, logging status, Default (whether you are denying a sort of traffic by default) and which specific ports are denied.
- Include pic here:
- To configure UFW to deny all incoming and outgoing HTTP traffic, run `sudo ufw deny out 80` and then `sudo ufw deny in 80`. As we just mentioned, you can double check that this worked using the `status verbose` argument.
- Now, when you open Firefox, restart your http:// page. It should display this message:
- (picture)
- The applications of this go on and on - you can try the same with port 443 to deny HTTPS traffic.

## **Notes**
- Run `cat /var/log/ufw to see logs
- You can standard input your firewall rule table to a file by using `sudo ufw status verbose > /tmp/config_firewall.policy`.
- Once your firewall is enabled, try pinging 8.8.8.8. You'll notice that packets are transmitted, but none are received.
- Picture:
- A whole host of firewall policies can be implemented with this tool.
