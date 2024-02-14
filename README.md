<h1>DIY-Virtualized-Cyber-Lab</h1>
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
  <img src="https://i.imgur.com/cuYkioE.png" height="60%" width="60%" alt="WAN Interface"/>
<p><i>Enter the LAN interface</i></p>
  <img src="https://i.imgur.com/6Ca7nuy.png" height="60%" width="60%" alt="LAN Interface"/>
<p><i>This will be the ISOLATED interface</i></p>
  <img src="https://i.imgur.com/ORG9kk3.png" height="60%" width="60%" alt="ISOLATED Interface"/>
<p><i>This will be the AD_LAB interface</i></p>
  <img src="https://i.imgur.com/sVpVRXY.png" height="60%" width="60%" alt="AD_Lab Interface"/>
<br />
<img src="https://i.imgur.com/vjLHALV.png" height="60%" width="60%" alt="Y for Interface Assignment"/>

<h3>Configuring the Interfaces</h3>

<h4>Configure the LAN</h4>

<h4>Configure the Isolated LAN</h4>

<h4>Configure the AD Lab LAN</h4>

<h4>Final Check</h4>

<br />
<img src="https://i.imgur.com/Ihwuk0n.png" height="75%" width="75%" alt="Linux command line steps"/>
<br />


<img src="https://i.imgur.com/0pMs6K4.png" height="75%" width="75%" alt="Linux command line steps"/>
<br />
At the 
<br />
