# IBIP
The IRC Bot Identification Protocol Standard

The IBIP Standard is designed to allow channel operators and IRC administration an easy way to determine if a User is a bot.

This standard should be defined in the Server INFO response as a server feature/requirement.

The requirements are as defined.

* The bot must respond to a message (PRIVMSG) that is **.bots**
* The response must follow the following format: **Reporting in! (Optional)[<Bot Language>] <Additional Information>**
