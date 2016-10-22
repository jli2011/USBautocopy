# USB AutoCopy

USB AutoCopy is a program that is set to run at startup and copies all files from any external device automatically to the local host. For example, when a user plugs in a USB, the program automatically copies and saves all the contents of that USB locally. That path of the copied files can be manually set by the user. See instructions below:

First, create a new text file in your documents folder and paste the following code:

```
#!/bin/sh

while(true)
do
    cp -r /media/root ~/Downloads
done
```

The cp command means “Copy”. The -r stands for recursive. This means that the command will copy all the files including files inside the subfolders.

The first path is the path of your external device. By default, external devices are placed in the media folder when connected. “Root” is simply the name of the user. If your username is not “root” then simply replace that with your current username. For example, my username is “staff1”, so my first path is /media/staff1.

The second path is the location that you want your copied files to be saved. You can choose any location. I simply chose to save mines in my Downloads folder.

The while loop keeps the program running. This way, any new files added to the external drives will be automatically copied and saved.

Once you are done, save the file as “mediacopy.sh”. I saved mines in my Documents folder. Then set the file to be an executable. You can do this by right-clicking the file > select properties tab > and check the box that says “Allow executing file as program”.

![Alt text](https://jiajieli.files.wordpress.com/2016/10/screenshot-from-2016-10-05-10_00_10.png)

If that option is not available, you can do the same thing by using the chmod command in terminal. First, cd to your file directory and execute the following command:

chmod +x mediacopy.sh

Once the file is set as an executable, go back to your terminal and execute the following command:

crontab -e

Cron is a Unix utility that allows tasks to be run automatically in the background. You will need to add your mediacopy.sh file to Cron as a task in order for it to run at startup. To do this, add the following command at the very bottom of the crontab:

@reboot ~/Documents/mediacopy.sh

This is telling the program to execute your program each time at startup. The syntax is simply @reboot <path of file>. Once you are done, your crontab should look something like this:


![Alt text](https://jiajieli.files.wordpress.com/2016/10/screenshot-from-2016-10-05-09_59_09.png)

Save your changes and reboot the system. After it restarts, plug in an external device. You should see a folder with your username show up in the Downloads folder. When you open the folder, you’ll see a folder with a mix of letters and numbers. This is simply the name given to your device.

![Alt text](https://jiajieli.files.wordpress.com/2016/10/screenshot-from-2016-10-05-10_07_35.png)

The program also works with Bash. If you prefer Bash, simply do the following:

Change #!/bin/sh to #!/bin/bash.
Change the name from mediacopy.sh to mediacopy.bash.
Update the filename in Cron.
