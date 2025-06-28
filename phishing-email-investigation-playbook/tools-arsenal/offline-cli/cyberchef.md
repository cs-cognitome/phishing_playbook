# CyberChef

To download and use CyberChef on Parrot OS, you can either use the Snap package manager or clone the Git repository and build it locally. Both methods provide a local instance of the tool, useful for offline use or specific customization. \
\
Method 1: Using Snap&#x20;

1. **Update the package manager:**

```bash
   sudo apt-get update
```

2. **Install snapd (if not already installed):**&#x20;

```bash
   sudo apt-get install snapd
```

3. **Install CyberChef:**

```bash
   sudo snap install cyberchef
```

\
Method 2: Cloning the Git repository&#x20;

1. **Update the package manager:**

```bash
   sudo apt-get update
```

2. **Install required dependencies:**

```bash
   sudo apt-get install build-essential git nodejs npm
```

3. **Clone the CyberChef repository:**&#x20;

```bash
   git clone https://github.com/gchq/CyberChef.git
```

4. **Navigate to the directory:**

```bash
   cd CyberChef
```

5. **Build CyberChef:**

```bash
   npm install
```

6. **Run CyberChef:**

```bash
   npm start
```

This will open CyberChef in your default browser, typically at `http://localhost:8080/`.&#x20;
