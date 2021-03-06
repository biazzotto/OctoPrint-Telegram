# OctoPrint-Telegram

This plugin integrates Telegram Messenger with Octoprint. It sends messages (with photos if available) on print start, end and failure. Also it sends messages during the print at configurable intervals. That way you don't have to remember to regularly have a look at the printing process.
Also, you can control Octoprint via messages. Send `/status` to get the current printer status or `/abort` to abort the current print. Send `/help` for a list of all recognized events.

## Screenshots
![Screenshot](../screenshots/features1.png?raw)
![Screenshot](../screenshots/features2.png?raw)
![Screenshot](../screenshots/features3.png?raw)
![Screenshot](../screenshots/features4.png?raw)
![Screenshot](../screenshots/features5.png?raw)

## Contact / Help

If you want to talk to other users of this plugin and maybe have some influence in the development of this plugin,
you can join the [Octoprint-Telegram-Users-Group](https://telegram.me/joinchat/CXFirQjl9XTp5dr4OZqH9Q).

If you just want to keep up to date with new versions, we also have the channel 
[Octoprint-Telegram-News](https://telegram.me/octoprint_telegram_news).

## Setup

Install via the bundled [Plugin Manager](https://github.com/foosel/OctoPrint/wiki/Plugin:-Plugin-Manager)
or manually using this URL:

    https://github.com/fabianonline/OctoPrint-Telegram/archive/stable.zip

To allow the plugin to send messages via telegram, you have to register a telegram bot. Follow these steps:

* Contact [@botfather](http://telegram.me/botfather) in Telegram Messenger. Either click the link or use the "new chat" / "search" feature of your telegram client to search for "@botfather".

    ![Screenshot](../screenshots/newbot1.png?raw)
* Send `/newbot` to @botfather. Enter a name for the bot, e.g. "Fabians Octoprinter Bot". Then enter a username for the bot, e.g. "FabiansOctoprinterBot". This username has to end in "bot".
* The Botfather hands you a token. You need this to use your bot. Keep this token secret!
    
    ![Screenshot](../screenshots/newbot2.png?raw)
* While you're there, you could also (these steps are optional!):
 * Give your bot a nice profile picture. Send `/setuserpic` to @botfather, select the bot and send the Octoprint logo.

    ![Screenshot](../screenshots/newbot3.png?raw)
 * Tell the Botfather which commands are available. This enables Telegram to auto-complete commands to your bot. Send `/setcommands` to @botfather, select the bot and then send this (one message with multiple lines):
 ```
 abort - Aborts the currently running print. A confirmation is required.
 shutup - Disables automatic notifications till the next print ends.
 imsorrydontshutup - The opposite of /shutup - Makes the bot talk again.
 status - Sends the current status including a current photo.
 settings - Displays the current notification settings and allows you to change them.
 list - Lists all the files available for printing and lets you start printing them.
 print - Lets you start a print. A confirmation is required.
 upload - You can just send me a gcode file to save it to my library.
 sys - Execute Octoprint System Commands.
 ctrl - Use self defined controls from Octoprint.
 ```

    ![Screenshot](../screenshots/newbot4.png?raw)
* Now enter Octoprint's settings and select Telegram.
* Enter the token you got from BotFather into the field "Telegram Token".
* Hit the "Test Token" button. It should report success.
* Send a message (any message will do) to your new bot.
* Now hit reload under the known user list. The chat should appear in the list.
* Save settings to accept new user(s) in list
* Now reopen octoprit settings and check/set the configurations for new users.


## Configuration

* Configuration is done via Octoprint's settings dialog.
* Token: Enter your bot token here. You got this from @botfather, when you created your bot there. After hitting 'Test Token', the current connection status will be shown.
* Known Chats: This list shows all known users. Here you can edit their rights and set notifications.
* Send notification every: Whenever the current z value grows by this value (or more) or the given time has passed since the last notification, a message will be sent.
 * Setting the height to 1.0mm would send messages at z=1.0, z=2.0, z=3.0 and so on.
 * Having the height at 1.0mm with a layer height of 0.3 would send messages at z=1.2, z=2.4, z=3.6 and so on.
 * Setting the time or height to `0` disables those checks. Setting both values to `0` completely disables automatic notifications while printing.
* You can set if you want messages at print start, finish and failure events.
* You can change the messages. Usable variables are:
 * `{file}` (only usable while printing) - The currently printing file.
 * `{z}` (only for height change events) - The current z value.
 * `{percent}` (only useful for height change notifications) - The current percentage of the print progress.
 * `{time_done}`, `{time_left}` (only useful for height change events) - Time done / left in the print.
 * `{bed_temp}`, `{e1_temp}`, `{e2_temp}` - Temperatures of bed, extruder 1 and extruder 2.
 * `{bed_target}`, `{e1_target}`, `{e2_target}` - Target temperatures of bed, extruder 1 and extruder 2.
