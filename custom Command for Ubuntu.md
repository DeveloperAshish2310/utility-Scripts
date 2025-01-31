# Useful Linux Commands

## For Check GPU Usage
```bash
nvtop
```
**Note:** `nvtop` is a real-time GPU monitoring tool. It displays GPU usage and processes running on NVIDIA GPUs.

**Tags:** `#GPU #Monitoring #NVIDIA`

---

## For Open File Explorer with Terminal
```bash
xdg-open <dir>
```
**Note:** This opens a file explorer window for the specified directory in your default file manager.

**Tags:** `#FileExplorer #Terminal`

---

## Start XAMPP All Service
```bash
sudo /opt/lampp/lampp start
```
**Note:** This command starts all the services (Apache, MySQL, etc.) in XAMPP.

**Tags:** `#XAMPP #Start #Service`

---

## Stop XAMPP All Service
```bash
sudo /opt/lampp/lampp stop
```
**Note:** This command stops all the services in XAMPP.

**Tags:** `#XAMPP #Stop #Service`

---

## Uninstall XAMPP
```bash
sudo /opt/lampp/./uninstall
```
**Note:** This uninstalls XAMPP from your system.

**Tags:** `#XAMPP #Uninstall`

---

## Give Permission to All Its Subfolders
```bash
sudo chmod -R 777 <path>
```
**Note:** This gives full read, write, and execute permissions to the specified directory and all its subdirectories.

**Tags:** `#Permissions #chmod #Recursive`

---

## Give Permission
```bash
sudo chmod 777 <path>
```
**Note:** This gives full permissions (read, write, execute) to the specified file or directory.

**Tags:** `#Permissions #chmod`

---

## VI Editor Commands

- **Switch to Normal Mode**: Press `Esc` to ensure you are in Normal mode.
- **Save the File**: Type `:w` and press Enter to save the file.
- **Save and Quit**: Type `:wq` and press Enter.
- **Quit Without Saving**: Type `:q!` and press Enter.

**Note:** These are basic commands for the `vi` text editor.

**Tags:** `#VI #Editor #Commands`

---

## SSH
```bash
ssh username@ipaddress -p <port>
```
**Note:** This command connects to a remote server via SSH on custom port.

**Tags:** `#SSH #Connection`

---

## Remove Package with All Its Dependencies
```bash
sudo apt-get purge --auto-remove jellyfish
```
**Note:** This command removes a package and its associated dependencies that are no longer required.

**Tags:** `#PackageManagement #apt-get #Remove`

---

## Clear RAM Cache
```bash
sudo sync
sudo sh -c 'echo 3 > /proc/sys/vm/drop_caches'
```
**Note:** These commands clear the RAM cache, freeing up memory.

**Tags:** `#RAM #Cache #Clear`

---

## Disable Emoji Hotkey
```bash
gsettings set org.freedesktop.ibus.panel.emoji hotkey "[]"
```
**Note:** Disables the emoji hotkey in the IBus input method.

**Tags:** `#IBus #Emoji #Hotkey`

To re-enable the emoji hotkey:
```bash
gsettings set org.freedesktop.ibus.panel.emoji hotkey "['<Ctrl><Shift>e']"
```
This will set the hotkey back to its default value of `Ctrl-Shift-e`.

**Tags:** `#IBus #Emoji #Hotkey`

---

## Get Service List on a Specific Port
```bash
sudo lsof -i :5000
```
**Note:** Lists all services listening on port 5000.

**Tags:** `#Service #Port #lsof`

---

## Kill Services or Script by PID
```bash
sudo kill -9 <pid>
```
**Note:** This forcefully kills the process with the specified PID. `-9` forces the termination of the process.

**Tags:** `#Process #Kill #PID`

---

## Update VS Code
```bash
wget 'https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64' -O /tmp/code_latest_amd64.deb
sudo dpkg -i /tmp/code_latest_amd64.deb
```
**Note:** This updates VS Code to the latest stable version.

**Tags:** `#VSCode #Update #Linux`

---

## Get List of All Installed Apps
```bash
apt list --installed
```
or
```bash
dpkg -l
```
or
```bash
dpkg --get-selections | grep -v deinstall
```
**Note:** These commands list all installed packages on your system.

**Tags:** `#InstalledApps #PackageManagement #List`

---

## Get the Size of the /var Directory
```bash
sudo du -sh /var
```
**Note:** Displays the total size of the `/var` directory.

**Tags:** `#DiskUsage #Size #Directory`

---

## Get All Folder Size in Current Directory
```bash
for dir in */; do 
    sudo du -sh "$dir"
done
```
or
```bash
for dir in */; do sudo du -sh "$dir"; done; du -sh .
```
**Note:** These commands show the size of all directories in the current directory.

**Tags:** `#DiskUsage #FolderSize #Directory`

---

## Get All File and Folder Size
```bash
du -sh * | sort -h
```
**Note:** Displays the size of all files and directories in the current directory, sorted by size.

**Tags:** `#DiskUsage #FileSize #FolderSize`

---

## Creating Custom Command for Linux Terminal: Making Use of Aliases

```bash
alias shortcut_name='command_to_run'
```
Example:
```bash
alias ll='ls -la'
```
**Note:** Aliases allow you to create custom shortcuts for commands.

To make the alias permanent:
1. Add the alias in `~/.bashrc`
2. Run:
```bash
source ~/.bashrc
```

**Tags:** `#Aliases #CustomCommands #Terminal`

---

## Example Custom Alias
```bash
alias myserver='ssh root@192.168.1.25 -p 5005'
```
**Note:** This alias creates a shortcut for connecting to the SSH server.

**Tags:** `#Aliases #SSH #CustomCommand`

---

## Install Pyzbar in Ubuntu or Linux
```bash
sudo aptitude -y install python3-pyzbar
```
**Note:** This installs the `pyzbar` library, which is used for barcode scanning.

**Tags:** `#Python #Library #Install`

---

## Add Train Data in Tesseract
Path:
```
/usr/share/tesseract-ocr/4.00/tessdata
```
**Note:** This path is where Tesseract OCR stores its language training data.

**Tags:** `#Tesseract #OCR #TrainData`

---

## Control Screen Brightness

### Get Monitor Name
```bash
xrandr --listmonitors
```
**Note:** Lists all connected monitors.

**Tags:** `#Display #Monitor #Brightness`

### Change Brightness
```bash
xrandr --output <monitor_name> --brightness 0.7
```
**Note:** Changes the brightness of the specified monitor.

### Example to Change Monitor Brightness for HDMI-1
```bash
xrandr --output HDMI-1 --brightness 0.7
```
**Tags:** `#Display #Monitor #Brightness`
