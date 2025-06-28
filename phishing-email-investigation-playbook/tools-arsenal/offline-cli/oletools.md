# oletools

These are part of the **`oletools`** suite, which is essential for phishing and malware analysis, especially for **Office document macros** (`.doc`, `.xls`, `.ppt`, etc).



### Install via `pip`

```bash
sudo apt update
sudo apt install python3-pip
pip3 install oletools
```

This gives you access to:

| Tool      | Purpose                                           |
| --------- | ------------------------------------------------- |
| `oleid`   | Identifies security risks in Office files         |
| `olevba`  | Extracts and analyzes VBA macros from Office docs |
| `olemeta` | Shows metadata of OLE files                       |
| `mraptor` | Detects suspicious macro code                     |
| `rtfobj`  | Extracts embedded objects from RTF files          |



### Confirm It’s Working

```bash
oleid sample.doc
olevba suspicious_invoice.doc
```

You should see output like:

```
+----------+----------------+
| Indicator| Value          |
+----------+----------------+
| Macros   | Suspicious     |
| AutoExec | Present        |
| ...      | ...            |
```



### Optional: Upgrade&#x20;

To keep tools fresh:

```bash
pip3 install --upgrade oletools
```
