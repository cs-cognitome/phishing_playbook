# sublime-text

### 1. Debian/Ubuntu (Parrot OS)



**Install prerequisites & add GPG key**

```bash
sudo apt update && sudo apt install -y wget gnupg
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

\
**Select the channel**

Stable:

```bash
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```

Dev (more frequent updates):

```bash
echo "deb https://download.sublimetext.com/ apt/dev/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```



**Update & install**

```bash
sudo apt update
sudo apt install sublime-text
```



**Verify**

```bash
sublimetext --version
# or
which subl
```
