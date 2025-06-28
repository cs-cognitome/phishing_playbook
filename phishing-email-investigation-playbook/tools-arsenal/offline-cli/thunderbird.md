# thunderbird

1. Download from the official website: [https://www.thunderbird.net/en-GB/thunderbird/all/](https://www.thunderbird.net/en-GB/thunderbird/all/)

<div align="left"><figure><img src="../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure></div>

2. Unpack it&#x20;

```bash
tar -xjf thunderbird-*.tar.bz2
```



3. Put it somewhere tidy&#x20;

{% code overflow="wrap" %}
```bash
sudo mv thunderbird /opt/thunderbird
sudo ln -s /opt/thunderbird/thunderbird /usr/local/bin/thunderbird   # now “thunderbird” works anywhere
```
{% endcode %}

What does this line do: `sudo ln -s /opt/thunderbird/thunderbird /usr/local/bin/thunderbird`&#x20;

* **`ln`** – the Unix “link” command.
* **`-s`** – tells it to create a _symbolic_ link (sort of the shortcut).
* **`/opt/thunderbird/thunderbird`** – the _target_: the real Thunderbird executable we unpacked in

&#x20;`/opt`.

* **`/usr/local/bin/thunderbird`** – the _link name_: where the shortcut will live.



4. Add a desktop icon (one-liner)

```bash
cat > ~/.local/share/applications/thunderbird.desktop <<'EOF'
[Desktop Entry]
Name=Thunderbird
Exec=/opt/thunderbird/thunderbird %u
Icon=/opt/thunderbird/chrome/icons/default/default128.png
Type=Application
Categories=Network;Email;
StartupNotify=true
EOF
update-desktop-database ~/.local/share/applications
```



5. Launch and update&#x20;

```bash
thunderbird &
```

`&` at the end of a shell command tells the shell:

* **Start the program as a&#x20;**_**background job**_**.**\
  – The command gets its own PID and keeps running, but the prompt returns immediately so you can type more commands.

So `thunderbird &` launches Thunderbird and gives you your terminal back instead of locking it until you close the mail client.
