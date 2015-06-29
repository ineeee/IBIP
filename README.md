# IBIP
The IRC Bot Identification Protocol Standard

### Abstract

The IRC Bot Identification Protocol, or IBIP, formalizes the detection and enumeration of robots on an IRC network.

IBIP relies upon the standard behavior of IRC clients, as standardized in [RFC 2812](https://tools.ietf.org/html/rfc2812).

This standard should be defined in the Server INFO response as a server feature/requirement.

### Labels

* A **robot** or **bot** is an automated script or program that performs tasks on an IRC network.
* A **client** is a user, usually humanoid, connected to an IRC network.
* A **target** is an IRC channel or nickname used by both **clients** and **robots** to direct IBIP messages.

### Protocol

IBIP has two mandatory components: a *call* component and a *response* component.

Human **clients** are normally the originators of the *call* component, while **robots** respond to the call with the *response* component. However, nothing stop **robots** from originating an IBIP call, and nothing stops human **clients** from falsely responding to the call.

#### The "call" component

Clients expecting a response from **all** IBIP-compliant IRC bots in the current channel should send a PRIVMSG in the following format:

```
PRIVMSG target :.bots
```

Within an IRC client, this message will be just `.bots`.

The target may be one of two options:

* A channel, like `#bots` or `#help`
* An IRC nickname, like `user123` or `johndoe`

If the target is a channel, the client must expect to receive proper responses from all IBIP-compliant bots in the targeted channel.

If the target is a nickname, the client must expect to receive either no proper responses or exactly one proper response from the IBIP-compliant bot messaged. If the nickname messaged is not the nickname of an IBIP-compliant bot **or** does not exist on the network, the client should not expect to receive a proper response.

#### The "response" component

Upon receiving a PRIVMSG of the format specified above, IBIP-compliant IRC bots are expected to send a response PRIVMSG in the following format:

```
PRIVMSG target :Reporting in! [<language>] information
```

Where the target is one of two options:

* The IRC channel from which the request originated.
* The IRC nickname of the user who sent the IBIP "call".

If the call was sent through a channel and **not** privately, the bot should reply through the channel. If the call was sent privately, the bot should reply through a corresponding PRIVMSG directly to the sender.

The response sent to the target has the following format:

```
Reporting in! [<language>] information
```

In this format, the "Reporting in!" component is **static** and should **not** vary between IBIP-compliant bots.

The "[\<language\>]" component is **optional**, and specifies the language(s) in which the IRC bot was developed. If multiple languages were used, it is recommended that they be separated by slashes, although this is not mandatory. This component **may not** contain mIRC color codes or other non-text characters, to simplify parsing.

After the "[\<language\>]" component, the bot writer may choose to specify any additional information they consider pertinent to someone identifying bots with IBIP. This information is **optional**.

In summary, an example IBIP response might look like this:

```
PRIVMSG #channel :Reporting in! [C] More info at http://example.com
```
