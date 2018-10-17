MOVO NETWORKING GUIDE

Important: In general, when you switch different network configurations, restart your computer and
the Movo so that all network caches are cleared.

Switching Movo onto Wifi

1. Put Movo on RLAB using the Anewkodi WiFi dongle you'll find on Movo's back. Plug this
into the USB Port behind Movo.
2. Put your computer on RLAB. You could use a WiFi dongle or just directly plug it into a
wall tap.
   2.a) If you're using WiFi, then make sure your WiFi dongle points at only one WiFi Access Point (AP).
        This will prevent it from jumping from AP to AP which increases connection latency. Use the following
        command:
3. Use the following command to add a route between RLAB's IP address space and the 10.66.171.* IP address 
space that Movo uses. `sudo route add -net 10.66.171.0 netmask 255.255.255.0 gw [movo IP on RLAB] dev [network interface]`.
The network interface and IP can be found by running ifconfig (network interface looks like eth0 or wlan3). Also, Movo has a static address on RLAB wireless: 138.16.161.10
4. Edit your ~/.bashrc file to export your ROS_IP as the IP address of your computer (on RLAB). You can find this
IP address by running ifconfig.
5. Edit your setup.sh file in the root of your movo_ws to also export the ROS_IP as the IP address of your computer
(on RLAB).



General Debugging Steps

1. Try to ping movo2. If you can't do this, either the connection is bad or DNS connecting the word 'movo2' to
the address 10.66.171.1 is not setup correctly. If it seems to be the latter, try pinging 10.66.171.1 and if that
works, you should be fine - but try to still figure out what happened to your DNS setup.
2. Try to ssh movo2. If you can ping movo2 but can't ssh it, then there is a problem on the Movo's NUC with the
ssh setup. Ideally, if you can ping movo2, you should be able to ssh it.
3. Try `rostopic list` to see if that works, then try echoing a topic like tf. If this does not work, then there is a
problem with your ROS_MASTER_URI and/or ROS_IP.
4. Check if the ROS_IP is correct. It should be the same as your computer's IP on whatever network you're on.
Symptoms of this are that you can list and echo topics, but Ein and Movo joystick control won't work.
5. Check if your ROS_MASTER_URI is correct. It should be http://movo2:11311 or http://10.66.171.1:11311.
6. Reboot your computer and the Movo to restart all ROS Nodes and clear all network caches.
