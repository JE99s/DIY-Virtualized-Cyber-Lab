<h1>DIY Virtualized Cyber Lab</h1>
<h2>Description</h2>

<p>I'll walk you through my process of creating a virtual environment to hone technical skills. It can be done via VBox or VMware. I'll be utilizing VirtualBox for this project.
  
This can be run on both a desktop or laptop. Your daily-use computer (laptop) can run labs and it could be a mobile security lab.
</p>

<br />

<img src="https://i.imgur.com/ONUVZPC.png" height="80%" width="80%" alt="Cyber lab Concept"/>
<h2>Utilities Used</h2>

- <b>VirtualBox Hypervisor</b>
- <b>pfSense ISO file</b>
- <b>Kali Linux Offensive VM</b>
<h2>Environments Used</h2>
- <b>Windows 10 Host Machine </b>
<br />
<h3>Recommended System Specifications & Configurations</h3>

-  <b>Multithreaded CPU with Virtualization Support</b>
-  <b>At least 16GB RAM - 32GB would be better</b>
- <b>Plenty of free disk space interally or externally (Regarding externally, I highly recommend External SSDs)</b>
<br />
<p>It's vital ensure that virtualization is enabled on your host system, mostly likely in the BIOS. </p>
<h2>Walk-through:</h2>
On my host machine, I will start with establishing the proper network segmentation for the virtual environment. I need to create a pfSense Virtual Machine (VM) so it can act as a firewall between the different virtual networks that will soon be created.
<br />
<h3>Intstall Virtual Box</h3>
<p>To download the Virtualbox installer for your host OS, navigate to their downloads <a href="https://www.virtualbox.org/wiki/Downloads">page</a>.
You'll see a list of downloads based on the host OS. At the time of sharing my journey, the latest version was <b>7.0.14</b>. </p>
<br />
<img src="https://i.imgur.com/GFoQLeu.png" height="35%" width="35%" alt="VBox Installer Version"/>
- If downloading for <b><ins>Windows</ins></b>, click <i>Windows hosts</i>.
- If downloading for <b><ins>Mac OS</ins></b>, click <i>OS X hosts</i>.
- If downloading for <b><ins>Linux</ins></b>, click <i>Linux distributions</i> and follow the instructions. You can download via an <b>.rpm</b> or <b>.deb</b> package, or you can install using your package manager such as <b>yum</b> or <b>apt</b>.
<br/>
<h3>Install the VirtualBox Extension Pack</h3>
<p>Once you've installed VirtualBox, it is recommended o add the extension pack for better VM support and functionality.</p>
<img src="https://i.imgur.com/RezKGaS.png" height="35%" width="35%" alt="VBOX Extension Pack"/>
<br />
<p>You can download the extension pack file. Once you open the file, VirtualBox should be the default file handler and install the the extension pack</p> <br />
<p><b><i>***NOTE: You must reinstall the extension pack any time you update your VirtualBox!***</i></b>
</p>
  
<h3>Virtual Box Guest Additions</h3>
<p>Virtual Guest Additions are additional pieces of software that can be installed <b><ins>inside the the VM</ins></b>, to have the machine run more smoothly inside VBox.</p>

<p>For example, sometimes you may have a VM that has poor screen resolution, the screen doesn't resize, or some other strange issues. You may need to install the VirtualBox Guest Additions drivers to help the VM run more smoothly. </p>
<br />
<p>Whenever you are creating a lab - whether in the cloud or on prem. - the network should always be planned out first. Future growth should be factored in as well. It's much more difficult to change network design later than planning for it now.</p>

  <p>⚠️
pfSense is acting as the NAT router and firewall for the lab environment. Therefore, <b><ins>pfSense will need to be the first VM to boot</ins></b> when running your lab. After pfSense boots, you can start your other VMs.</p>

<h3>Download pfSense</h3>
<p>Go to: https://www.pfsense.org/download/ and choose the image with the following specifications:

- AMD64
- ISO installer
- Choose the mirror closest to you</p>
<img src="https://i.imgur.com/ir1dIls.png" height="50%" width="50%" alt="VBOX Extension Pack"/>
<p>Now, go to the <b><ins>folder where you downloaded pfSense.</ins></b> We need to extract the <b>.iso</b> file from the archive. To make extracting easier I have <a href="https://www.7-zip.org/">7zip</a> installed. It can be some other archive extraction utility to decompress this <b>.gz</b> archive.

Once extracted, we should now have a <b><i>pfSense-CE-#.#.#-RELEASE-amd64.iso</i></b> file in the folder.</p>
<h3>VBox Configurations For PfSense VM</h3>
<p>Now the pfSense VM needs to be created. I open VirtualBox and click the <b>New</b> button</p>
<img src="https://i.imgur.com/TlIcvL6.png" height="5%" width="5%" alt="VBOX New Button"/>
<p>The <b><ins>Name</ins></b> and <b><ins>Machine Folder</ins></b> are specific to your computer. Ensure you choose the correct <b><ins>Type</ins></b> and <b><ins>Version</ins></b> as shown below:</p>
<img src="https://i.imgur.com/UEvd86q.png" height="80%" width="80%" alt="pfSense VM Name and Operating System"/>
<br />
<img src="https://i.imgur.com/5SDYiFM.png" height="75%" width="75%" alt="pfSense VM Hardware"/>
<br />
<br/>
<img src="https://i.imgur.com/i7x3e7S.png" height="55%" width="55%" alt="pfSense VM Virtual Hard Disk"/>
<br />
<br/>
<img src="https://i.imgur.com/Jx02MZv.png" height="55%" width="55%" alt="Configuration Summary"/>
❗ <b>Do not start the VM yet!</b>
<br/>
<h3>Customize the PfSense VM</h3>
<p>Right-click  the VM and choose <b>Settings</b>
Move <b>Hard Disk</b> above <b>Optical</b> and disable <b>Floppy</b></p>
<figure>
  <img src="" height="7%" width="7%" alt="Order of hard disk, optical, and floppy"/>
  <figcaption>This boot order ensures the operating system boots upon installation from disc</figcaption>
</figure>
<br />

<br />

Disable audio

Disable USB
<br />
<h3>Configure the Network Interfaces</h3>
<h4>Adapter 1: WAN</h4>
<img src="https://i.imgur.com/7tHDA26.png" height="60%" width="60%" alt="VM Network Settings, Adapter 1"/>

<br />
<h4>Adapter 2: LAN</h4>
<img src="https://i.imgur.com/L9aarW1.png" height="60%" width="60%" alt="VM Network Settings, Adapter 2"/>
<br />
<h4>Adapter 3: ISOLATED</h4>
<img src="" height="60%" width="60%" alt="VM Network Settings, Adapter 3"/>
<br />
<h4>Adapter 4: AD_LAB (Active Directory)</h4>
<img src="https://i.imgur.com/HFaLYzi.png" height="60%" width="60%" alt="VM Network Settings, Adapter 4"/>
<br />
<b>All done</b>. Click <b>OK.</b>
<br />
<h3>Installing pfSense</h3>
Let's go ahead and start the machine.
<img src="https://i.imgur.com/KcHMOd4.png" height="6%" width="6%" alt="VBOX Start Button"/>
<br />
If it asks for the startup disk, just choose the <b>.iso</b> disk (file) we downloaded earlier. Press <b>Enter.</b>
<img src="https://i.imgur.com/XYiM39t.png" height="80%" width="80%" alt="pfSense copyright agreement box"/>
<br />
Choose <b>Install pfsense</b>
<br/>
<img src="https://i.imgur.com/KyXJJRM.png" height="80%" width="80%" alt="Choose install pfSense"/>
<br/>
<p>Choose <b>Auto (ZFS)</b></p>
<img src="https://i.imgur.com/uIbtI1X.png" height="80%" width="80%" alt="Auto (ZFS)"/>
<br />
<p>Proceed with Installation using the defaults</p>
<img src="https://i.imgur.com/V7gzcRj.png" height="80%" width="80%" alt="Proceed with installation via defaults"/>
<br />
<p>Stripe - No Redundancy</p>
<img src="https://i.imgur.com/9HEA25C.png" height="80%" width="80%" alt="Stripe - No Redundancy"/>
<br />
<p>Use the <b><i>Space Bar</i></b> such that an <b><i>*</i></b> (asterisk) denotes the selected disk.</p>
<img src="https://i.imgur.com/vML4at9.png" height="80%" width="80%" alt="Asterisk *"/>
<br />
<p>Use your arrow keys to select <b>YES</b> and proceed.</p>
<img src="https://i.imgur.com/hFq71Qc.png" height="80%" width="80%" alt="Yes to proceed"/>
<br />
<p>Wait for installation process to complete...</p>
<img src="https://i.imgur.com/vj7xiUi.png" height="80%" width="80%" alt="Wait for installation to complete"/>
<br />
<p>Choose <b>Reboot</b></p>
<img src="https://i.imgur.com/3exk4x3.png" height="80%" width="80%" alt="Reboot for pfSense installation"/>
<br />


<h3>Configurations Inside pfSense</h3>
<p>Wait for the VM to finish booting. When asked <b><i>Should VLANs be set up now [y|n]?</i></b>, choose <b><i>n</i></b>.</p>

<p><i>Enter the WAN interface</i></p>
  <img src="https://i.imgur.com/cuYkioE.png" height="65%" width="65%" alt="WAN Interface"/>
<p><i>Enter the LAN interface</i></p>
  <img src="https://i.imgur.com/6Ca7nuy.png" height="65%" width="65%" alt="LAN Interface"/>
<p><i>This will be the ISOLATED interface</i></p>
  <img src="https://i.imgur.com/ORG9kk3.png" height="65%" width="65%" alt="ISOLATED Interface"/>
<p><i>This will be the AD_LAB interface</i></p>
  <img src="https://i.imgur.com/sVpVRXY.png" height="65%" width="65%" alt="AD_Lab Interface"/>
<br />
<img src="https://i.imgur.com/vjLHALV.png" height="60%" width="60%" alt="Y for Interface Assignment"/>

<h3>Configuring the Interfaces</h3>

<p>
  - The WAN interface should pull an IP address from your home network
  - The Default LAN IP address space is 192.168.1.1/24
  - OPT1 (optional interface 1) - Isolated - is not yet configured
  - OPT2 (optional interface 2) - AD_LAB - is not yet configured
</p>
<img src="https://i.imgur.com/k7V33EZ.png" height="65%" width="65%" alt="Configuring Interfaces"/>

<h4>Configure the LAN</h4>
<img src="https://i.imgur.com/LcanRFk.png" height="65%" width="65%" alt="Enter option 2"/>
Enter option 2 to set the IP address for the interface. Enter option 2 once againt for the LAN interface.
<br />
<p>Enter 'n' to configure the address statically</p>
<img src="https://i.imgur.com/fp8z3SG.png" height="65%" width="65%" alt="Enter 'n' to configure the address statically"/>
<br/ >
<p>Enter the network address and subnet mask bits</p>
<img src="https://i.imgur.com/b1VOEaY.png" height="65%" width="65%" alt="Enter the network address and subnet mask bits"/>
<br />
<p>Press Enter here, this is a LAN.</p>
<img src="https://i.imgur.com/ZZFgnoP.png" height="65%" width="65%" alt="Press enter here this is a LAN."/>
<br />
<p>Enter 'n' as to configure the address statically</p>
<img src="https://i.imgur.com/UM1UIuI.png" height="65%" width="65%" alt="'n' to config the address statically"/>
<br />
<p>Press Enter. We will not be using IPv6</p>
<img src="https://i.imgur.com/GuZj4vs.png" height="65%" width="65%" alt="no IPv6"/>
<br />
<p>Enter y to enable the DHCP server</p>
<img src="https://i.imgur.com/Yg2nppF.png" height="65%" width="65%" alt="enable DHCP server"/>
<br />
<p>Enter the start and end range</p>
<img src="https://i.imgur.com/OrDAhDB.png" height="65%" width="65%" alt="IP address range for DHCP server"/>
<br />
<p>Enter n, we want to keep using TLS on the web portal</p>
<img src="https://i.imgur.com/CSvLJNl.png" height="65%" width="65%" alt="n, want to keep using TLS on web portal"/>
<br />
<img src="https://i.imgur.com/NnYohO7.png" height="69%" width="69%" alt="Done with LAN"/>
<p>Press Enter. ALl done with the LAN interface</p>

<h4>Configure the Isolated LAN</h4>
<img src="https://i.imgur.com/OaOI2Hn.png" height="65%" width="65%" alt="Enter option 2 & 3"/>
Enter option 2 to set the IP address for the interface. Enter option 3 to configure the OPT3 interface.
<br />
<p>Enter 'n' to configure the address statically</p>
<img src="https://i.imgur.com/WRb6oW5.png" height="65%" width="65%" alt="Enter 'n' to configure the address statically"/>
<br/ >
<p>Enter the network address and subnet mask bits</p>
<img src="https://i.imgur.com/RHfMAKi.png" height="65%" width="65%" alt="Enter the network address"/>
<img src="https://i.imgur.com/YT2GbUB.png" height="65%" width="65%" alt="Enter subnet mask bits"/>
<br />
<p>Press Enter here, this is a LAN.</p>
<img src="https://i.imgur.com/FBfEjMM.png" height="65%" width="65%" alt="Press enter here this is a LAN."/>
<br />
<p>Enter 'n' as to configure the address statically</p>
<img src="https://i.imgur.com/igSHmLG.png" height="65%" width="65%" alt="'n' to config the address statically"/>
<br />
<p>Press Enter. We will not be using IPv6</p>
<img src="https://i.imgur.com/o4ugWBs.png" height="65%" width="65%" alt="no IPv6"/>
<br />
<p>Enter y to enable the DHCP server</p>
<img src="https://i.imgur.com/RNPDASm.png" height="65%" width="65%" alt="enable OPT1 DHCP server"/>
<br />
<p>Enter n, we want to keep using TLS on the web portal</p>
<img src="https://i.imgur.com/CSvLJNl.png" height="65%" width="65%" alt="n, want to keep using TLS on web portal"/>
<br />
<img src="https://i.imgur.com/oQA9JlU.png" height="69%" width="69%" alt="Done with LAN"/>
<p>Press Enter. ALl done with the ISOLATED LAN interface</p>

<h4>Configure the AD Lab LAN</h4>
<img src="https://i.imgur.com/RkghfDX.png" height="65%" width="65%" alt="Enter option 2 & 4"/>
Enter option 2 to set the IP address for the interface. Enter option 4 to configure the OPT4 interface.
<br />
<p>Enter 'n' to configure the address statically</p>
<img src="https://i.imgur.com/iuUeLv0.png" height="65%" width="65%" alt="Enter 'n' to configure the address statically"/>
<br/ >
<p>Enter the network address and subnet mask bits</p>
<img src="https://i.imgur.com/1adL7Vm.png" height="65%" width="65%" alt="Enter the network address"/>
<img src="https://i.imgur.com/kXrocwo.png" height="65%" width="65%" alt="Enter subnet mask bits"/>
<br />
<p>Press Enter here, this is a LAN.</p>
<p>Enter 'n' as to configure the address statically</p>
<img src="https://i.imgur.com/7TmJykc.png" height="65%" width="65%" alt="'n' to config the address statically"/>
<br />
<p>Press Enter. We will not be using IPv6</p>
<img src="https://i.imgur.com/sVh8Cso.png" height="65%" width="65%" alt="no IPv6"/>
<br />
<p>Enter n to disable the DHCP server, as the domain controller wil be acting as the DHCP server</p>
<img src="https://i.imgur.com/lvfy1Gy.png" height="65%" width="65%" alt="disable OPT4 DHCP server"/>
<br />
<p>Enter n, we want to keep using TLS on the web portal</p>
<br />
<p>Press Enter. All done with the AD_LAB interface</p>

<h3>Final Check</h3>
<p>You should now see something like this</p>
<img src="https://i.imgur.com/asnfjxa.png" height="70%" width"70%" alt="Final check"/>
<br />
<h4>One thing to Note</h4>
<p><b><ins>I will not</ins></b> be making the pfSense web console available from the WAN. This is because you may find yourself using a laptop and if you connect to public wireless networks, then your pfSense web console would be open to other on that network. We will us the Kali VM to configure the pfSense firewall rules shortly, but first...</p>

<h3>Importing Kali Linux VM Into Lab</h3>
<p>Go to https://www.kali.org/get-kali/</p>
<img src="https://i.imgur.com/Jy2f1gz.png" height="70%" width="70%" alt="Kali Linux VM information"/>
<br />
<p>Click <i>Virtual Machines</i> and ensure to download the VM that correlates to the VirtualBox 64-bit download icon</p>
<img src="https://i.imgur.com/wuSn51f.png" height="70%" width="70%" alt="Kali Linux VM VBox download icon"/>
<br />
<p>It's a big file, so you might have to wait a bit for the download to complete. Make sure that VirtualBox is open. Extract the <b>.7z</b> file to unarchive the <b>.vbox</b> and <b>.vdi</b> files. Rename the folder containing the VM files. Select the folder and move to a preferred location where you keep your VirtualBox VMs (e.g., alongside the pfSense VM).</p>

<p>Click 'Tools' to add a VM</p>
<img src="https://i.imgur.com/K1d0MZn.png" height="7%" width="7%" alt="VirtualBox Add VM button"/>
<br />
<p>Choose you Kali VM's <b>.vbox</b> file</p>
<h4>❗ Do not start the VM yet</h4>
<p>Right-click the Kali and choose <b>Settings</b>.</p>
<img src="https://i.imgur.com/kSJXHYB.png" height="60%" width="60%" alt="settings > Network Kali"/>
<p>⚠️  <b><ins>Attach the Kali VM to the pfSense LAN</ins></b></p>
<img src="" height="60%" width="60%" alt="Attach kali to LAN"/>
<p>You may also wish increase the RAM in the <b>System</b> settings, but that is your choice to make based on available resources. Next, click <b>OK</b>. Now start the Kali VM. The default credentials are:

- Username: <b>kali</b>
- Password: <b>kali</b></p>
<img src="https://i.imgur.com/huRsrUv.png" height="60%" width="60%" alt="Kali VM login screen"/>
<p>Please change the password promptly. Additionally, we can check in the terminal to ensure we're (connected to) on the LAN interface. We have the IP address <b>10.0.0.11</b> from the DHCP server on pfSense.</p>
<img src="https://i.imgur.com/CKxjiN0.png" height="70%" width="70%" alt="Kali IP address"/>

<h3>Configuring the pfSense Firewall</h3>
<p>On the Kali Linux VM, open your browser and navigate to: <b>https://10.0.0.1</b>. Click <b>Advanced</b> to accept the risk sand continue.</p>
<img src="https://i.imgur.com/AHxNyzS.png" height="70%" width="70%" alt="Websearch 10.0.0.1"/>
<img src="https://i.imgur.com/XNq71vu.png" height="70%" width="70%" alt="Accept the Risk and Continue"/>
<br />
<img src="https://i.imgur.com/6MZdP0O.png" height="70%" width="70%" alt="pfsense login page"/>
<p>The default credentials are:
  
- Username: <b>admin</b>
- Password: <b>pfsense</b>

Click <b>Next</b></p>
<img src="https://i.imgur.com/eon9LIU.png" height="70%" width="70%" alt="Welcome to pfSense software"/>
<p>Click <b>Next</b> (again). Fill out the <b>Hostname and Domain</b>. <b><ins>Uncheck</ins> Override DNS</b>. Click <b>Next</b>.</p>
<img src="https://i.imgur.com/Xh9K4jK.png" height="70%" width="70%" alt="Override DNS"/>
<p>Double check your <b>timezone</b> and click <b>Next</b>.</p>
<img src="https://i.imgur.com/9J1pRRJ.png" height="70%" width="70%" alt="Timezone"/>
<p>Scroll down and <b>uncheck this box</b>. We're double-NAT, which means that the WAN network is also a private network, so we want to allow this. Click <b>Next</b>.</p>
<img src="https://i.imgur.com/xKyqfsu.png" height="70%" width="70%" alt="Block RFC...Private Networks"/>
<p>Leave this alone. Click <b>Next</b>.</p>
<img src="https://i.imgur.com/oBYrtBq.png" height="70%" width="70%" alt="Configure LAN interface page"/>
<p>Change the admin password. <b><ins>Save it in a password vault.</ins></b> Click next.</p>
<img src="https://i.imgur.com/ZGEvxiH.png" height="70%" width="70%" alt="Change admin password"/>
<p>Click <b>Reload</b>and wait for the web configurator to refresh. Click <b>Finish</b>.</p>

<h3>Configure the Intefaces</h3>
<h4>Isolated Interface</h4>
<p>Choose OPT1</p>
<img src="https://i.imgur.com/DDVR9tr.png" height="25%" width="25%" alt="Choose OPT1"/>
<p>Set the <b>Description</b> to <b><i>Isolated</i></b>. Scroll down and click <b>Save</b> and <b>Apply Changes</b>.</p>
<img src="https://i.imgur.com/UC9otEW.png" height="60%" width="60%" alt="Isolated description"/>
<h4>AD_LAB Interface</h4>
<p>Choose OPT2</p>
<p>Set the Description to <b>AD_LAB</b>. Scroll down and click <b>Save</b> and <b>Apply Changes</b>.</p>
<img src="https://i.imgur.com/xKtTAYb.png" height="25%" width="25%" alt="Select OPT2"/>
<img src="https://i.imgur.com/zsTkvdP.png" height="60%" width="60%" alt="AD_LAB Description"/>
<h3>Optimize the DNS Resolver Service</h3>
<p>Go to <b>Services > DNS Resolver</b></p>
<img src="https://i.imgur.com/XG23H4M.png" height="25%" width="25%" alt="Choose DNS Resolver"/>
<p>Check these boxes, click <b>save</b> and <b>apply changes</b>.</p>
<p>⚠️  <b><ins>Note: Jan 1, 2024</ins></b>

Netgate is pushing people to the Kea DHCP daemon, as they're drepecating the ISC DHCP daemon. If you opt to move to the Kea DHCP daemon, these options will not be available. You will need to switch back to ISC DHCP, make your desired selections, then switch back to Kea DHCP.

https://www.reddit.com/r/PFSENSE/comments/17z1u6f/dhcp_registration_on_dns_resolver/</p>
<br />
<img src="https://i.imgur.com/RX9zYzA.png" height="60%" width="60%" alt="Check DHCP reg. & Static DHCP"/>
<p><b><ins>Still under DNS Resolver</ins></b>, go to <b>Advanced Settings</b>. Check both of these boxes. Click <b>save</b> and <b>apply changes</b>.</p>
<img src="https://i.imgur.com/AmgQ5JK.png" height="60%" width="60%" alt="Check Prefetch support & Prefetch DNS key support"/>

<h3>Give Kali a Static DHCP Lease</h3>
<p>Go to <b>Status > DHCP Leases</b></p>
<img src="https://i.imgur.com/jOudyfq.png" height="25%" width="25%" alt="Select DHCP Leases"/>
<img src="https://i.imgur.com/O28TkPS.png" height="60%" width="60%" alt="Click on the button to add a static mapping & Change Kali IP address to 10.0.0.2"/>
<p>Click <b>Save</b> and <b>Apply Changes</b>.</p>

<h3>Congifure the Firewall Rules</h3>
<h3>Make Some System Tweaks to pfSense</h3>
<p>Go to <b>System > Advanced</b></p>
<img src="https://i.imgur.com/xMnwhbn.png" height="25%" width="25%" alt="Choose System > Advanced"/>
<p>Go to <b>Networking</b></p>
<img src="https://i.imgur.com/fTrbtob.png" height="25%" width="25%" alt="Networking"/>
<p>Scroll down and <b><ins>check this box</ins></b></p>
<img src="https://i.imgur.com/SyvblzE.png" height="60%" width="60%" alt="Check Hardware Checksum Offloading box"/>
<p>Click Save and Apply Changes. Click Reboot and reboot now.</p>
<p>⚠️  Wait for pfSense to come back up before proceeding</p>
<br />
<h3>Grab Kali's New DHCP Reservation</h3>
<p>Log into your Kali VM and open a terminal. Run the command as pictured below.</p>
<img src="https://i.imgur.com/eQw3I6s.png" height="60%" width="60%" alt="Kali Linux command to reset IP address"/>
<p>Your IP address should now be <b>10.0.0.2</b> as configured.</p>
<img src="https://i.imgur.com/lDLqgqz.png" height="60%" width="60%" alt="Configured Kali IP address"/>
