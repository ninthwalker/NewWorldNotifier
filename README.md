<p align="center">
<img align="center" src="https://raw.githubusercontent.com/ninthwalker/NewWorldNotifier/master/screenshots/NewWorldNotifierLogo.png" width="225"></p>
<p align="center">
<img src="https://raw.githubusercontent.com/ninthwalker/NewWorldNotifier/master/screenshots/NewWorldNotifierQuePopped.png"></p>  

## New World Notifier
Sends a message when your New World Server Queue has ended.  
Currently supports Discord, Telegram, Text Messages, Alexa 'Notify Me' Skill, Home Assistant scripts and Pushover (Thanks @pattont). If you want another notification type, let me know.    
  
Note: This does not interact with the game at any level or in any way.  
Default settings should work for most people. Just set up at least one notification app and you are good to go!  

## Details/Requirements
1. Windows 10
2. Powershell 3.0+ (Comes with WIN10)
3. .Net Framework 3.5+ (Usually already on Windows 10 as well)
4. The New World Game (You have to purchase/install this on your WIN 10 computer yourself)
5. Discord, Telegram, Pushover, Cell Phone, or Alexa Device. (Other apps/notifications possible in the future if requested)  

## How it works
It's super simple. It takes a screenshot of a specific area of your monitor (Where the Queue window is).  
It then uses Windows 10 Built-in OCR (Optical Character Recognition) to read the text in that screenshot to see if the queue goes away. If it has, it sends you a message. Too easy!

## How to use  
Prereq's: New World Must be running in the foreground of your monitor.  
(If using the Discord notification type, the Desktop Discord App on your computer must *not* be running. (Discord does not send mobile notifications if you are Active in another Discord app =( See Dev post [here](https://twitter.com/discordapp/status/720723876934582272))  
After clicking the shortcut (Download Option One) or Launching the script from the command line (Download Option Two):  

1. Click 'Start' to begin scanning your queue status and notifying you.
2. Click 'Stop' to halt scanning and notifications.
3. ???
4. Profit!  
  
## Install Options  

**Option One**  
 (Recommended - Easiest to use)

1. Click the 'Code' button on this page. Then select 'Download ZIP'  
2 . You may need to 'unblock' the zip file downloaded. This is normal behavior for Microsoft Windows to do for files downloaded from the internet.  
`Right click > Properties > Check 'Unblock'`
3. Extract the contents of the ZIP file. You only need the 'NewWorldNotifier.lnk' shortcut, and the NewWorldNotifier.ps1 files. Make sure these 2 files are kept in the same directory wherever you move them to.  
4. Once Setup is completed, you can double click the shortcut to run the New World Notifier script.  

**Option Two**  
(For those with some Powershell experience, or if you don't want to use the shortcut method above)
1. Copy the NewWorldNotifier.ps1 file to your computer.
2. Open a powershell console and navigate to the folder you saved the NewWorldNotifier.ps1 file to.
3. Enter the below command to temporarily set the execution policy:  
`Set-ExecutionPolicy -Scope Process Bypass`  
Alternatively, set the execution policy to permanently allow powershell scripts:  
`Set-ExecutionPolicy -Scope Currentuser Unrestricted`  
4. Once setup is completed, you can launch the script by entering the following command in powershell:  
`.\NewWorldNotifier.ps1`  

## Config/Settings  
Some initial configuration is required before it will work for you.  
If you right click and edit the NewWorldNotifier.ps1 file you will see a section near the top that requires you to enter your own settings.

**Note: The only required setting to make this work is to set up one notification type.**  
Currently supported Notification apps are: Discord, Telegram, Pushover, Text Messages, Home Assistant and the Alexa 'Notify Me' Skill.  

### Required Settings:  
At least one of the below notification types is required. Or you can set up all 5 if you want!  

* **Discord**  
Set discord to $True to enable this notification type.
Enter in the discord webhook for the channel you would like the notification to go to.  
Discord > Click cogwheel next to a channel to edit it > Webhooks > Create webhook.
See this quick video I found on Youtube if you need further help. It's very easy. Do not share this Webhook with anyone else.  
[Create Discord Webhook](https://www.youtube.com/watch?v=zxi926qhP7w)  

* **Pushover**  
Set pushover to $True to enable this notification type.  
Log in and create a new application in your Pushover.net account.  
Copy the User API Key and the newly created Application API Key to the Pushover variables.  
Set the optional commented out settings if desired.  
(Thanks to @pattont for this Notification Type)    

* **Telegram**  
This can be a little more complicated to set up, but you can look online for further help. The basics are below but I didn't go into detail:  
Set telegram to $True to enable this notification type.  
Get the Token by creating a bot by messaging @BotFather  
Get the ChatID by messaging your bot you created, or making your own group with the bot and messaging the group. Then get the ChatID for that conversation with the below step.  
Go to this url replacing [telegramBotToken] with your own Bot's token and look for the chatID to use. 
https://api.telegram.org/bot[telegramBotToken]/getUpdates

* **Text Message**  
Note: I didn't want to code in all the carriers and all the emails. So only Gmail is fully supported for now. If using 2FA, make a google app password from here: https://myaccount.google.com/security.  
Feel free to do a pull request to add more if it doesn't work with these default settings and options. Or just edit the below code with your own carrier and email settings.  
Set textMsg to $True  to enable this notification type.  
Enter carrier email, should be in the format of:  
"@vtext.com", "@txt.att.net", "@messaging.sprintpcs.com", "@tmomail.net", "@msg.fi.google.com"  
Enter in your phone number, email address and email password.  
Change the smtp server and port if you are not using Gmail.  

* **Alexa 'Notify Me' Skill**  
Set alexa to $True to enable this notification type.  
Enable the Skill inside the Alexa app. once linked it will email you an Access Code.  

* **Home Assistant**  
This is probably way more advanced than most people will use, but it's here for those that want it.  
I personally use this so my Alexa devices will announce when my queue has ended.  
Set HASS to $True  
Set your HASS URL, and API Token  
Enter in your script's entity_id that you want to have run when the Queue .

### Optional/Advanced Settings:  

1. **Configure your own X,Y Coordinates of your Queue window**      
Everyones monitors are different, so just in case the default screenshot area does not work for you, you can specify your own. 

    1. Launch New World and queue for your character. Leave it up and go to step b.  
    1. Launch the NewWorldNotifier app and click the 'Get Coords'.  
    1. The next 2 mouse clicks (approx) that you perform will be recorded into the window for you to get the X,Y coordinates.
Your first click should be on the top left corner of the Queue window. Your second click should be on the bottom right of the Queue window. If you miss, or mess up, just click 'Exit Coords' in the app, and start again by clicking 'Get Coords'
    1. Keep the NewWorldNotifier app open, write down, memorize (you're smart!), or screenshot the NewWorldNotifier window that has the Top Left and Bottom Right X,Y coordinates. You will need these for the next step.  
    1. Right click on the actual script file. (NewWorldNotifier.ps1) and select Edit. This should open the script for editing. Enter in the coordinates created during step d into their respective sections.  
    1. Set the 'useMyOwnCoordinates' to "Yes".

2. **Screenshot Path**  
Set the path to where you would like the temporary screenshot to be saved to.  
By default it goes to your %temp% Directory.  

3. **Screenshot Delay**  
If you would like to change how often the script scans the Queue Window you can enter a different time here in seconds.
Note: this script uses hardly any resources and is very quick at the screenshot/OCR process.   
Default Value: 30 seconds  
  
4. **Stop on Queue**  
'Yes' will stop the script when the Queue window is gone. 'No' will have it continue to scan and must be stopped manually.  
Default is 'Yes'  

## FAQ/Common Issues  
1. As noted above, this app is entirely legal/safe/conforms to all TOS of Amazon and New World. This does not touch the game or files in any way.  
2. make sure you have double quotes around your app webhooks and most settings you configured in the script. ie: "webhook here"  
3. If you use a different language setting other than English for your default windows language, this may not work, or will need script edits.  
4. Remember that the Game window needs to be at the foreground of one of your monitors for this to work. Don't have another application or window covering the game.  

## Screenshots  

<img src="https://raw.githubusercontent.com/ninthwalker/NewWorldNotifier/master/screenshots/NewWorldNotifierQuePopped.png">  

![](https://raw.githubusercontent.com/ninthwalker/NewWorldNotifier/master/screenshots/NewWorldNotifierStart.png) ![](https://raw.githubusercontent.com/ninthwalker/NewWorldNotifier/master/screenshots/NewWorldNotifierCoords.png)  

![](https://raw.githubusercontent.com/ninthwalker/NewWorldNotifier/master/screenshots/NewWorldNotifierRunning.png) ![](https://raw.githubusercontent.com/ninthwalker/NewWorldNotifier/master/screenshots/NewWorldNotifierEnded.png)  

![](https://raw.githubusercontent.com/ninthwalker/NewWorldNotifier/master/screenshots/NewWorldNotifierScripts.png)  
