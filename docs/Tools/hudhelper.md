# HUD Helper
This is a server-side mod which facilitates the use of Volute clients on the 
server, as well as a streamer using the HUD for streaming on Twitch.  It 
includes the feature of [Reload Fix](reloadfix.md) as well as the following:

- Spectators (streamers) receive **all player entities at all times**, meaning 
that the wallhack can always see everyone, and every player position can be 
accurately plotted on the radar.  Without this, the game only sends player 
information to those clients that may be able to see them in-game.
- Spectators (streamers) **receive all player health at all times**.  The HUD 
Helper uses an existing unused field (called `loopSoundFlags`) to track 
health.  Without this, the player health only updates when the streamer is 
near the player.
- Dead players who are watching a team-mate have their **camera modified from 
the server-side**, in order to ignore the lean of the player they are 
spectating and force them into a first-person camera.  This is to remove the 
long-abused third-person view which allows dead team-mates to look over or 
around walls.

## Installation
1. Download the `brixton-hudhelper.so` file.  Note that this only works on 
Linux servers.
1. Upload the file to your server, and place it in the same folder as 
`fgamededmohaa.so`.
1. Modify your launch command for the server to include the `LD_PRELOAD` 
directive, e.g., `LD_PRELOAD=./brixton-hudhelper.so ./mohaa_lnxded XXX`.  This 
ensures that `brixton-hudhelper.so` is loaded before any other libraries, and 
allows it to hook the relevant server functions to change server behaviour.

## Download
- [brixton-hudhelper.zip](/static/brixton-hudhelper.zip)

## How It Works
HUD Helper performs the same Reload Fix anti-spam behaviour as described in 
[Reload Fix](reloadfix.md#how-it-works).

HUD Helper also hooks the relevant functions on the server to modify the logic 
for sending entities, ensuring that if the player is a spectator, all player 
entities are sent.  It also adds information such as client HP to each entity 
as well.  This is not normally sent as part of the entity data, only to 
spectators for the current player they are spectating.

HUD Helper also inserts itself into the process of calculating dead player 
camera positions to skip the lean calculation, and forces the cvars 
`g_spectatefollow_up` and `g_spectatefollow_forward` to be 0 (regardless of 
their cvar values).

<!---
--->
