# Safe Handling / VM Preparation

### :safety\_vest: Safe Handling Advice:

* Do not open live attachments unless in **isolated VMs or sandboxes**
* Avoid clicking URLs without sandboxing (use URLScan.io or ANY.RUN)
* Treat **all samples as if they’re dangerous**



This is **crucial** to get right. If you want to analyze phishing samples (especially those with live attachments or embedded malware), your VMs must be **properly isolated**.&#x20;

***

### **1. Disable Networking (Unless Needed)**

**Default: Keep VM networking off** unless you're specifically sandboxing with tools like `urlscan.io`, `ANY.RUN`, or redirecting traffic through an analysis proxy.

#### In VirtualBox / VMware:

* Set **Network Adapter to “Host-only” or “Internal Network”**\
  ⛔ Avoid “NAT” or “Bridged” modes unless you’re routing traffic through a **controlled gateway**

Or:

* **Manually disable the NIC inside the VM**

```bash
sudo ifconfig eth0 down
# or for newer distros
sudo ip link set eth0 down
```



### **2. Snapshot Before Analysis**

Take a VM **snapshot** right before you analyze anything:

* Easy to revert if malware makes system changes
* Protects your environment from persistence or lateral movement



### **3. Isolate from Host OS**

* Never share folders or clipboard between host and VM
* Disable drag and drop
* In VirtualBox:
  * Shared Clipboard: **Disabled**
  * Drag’n’Drop: **Disabled**



### **4. Use Separate VMs for Malware vs. Logging**

* **One VM for analysis** (e.g., opening .eml or .doc phishing files)
* **Another for logs/SIEM** (e.g., ELK or Splunk forwarder target)

This reduces the chance that malware interferes with your logging pipeline.



### **5. Monitor for Suspicious Behavior**

Run `htop`, `netstat`, or even install **Sysdig / AuditD** to watch for:

* New outbound connections
* Unusual processes (PowerShell, `/tmp/.xyz`, encoded scripts)
* File writes to suspicious paths



### **6. Safe File Handling Tips**

* Don’t open suspicious files with default apps
* Use CLI tools: `strings`, `file`, `exiftool`, `sha256sum`
* Use **sandbox-safe viewers** (like hex editors, CyberChef, or FLOSS)





### ✅ Summary Checklist

| Setting                    | Recommendation                                |
| -------------------------- | --------------------------------------------- |
| Network                    | Host-only or disabled                         |
| Clipboard/Drag'n'Drop      | Disabled                                      |
| Snapshots                  | Before every experiment                       |
| File sharing               | Disabled                                      |
| VM Tools (like Guest Add.) | Remove if not needed                          |
| Internet Access            | Only when sandboxing in controlled conditions |



## :safety\_vest: What is defanging and why do we need it?&#x20;

**Defanging** is the process of modifying malicious indicators (like URLs, IPs, or email addresses) so they can't be accidentally clicked or executed — while still keeping them readable for analysis.

#### **Example:**

* Original URL:\
  `http://malicious-site.com`
* Defanged version:\
  `hxxp://malicious-site[.]com`&#x20;



#### **Why We Need It:**

1. **Prevent Accidental Execution**\
   So no one (including you) clicks the link and infects themselves or their system.
2. **Safe Sharing**\
   You can safely paste it into reports, chats, docs, or forums without triggering security tools or firewalls.
3. **Keep It Human-Readable**\
   Analysts can still recognize and understand the indicator, even defanged.



#### Common Defanging Tactics:

| Type  | Original               | Defanged                   |
| ----- | ---------------------- | -------------------------- |
| URL   | `http://`              | `hxxp://`                  |
| Dots  | `.com`                 | `[.]com`                   |
| IP    | `192.168.1.1`          | `192[.]168[.]1[.]1`        |
| Email | `attacker@example.com` | `attacker[@]example[.]com` |



#### Tool for this: [https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/)
