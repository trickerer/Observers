### This mod was last updated:
### last version: 14 May 2020, TrinityCore revision: [e2434e4f47](https://github.com/TrinityCore/TrinityCore/commit/e2434e4f47)
### 2013 version: 12 Dec 2013. TrinityCore revision: [385e2dba37](https://github.com/TrinityCore/TrinityCore/commit/385e2dba37)

# [ Observers Manual ]
>Compiled by: Trickerer (onlysuffering @ Gmail dot Com)  
>Version 0.2 - 18 May 2020  

---------------------------------------
### Contents
1. [Observers](#observers)
    - [Installation](#installation)
    - [Commands](#commands)
    - [Usage](#usage)
    - [DB Occupations](#db-occupations)
3. [Guide Changelog](#guide-changelog)

---------------------------------------

## Observers
Observers is a TrinityCore mod (https://github.com/TrinityCore/TrinityCore/), currently only 3.3.5 branch is supported  
This mod allows people to watch other players play the game without being restricted by levels, maps or anything  

Some people may want to present their game skill to other players.  
But it is also useful as a GM tool to track players suspected in cheating, exploiting, botting, etc.  

### Installation
At the very start of this document you can find a link for TrinityCore revision for the last version of this mod  
Follow TrinityCore Installation Guide (https://TrinityCore.info/) to install the server first  
Download Observers.patch and put it into your TrinityCore folder  
Apply the patch using `patch -p1 < Observers.patch` command (creating new files)  
(Re)run CMake and (re)build  
Merge `worldserver.conf.dist` into your worldserver.conf file (Observers mod settings)  
Apply `characters_observers.sql` from /TrinityCore/sql/custom/Observers/ to your `characters` DB  
Launch the server

### Commands
Here you can find a list of commands you need to get started  
Note that some commands may not be available to all accounts (depending on their access level and permissions set in the RBAC tables). You may need to change your account permissions to enable usage of some commands  
Commands are divised by persmissions into two groups: player commands and GM commands
```
KEY:
< > (less/greater than) indicates infon or action you need for the command, can be left out to list info  
 |  (pipe character) indicates parameter options (i.e. this|that  = this OR that)  
 -- (two dashes) indicates information follows about the command  
```
* **`.observe <NAME>`** -- (Player command) start watching named player. You need an approval from that player (see below)  
    - NAME = player's name, case-insensitive  
    **Example Usage:**  
        - `.observe trickerer` (start watching player named 'trickerer')  
        - `.obs trickerer`  
* **`.deobserve`** -- (Player command) stop watching and return camera to your location  
    - (No arguments)  
    **Example Usage:**  
        - `.deobserve`  
        - `.deob`  
* **`.observers`** -- (Player command) by itself will list all syntax available  
    - **`reloadconfig`** -- (GM command) reloads Observers config settings  
        - (No arguments)  
        **Example Usage:**  
            - `.observers reloadconfig`  
            - `.observers reload`  
    - **`allow <NAME>`** -- (Player command) approve a player to watch you  
        - NAME = player's name, case-insensitive  
            - all, a = approve all pending players  
            - auto on = approve all new pending observers automatically  
            - auto off = return to manual mode for new observers  
            **Example Usage:**  
                - `.observers allow trickerer` (approve player)  
                - `.observers allow all` (approve all pending)  
                - `.observers a all` (same as above)  
                - `.observers allow auto on` (enable autoapprove)  
                - `.observers a a o` (same as above)  
    - **`forbid <NAME>`** -- (Player command) bans player from watch you, player is kicked automatically  
        - NAME = player's name, case-insensitive  
            - all, a = ban all pending observers  
            - auto on = ban all new pending observers automatically  
            - auto off = return to manual mode  
            **Example Usage:**  
                - `.observers forbid trickerer` (kick and ban player)  
                - `.observers forbid all` (ban all pending)  
                - `.observers f all` (same as above)  
                - `.observers forbid auto on` (enable autoforbid)  
                - `.observers f a o` (same as above)  
    - **`kick <NAME>`** -- (Player command) kicks currently active observer  
        - NAME = player's name, case-insensitive  
            - all, a = kick all observers  
            **Example Usage:**  
                - `.observers kick trickerer` (kick player)  
                - `.observers kick all` (kick everyone)  
    - **`list`** -- (Player command) by itself will list all syntax available  
        - active = list currently watching players  
        - allowed = list allowed players  
        - forbidden = list forbidden players  
        - pending = list pending players  
        - all, a (GM command) = lists all above, showing status  
        **Example Usage:**  
            - `.observers kick trickerer` (kick player)  
            - `.observers kick all` (kick everyone)  

### Usage
First pick a player you want to watch and use `.observe` command, this will put you into pending list for that player and send a notification. After you are approved you are free to use `.observe` command again to start watching.  
If you want to silently peek on a player, use `.observe` command while in GM mode (sneaks must be enabled in config). This will bypass all conditions and give no output on the other side, you are also unaffected by any forbid, kick and list commands whatsoever.  
```
Note that you can only start observing if your character is idle and in a safe spot.
```
  
While active, observers become invisible and are prevented from performing any activities which interfere with other players' game experience. 
### DB Occupations
Observers data is stored in the following location:

- `characters` DB
    - `characters_observers` (created by this mod) contains information on all registered observers  

If you need to uninstall the mod you'll have to remove `characters_observers` table manually

---------------------------------------
## Guide Changelog

- **Version 0.2** (_18 May 2020_)
    - Add extra info on conditions
    - Add info on 2013 version
- **Version 0.1** (_02 May 2020_)
    - Create proper manual

---------------------------------------
