# hajukebox
Contains my Media Player dashboard code

#Problem I wanted to solve.

I have a mixture of Google smart speakers and Sonos speakers dotted around the house.
The Sonos speakers don’t get used daily and don’t want them to be constantly on standby wasting power so they are connected to the mains using smart switches.
I have a ‘Sonos connect’ connected to a home theatre system, also powered on and off via a smart switch. The Home theatre system is controlled using a Logitech Elite remote control.

I wanted to make it easy for my wife (and me) to be able to select an internet radio station and send it to any of the various speakers or the home theatre system and have it automatically power on if currently powered off.

I subsequently extended it to enable the selection of specific Plex Media Server playlists in addition to internet radio stations.

I wanted the front end to be reasonably attractive and intuitive and easy to add additional sources and/or speakers.

My Solution
I tried a number of different ‘jukebox’ style options. In particular, I took some inspiration from Lukx’s Jukebox Card for Home-Assistant but felt it wasn’t ‘pretty’ enough for a high WAF.
Nothing I looked at seemed to meet all my specific requirements so I ended up building a lovelace interface of my own using several different components.
The key component is the awesomely powerful Button Card by @RomRider .
I have shamelessly copied Keith Townsends templates in his thread Fun with custom:button-card as the basis for my UI.

Speaker selection buttons
The speakers connected via a smart switch have a ‘power’ icon in the top right of the button.
If the button is ‘green’ it is connected to power and available to be switched on/off via Homeassistant.
If the button is ‘grey’ then the switch is currently not available (switched off at the mains) and requires someone to get up out of their chair and physically switch it on before HA can operate it.

Single tapping one of the speaker buttons in the speaker selection panel highlights the selected speaker.
Double tapping one of the speaker buttons will send the currently selected source to the currently selected speaker - which will automatically be powered on first if necessary and if the smart switch it is connected to is ‘available’.

Source selection buttons
Similarly, single tapping one of the radio (or music) sources will highlight the selected source.
Double tapping one of the source buttons will send the currently selected source to the currently selected speaker - which will automatically be powered on first if necessary and if the smart switch it is connected to is ‘available’.

Displaying speakers in use
Speakers currently in use (or paused) are displayed using kalkih’s mini-media-player
in an entity-filter card

Limitations
Plex playlists currently can’t be sent to the Sonos speakers using the plex.play_on_sonos service of the Plex Media Server integration. But the developer has told me this is in the works.


If I use the Radio Paradise App, for example, to cast to one of my Google speakers, the mini-media-player card displays a nice background image relevant to the music playing

I haven’t yet managed to find a way to achieve the same effect when casting to the player from the UI


Why not Google Assistant?
There are several reasons why Google Assistant doesn’t work well with my setup.
In order to use one of the Sonos speakers (and yes, I can use GA to send a source to my Sonos speakers) or the home theatre system they need to be powered on first. That’s a WAF barrier. She’d have to remember the right commands to give GA in the right sequence to make it work. Ain’t gonna happen.
A second reason is that - as you might be able to tell - we are fans of Radio Paradise. Earlier this year Radio Paradise stopped working via Tunein, the only option for internet radio stations using GA, so that’s a stumbling block
My wife wanted to be able to easily listen to a Spanish radio station. Again, there was no way she was going to remember the right commands to give GA to make that happen. But she can press a couple of buttons!
Since Google killed Google Play Music and transferred everything to the vastly inferior Youtube Music I’ve been trying to move to managing and accessing our music library locally - hence Plex. Unfortunately Plex doesn’t (yet?) play with Google Assistant.

