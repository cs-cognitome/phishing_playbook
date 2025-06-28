# Artifacts To Collect

### :e-mail: Manually: Email Artifacts To Collect  <a href="#manually-email-artifacts-to-collect" id="manually-email-artifacts-to-collect"></a>

#### How to Access Raw Headers:

* **Gmail**: More (⋮) → _Show Original_
* **Outlook Desktop**: File → Properties → Internet Headers
* **Outlook Web**: More actions (⋯) → _View > View message details_
* **Thunderbird**: View → Message Source



| Artifact                             | Where to find                                              | Purpose                                                              |
| ------------------------------------ | ---------------------------------------------------------- | -------------------------------------------------------------------- |
| **From:**                            | Email header (visible in client)                           | Check sender display name vs. actual address                         |
| **Reply-To:**                        | Email header (full/raw view)                               | May redirect responses to attacker-controlled email                  |
| **Return-Path:**                     | Raw header                                                 | Actual path for bounced emails — should match sender domain          |
| **Received:** chain                  | Full headers                                               | Shows hop-by-hop mail relay (trace true sending server)              |
| **Message-ID:**                      | Raw header                                                 | Should match domain and show consistency with sender infra           |
| **Subject:**                         | Directly in client                                         | Look for social engineering: urgency, lures, or weird topics         |
| **To:** / **CC:** / **BCC:**         | Email header or GUI                                        | Validate intended recipients and check for mass phishing             |
| **Date/Time:**                       | GUI or headers                                             | Useful for correlation and timing with other events                  |
| **MIME-Version** & **Content-Type:** | Full headers                                               | Look for malformed or suspicious content encoding                    |
| **Email body content**               | Visible in email body                                      | Grammatical errors, urgency, generic salutation, etc.                |
| **Hyperlinks (anchor tags)**         | Hover or inspect element                                   | Displayed vs. actual URL (check for mismatches or redirects)         |
| **Embedded images/media**            | Email body                                                 | Check for hidden tracking pixels or loaded from external sources     |
| **Attachments**                      | Visible in email client                                    | File type, name, extension, and size can raise red flags             |
| **SPF / DKIM / DMARC results**       | Some clients (Gmail shows in header) or via external tools | Authentication status of sender domain                               |
| **X-Originating-IP**                 | Raw headers (if present)                                   | Can reveal real client IP used to send the message                   |
| **User-agent / X-Mailer**            | Raw headers                                                | Info about client used to send the email (e.g., Outlook, PHP Mailer) |
| **Base64/Encoded content**           | Raw source                                                 | May contain hidden payloads or scripts in the body                   |
| **QR Codes**                         | Image in body                                              | Could link to malicious site — manually decode with tools            |



#### :toolbox: List of tools (to be updated)&#x20;

| Purpose                         | Tool                                                                                        | Notes                                              |
| ------------------------------- | ------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| Header parsing & SPF/DKIM/DMARC | ​[MXToolbox](https://mxtoolbox.com/EmailHeaders.aspx)​                                      | Email header analyzer, DNS tools, blacklist checks |
| Source validation & IP check    | ​[IPVoid](https://www.ipvoid.com/)​                                                         | Reputation of sender IPs, location, ASN            |
| Email reputation                | ​[Talos Intelligence](https://talosintelligence.com/)​                                      | Cisco's email/SenderBase reputation                |
| DKIM/SPF/DMARC validation       | ​[dmarcian](https://dmarcian.com/)​                                                         | Good visual parser and validation engine           |
| Raw header & MIME structure     | ​[Google Admin Toolbox: Messageheader](https://toolbox.googleapps.com/apps/messageheader/)​ | Visualizes delay paths, header fields              |
| Social/email presence           | ​[Hunter.io](https://hunter.io/) / [HaveIBeenPwned](https://haveibeenpwned.com/)​           | Check sender identity and data breach exposure     |





### :spider\_web: Manually: Web Artifacts To Collect <a href="#manually-web-artifacts-to-collect" id="manually-web-artifacts-to-collect"></a>

**Safety Tips:**

* Use **incognito** in **virtual machine**
* Block all outbound traffic with a **firewall**
* Never enter real credentials
* **Disable JavaScript** where possible (using NoScript or manual browser dev tools)&#x20;



| Artifact                              | Where to find                                                                  | Purpose                                                                  |
| ------------------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| **URL (including full path)**         | From the phishing email, browser logs, or HTTP requests                        | Core indicator; used to track the malicious site                         |
| **Domain name**                       | Extracted from URL                                                             | Used to analyze DNS records and WHOIS info                               |
| **IP address of the domain**          | `nslookup`, `dig`, browser dev tools, online DNS lookup                        | To geolocate, assess reputation, and link infrastructure                 |
| **WHOIS information**                 | `whois.domaintools.com`, `whois.net`, `whois` CLI                              | Identify domain owner, registration date, and registrar                  |
| **SSL/TLS Certificate details**       | Browser padlock → certificate info, or `crt.sh`, `censys.io`                   | Detect self-signed certs, suspicious issuance, common names (CN)         |
| **Hosting provider / ASN**            | `ipinfo.io`, `bgp.he.net`, `Shodan`, `SecurityTrails`                          | Infrastructure attribution and potential takedown route                  |
| **Page source (HTML/JS)**             | Browser → Right click → View Source, or DevTools → Network tab                 | Reveal obfuscated scripts, payloads, redirectors, form grabbers          |
| **Redirection chains**                | `httpstatus.io`, `curl -I`, browser DevTools → Network tab                     | Detect hidden forwarding to malicious pages                              |
| **Favicon hash**                      | `hashes.com`, `shodan.io/favicon`                                              | Fingerprint unique favicon to match reused phishing kits                 |
| **Open directories**                  | `https://domain.com/`, fuzz with tools like `dirb`, `gobuster`, browser access | Discover exposed files, phishing kits, or logs                           |
| **External JS/CSS/Assets URLs**       | Page source or DevTools                                                        | Trace if assets come from another malicious or compromised site          |
| **Form action destination**           | HTML source → `<form action="...">`                                            | Key indicator showing where stolen creds are sent                        |
| **Screenshots of web page**           | `urlscan.io`, `PhishTool`, `screenshotmachine.com`, browser                    | Document phishing content for evidence                                   |
| **Text content of the web page**      | Download via `wget`, browser copy, or dev tools                                | Content analysis (branding abuse, keywords, language, typos)             |
| **Typosquatting / lookalike domains** | `dnstwist`, `urlscan.io`, `whoisxmlapi`                                        | Find similar domains to map phishing campaign infrastructure             |
| **DNS records (A, MX, TXT, etc.)**    | `dig`, `nslookup`, `SecurityTrails`, `MXToolbox`                               | Analyze domain setup and possible SPF/DKIM spoofing abuse                |
| **Google Safe Browsing status**       | [transparencyreport.google.com](https://transparencyreport.google.com/)        | Check if URL is flagged by Google                                        |
| **VirusTotal URL scan**               | [www.virustotal.com](https://www.virustotal.com/)                              | Aggregate threat intelligence from multiple vendors                      |
| **Passive DNS records**               | `SecurityTrails`, `DNSDB`, `VirusTotal`, `PassiveTotal`                        | Historical IP/domain resolution — track threat actor infra reuse         |
| **Web page loading behavior**         | Browser DevTools → Network & Console tabs                                      | Observe dynamic content, JS execution, or suspicious external requests   |
| **Javascript behavior analysis**      | `jsunpack`, `any.run`, `browserflow`, manual inspection                        | Analyze for credential harvesting, beaconing, redirection                |
| **Screenshot-based similarity tools** | `PhishTank`, `urlscan.io`, `Netcraft`                                          | Identify reuse of phishing kits or visual impersonation                  |
| **Cookies & Local Storage**           | Browser DevTools → Application tab                                             | See if malicious site sets tracking cookies or stores stolen data        |
| **Referrer headers / Origin headers** | DevTools → Network tab or `curl -I`                                            | Identify if phishing site is embedded or redirected from elsewhere       |
| **JARM / TLS Fingerprints**           | `censys.io`, `shodan.io`, `jarm.tools`                                         | Fingerprint the server for correlation with other known malicious infra  |
| **Tracking pixels (web beacons)**     | DevTools → Network tab (look for 1×1 PNG/GIF/empty responses)                  | Reveal email/web tracking mechanisms used to monitor victim interaction  |
| **Console errors and warnings**       | Browser DevTools → Console tab                                                 | Identify broken or suspicious scripts, failed network calls, debug clues |







### :file\_folder: Manually: File Artifacts to Collect&#x20;

| Artifact                                  | Where to find                                                         | Purpose                                                             |
| ----------------------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **File Name**                             | File Explorer / Email client                                          | Often misleading or attention-grabbing (e.g., `Invoice_urgent.pdf`) |
| **File Extension**                        | File Explorer (enable “show extensions”)                              | Look for double extensions (`.pdf.exe`, `.docm`, `.xlsx.lnk`)       |
| **File Size**                             | Right-click → Properties                                              | Very small or very large files may be suspicious                    |
| **File Type (Magic Number)**              | `file` command (Linux) or [TrID](https://mark0.net/soft-trid-e.html)  | Check if actual file type matches extension                         |
| **Icon vs. File Type**                    | Visual inspection                                                     | A `.exe` with a PDF icon = trick                                    |
| **File Creation/Modification Timestamps** | Right-click → Properties → Details                                    | Check if they're recent or inconsistent                             |
| **Author/Company Metadata**               | Office: File → Info → Properties                                      | Check if forged, blank, or suspicious authors                       |
| **Macros Present?**                       | Open Office file → Developer tab → View Macros                        | Presence of macros in `.docm`, `.xlsm`, etc.                        |
| **Macro Warnings**                        | Office Security Warning bar                                           | File prompts to “Enable Content”? Red flag                          |
| **Embedded Objects (OLE)**                | Insert tab → Object (or unzip `.docx`)                                | Hidden files/scripts inside document                                |
| **Hyperlinks in Document**                | Right-click → Inspect / Hover                                         | Malicious links inside body of the doc                              |
| **Scripted content (VB, JS)**             | Open in text editor or inspect macros                                 | Look for obfuscated code or encoded strings                         |
| **Startup Behavior**                      | Drag `.lnk`, `.bat`, `.vbs` into Notepad                              | Check `Target` path for dropped payloads or commands                |
| **Auto-Execution Settings**               | Office Trust Center settings or file options                          | AutoOpen, AutoClose macros in Office files                          |
| **Suspicious filenames in archive files** | Open ZIP/RAR and examine each file                                    | `.exe` inside `invoice.zip` = likely payload                        |
| **Digital Signature**                     | Right-click → Properties → Digital Signatures tab                     | Unsigned or invalid = high risk                                     |
| **File hashes (MD5/SHA256)**              | `certutil -hashfile filename SHA256` (Windows) or `sha256sum` (Linux) | Use for IOC matching, VT scanning                                   |
| **Alternate Data Streams (ADS)**          | `dir /r` (Windows)                                                    | Detect hidden content in NTFS streams                               |
| **Encoded content (Base64)**              | Open in Notepad / text editor                                         | Look for `TVqQ...` (MZ header in Base64) or long encoded blocks     |
| **Filename encoding (Unicode tricks)**    | Examine in hex editor or rename                                       | Unicode spoofing (`Invoice․pdf.exe`) using homoglyphs               |

&#x20;

#### :toolbox: List of tools (to be updated)&#x20;

| Purpose                            | Tool                                                                             | Notes                                                      |
| ---------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Static file analysis               | ​[Hybrid Analysis](https://www.hybrid-analysis.com/)​                            | Upload suspicious files for deep static + behavioral check |
| Malware sandbox                    | ​[Joe Sandbox](https://www.joesandbox.com/)​                                     | Best-in-class behavioral analysis with detection breakdown |
| Obfuscation + strings + indicators | ​[Intezer Analyze](https://analyze.intezer.com/)​                                | Detects reused code, malware families                      |
| Extracts indicators, APIs, macros  | ​[PEStudio](https://www.winitor.com/)​                                           | Lightweight PE analyzer                                    |
| Analyze Office/macros              | ​[OLEVBA (from oletools)](https://github.com/decalage2/oletools)​                | Command-line, pulls VBA macros from Office docs            |
| File carving & metadata            | ​[ExifTool](https://exiftool.org/) / [TrID](https://mark0.net/soft-trid-e.html)​ | Detects hidden file types and containers                   |
| Scan with 60+ AV engines           | ​[VirusTotal](https://www.virustotal.com/)​                                      | Scan files, hashes, and URLs together (also has graph)     |



