# Reload Fix
This is a server-side mod which facilitates the use of Volute.  It is a 
sub-set of the HUD Helper, for servers that do not require all of its 
features.  Primarily, this fixes the "reload bug" which happens occasionally 
when players are using Volute.

During normal gameplay, on a server without HUD Helper or Reload Fix 
installed, players using Volute can sometimes find that their commands (e.g., 
reloading) are ignored by the server.  This is due to the fact that their 
Volute client is regularly asking the server for the list of players in order 
to populate the player's list in the F7 menu.

When sending this request regularly, alongside other commands such as 
"reload", the server sees this behaviour as spam.  Depending on the 
configuration of the server, it rate-limits clients who are seen as 
"spamming", and as a result may ignore some commands.

This affects any commands sent to the server that are "rate-limited", not just 
"reload", although that might be most visible.  With HUD Helper or Reload Fix 
installed, this problem is fixed.

## Download
- [brixton-reloadfix.zip](/static/brixton-reloadfix.zip)

## Installation
1. Download the `brixton-reloadfix.so` file.  Note that this only works on 
Linux servers.
1. Upload the file to your server, and place it in the same folder as 
`fgamededmohaa.so`.
1. Modify your launch command for the server to include the `LD_PRELOAD` 
directive, e.g., `LD_PRELOAD=./brixton-reloadfix.so ./mohaa_lnxded XXX`.  This 
ensures that the Reload Fix is loaded before any other libraries, and allows 
it to hook the relevant server functions to change server behaviour.

## How It Works
When installed, Reload Fix hooks the function responsible for processing 
commands from clients.  If it processes a `score` command, as sent by Volute 
clients, it does **not** count it as a rate-limited command, allowing all 
other commands to be processed as normal.  Note that this has no effect on 
*actually* spamming the server and existing rate-limit configuration  e.g., 
chat flood.  You will still be prevented from doing so.

<!---
--->
