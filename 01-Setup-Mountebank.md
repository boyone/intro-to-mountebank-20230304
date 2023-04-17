# Setup Mountebank

## Setup Node.js(Windows)

- Goto [Node.js downloads](https://nodejs.org/en/download/) and download Node.js for Windows
  - LTS
  - Current
- Run the Node.js Installer(Windows)
  - Welcome to the Node.js setup wizard
    - Select **_Next_**
  - End-User License Agreement (EULA)
    - Check **_I accept the terms in the License Agreement_**
    - Select **_Next_**
  - Destination Folder
    - Select **_Next_**
  - Custom Setup
    - Select **_Next_**
  - Ready to install Node.js
    - Select **_Install_**
    - Note: This step requires Administrator privileges.
    - If prompted, authenticate as an Administrator.
  - Installing Node.js
    - Let the installer run to completion.
  - Completed the Node.js Setup Wizard
    - Click **_Finish_**

## Setup Node.js(Mac)

1. Install Homebrew

   ```sh
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
   ```

2. Install Node.js

   ```sh
   brew install node
   ```

## Verify That Node.js was Properly Installed and Install Mountebank

1. Run command

   ```sh
   node -v
   ```

2. Update npm

   ```sh
   npm install npm -g
   ```

3. Install mountebank

   ```sh
   npm install mountebank -g
   ```

## Start Mountebank

```sh
mb start
```

Go to [http://localhost:2525](http://localhost:2525)

---

[Home](README.md) [Next](./02-Mountebank-cli.md)