
## If the 1815w is ME (Mobility Express) 
### 1. Hard Reset
Reset 1815w through the `Recover-Config` command.  

<br>

When the Controller boots, make sure to enter `Recover-Config` on the User: prompt  
Wait for the ME to reboot and enter initial setup.

&nbsp;
---
&nbsp;

### 2. Initial Setup.
Answer the prompts provided by the AP.  
After specifying your chosen initial configurations, wait for the AP to reboot again.

> [!NOTE]
> Make sure a DHCP server is setup for the APs and WLCs to gain IP addresses.

> [!IMPORTANT]
> Make sure the DHCP server defines a Primary Controller (Option 43)

&nbsp;
---
&nbsp;

### 3. Access the GUI
Once the 1815w reboots and obtains an IP from the DHCP server, access the GUI on a browser.  
On the browser, go to `Management` > `Software Update`

<br>

![updateAP]("img/updateAP.JPG")

&nbsp;
---
&nbsp;

### 4. Upload the updated image
Upload the image, `C9800-AP-universalk9.16.12.08` via TFTP
Enable TFTP on the PC using any TFTP Server App.  

> [!NOTE]
> Make sure a proper source directory and IP binding is defined for the TFTP Server.

<br>

Now, simply wait for the AP to update and reboot.

&nbsp;
---
&nbsp;

### 5. If the C9800 is connected in the network, the AP should automatically join. 
It might do another update if the C9800 has a higher image version.

&nbsp;
---
&nbsp;

### 6. Finally, simply wait for the AP to reboot and join the controller.

<br>
<br>

---
&nbsp;

## If the 1815w is Lightweight
### Force join AP
Apply the following commands to the AP:

<br>

10.92.1.7 = MUST be YOUR Controller IP
WLC_CA = MUST be the TRUSTPOINT name of your Controller

<br>

~~~
!@AP
capwap ap primary-base WLC_CA 10.92.1.7
~~~
