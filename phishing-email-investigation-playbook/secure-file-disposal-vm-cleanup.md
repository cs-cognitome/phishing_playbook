# Secure File Disposal / VM Cleanup

### STEP 1: Securely Dispose of the `.eml` File

You must not just delete the file — some malware or embedded exploits may persist in memory or leave behind temp artifacts.

#### Secure Deletion Command

In Kali Linux/Parrot OS:

```bash
shred -u -n 5 phishing-sample.eml
```

#### What it does:

* `shred` overwrites the file with random data **multiple times**
* `-u` removes it after shredding

Optional: Add `-n 5` to overwrite it 5 times (default is 3).

> 🛑 **Never move the sample to Trash.** Always overwrite and delete directly.

#### `wipe` (if installed)

```bash
wipe your_file.txt
```

> Parrot OS sometimes ships with `wipe`, Kali doesn't.

***



### STEP 2: Clean Temporary or Suspicious Files

#### Recommended Manual Checks:

```bash
# Check for unexpected files in temp
ls -lah /tmp

# Wipe temp
sudo rm -rf /tmp/*

# Remove bash history if needed
history -c
rm ~/.bash_history
```

#### Remove extracted payloads or created artifacts:

```bash
find . -name "*.exe" -o -name "*.vbs" -o -name "*.ps1" -delete
```





### STEP 3: Revert to Snapshot (Best Practice)

If you took a **VM snapshot before the investigation**, you now:

* Go to VMware → Snapshot Manager
* Revert to the "clean" state
* That wipes all traces — safest method

Even better if the snapshot was taken **before enabling networking** or **modifying system settings**.

***

### Optional: Full Deep Clean (No Snapshot)

If you forgot a snapshot but still want to reset VM:

#### Clean-up manually:

```bash
# Clear logs
sudo truncate -s 0 /var/log/*.log
sudo journalctl --rotate
sudo journalctl --vacuum-time=1s
```

Then reboot.

#### OR wipe & rebuild the VM:

* Export your analysis reports
* Delete and rebuild Kali/Parrot/any VM from ISO

###

### ✅ Summary: How to Finish Clean

| Task                 | Command                                   |
| -------------------- | ----------------------------------------- |
| Shred .eml safely    | `shred -u phishing-sample.eml`            |
| Clear temp + history | `rm -rf /tmp/* && history -c`             |
| Revert snapshot      | VMware Snapshot Manager                   |
| Full reset           | Reinstall Kali or restore clean VM backup |
