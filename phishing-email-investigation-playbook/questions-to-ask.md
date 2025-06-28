# Questions to ask

## Questions to ask —&#x20;

### Gathering email artifacts:&#x20;

1. What's the sender email address?&#x20;
2. What is the display name?&#x20;
3. Is there a reply-to address? Is it different?&#x20;
4. Who are the recepients?&#x20;
5. What is the subjedt line?&#x20;
6. Date and time? When was the email sent (UTC) ? (Though it can be spoofed, it matters a lot.)&#x20;
7. What does the email body say? (Any suspicious wording?)&#x20;
8. Are there any attachments or links?&#x20;
9. What does the header say (IP, SPF/DKIM/DMARC)?&#x20;
10. What is the sending server IP? Reverse DNS?&#x20;



### Gathering file artifacts:&#x20;

1. What is the file name + extension?&#x20;
2. Is the file type consistent with its icon/label?&#x20;
3. What is the SHA256 hash of the file?&#x20;
4. What do VirusTotal, Talos say?&#x20;
5. Is there any macro, script, or payload inside?&#x20;
6. Any embedded URLs, obfuscated code, or indicators?&#x20;
7. Did the file try to connect outbound?&#x20;



### Gathering web artifacts:&#x20;

1. What is the visible vs. real URL?&#x20;
2. Is the site live? What does it do?&#x20;
3. What does `curl -I` or DevTools say about headers?&#x20;
4. What's the SSL cert look like?&#x20;
5. Whois and hosting info? CDN or proxy?&#x20;
6. What does `urlscan.io` show? Redirects?&#x20;



### Defensive measures:&#x20;

<table data-header-hidden><thead><tr><th width="304">Category</th><th>Action</th></tr></thead><tbody><tr><td>Containment</td><td>Block sender IP/domain, isolate device</td></tr><tr><td>Prevention</td><td>Update mail filters, sandbox policy</td></tr><tr><td>Detection</td><td>Add hash/URL to threat intel system</td></tr><tr><td>Awareness</td><td>Notify user base or affected team</td></tr><tr><td>Forensics</td><td>Store copy of email, logs, memory for DFIR</td></tr></tbody></table>

\


