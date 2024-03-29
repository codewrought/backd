# backd
 Mac OS specific Bash script to automatically backup up multiple folders/drives into a destination-drive. The backup folders created on the destination-drive will have the format of YYYYMMDD-folder where YYYY = year, MM = month, DD = day and folder = the name of the source directory/folder that is being backed up. If the target drive has an existing backup folder from a previous run, it will be deleted first before a fresh copy replaces it with the current date's prefix. All backups will be placed at the root folder of the destination-drive.
 
One time setup:
1. Start the Terminal app.
2. "cd" into the folder where you downloaded this GitHub project. E.g. "cd ~/GitHub/backd".
3. Edit the backd script by editing the array of source folders/drives to be backed up. E.g. "vi backd". Follow the instructions in the comments for where/what to change. Look for the parts tagged with "EDIT ME".
4. Copy the backd file to /usr/local/bin using sudo. E.g. "sudo cp backd /usr/local/bin".

To run the script:
1. Make sure that your destination-drive is connected to the computer and is available for use.
2. In the Terminal.app, type "sudo backd destination-drive", where destination-drive is the name of the drive you want the backup to end up.
3. The script has an array of a secondary set of folders/drives that it can back up. These are the "essential" ones that you can back up more frequently. To back up the essential folders/drives, use the "-e" option. E.g. "sudo backd -e destination-drive".

To schedule this script to run daily (default 2:00AM every day):
1. Edit the com.codewrought.backd.plist. E.g. "vi com.codewrought.backd.plist". Modify the "destination-drive" to be the name of your destination backup drive. Optionally, if you want the schedule backin up the secondary set of folders/drive instead, you can add the "-e" option as the second parameter by adding the line "<string>-e</string>" between the first and second "ProgramArguments".
2. Copy com.codewrought.backd.plist file to /Library/LaunchDaemons. E.g. "sudo cp com.codewrought.backd.plist /Library/LaunchDaemons".
3. If you want to change when the script runs. Edit the "StartCalendarInterval" section.
4. To schedule the job, type: "sudo launchctl load -w /Library/LaunchDaemons/com.codewrought.backd.plist".
5. The output of the script will be in /tmp/ directory. To see the output in real-time when the scheduled script runs, you can run: "tail -f /tmp/com.codewrought.backd.stdout".
6. To do a test run of the scheduled script, type: "sudo launchctl start com.codewrought.backd".

Future version ideas:
Have a config file containing the source folders/drives instead of being a hard-coded array in the script.