<h1>Create Windows Terminal Roaming Profile</h1>
<h3>Background information</h3>
Windows Terminal is awesome to use and has many usecases. But having multiple Windows devices to work on and copying your configuration manually is time consuming and annoying. 
Looking for a "roaming" solution that automates this and syncs the configuration/folders accross my Windows devices, I found "mklink" to be a perfect solution.
Mklink creates a symbolic link between the Link and the Target folder.

<h3>Prerequisites</h3>

1. Have Windows Terminal installed, but not opened.
1. Have a Cloud Storage (For example OneDrive, Nextcloud etc) account that has; 
   - A client installed on your Windows device
   - A physical folder on your storage drive and actively syncs with the cloud

<h3>Configuration</h3>
<p>Run CMD as administrator<br></p>

**Create Symbolic link for Roaming State**\
Move the Roaming State folder to your Cloud connected location.
  - For OneDrive this would be: C:\Users\<username>\OneDrive\path\to\Moved Roaming State

*Important:* The Roaming State folder must not be left in the original directory. Mklink creates a new symbolic folder, and can't when the folder exits.

**Roaming State can be found at:** (folder location to save your Windows Terminal icons and backgrounds for example)
```
%LOCALAPPDATA%\packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe
```
Windows Key + R and paste the path above

Copy two paths:
1. Copy full path to Roaming State from the File Explorer address bar
1. Copy full path to your newly created Cloud connected folder

On CMD:
```
mklink /d "path/to/Roaming State" "path/to/Cloud connected/Roaming State"
```
Example:\
mklink /d "C:\Users\<username>\AppData\Local\packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState" "C:\Users\<username>\OneDrive\Roaming Windows Terminal\RoamingState"
<br></br>

**Create Symbolic link for Settings.json**\
Move the Settings.json file in the Local State folder to your Cloud connected folder.
  - For OneDrive this would be: C:\Users\<username>\OneDrive\path\to\Local State\settings.json

*Important:* Don't have Windows Terminal opened, otherwise it will generate a new settings.json file. Mklink creates a new symbolic file, and can't when the file exits.

**Local State can be found at:** (folder location where your Windows Terminal settings.json can be found)
```
%LOCALAPPDATA%\packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState
```
Windows Key + R and paste the path above

Copy two paths:
1. Copy full path to Local State from the File Explorer address bar
1. Copy full path + settings.json to your newly created Cloud connected folder

On CMD:
```
mklink /h "/path/to/Local State/settings.json" "path/to/Cloud connected/settings.json" 
``` 
Example:\
mklink /h "C:\Users\<username>\AppData\Local\packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json" "C:\Users\<username>\OneDrive\Roaming Windows Terminal\Local State\settings.json"

**[Symbolic link usage\documentation](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/mklink)** 
``` 
MKLINK [[/D] | [/H] Link Target
/h = Symbolic link for files
/d = Symblic link for directories
```

<h3>On your other Windows devices</h3>
<p>Follow the steps listed above. But instead of moving the Roaming and Locale State folders, you remove them. <br>
Mklink will create the settings.json file and Roaming State folder for you. </p>

<h3>Summary</h3>

* You have created a link between the Windows Terminal settings.json file and Roaming State folder to the cloud synced one
* When you click on the Symbolic folder you will be redirected to the Cloud connected location.
* All your Windows Terminals that are connected to your Cloud Storage location, configured as described above, will now be synchronized.
