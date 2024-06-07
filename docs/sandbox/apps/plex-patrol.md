# plex_patrol

## What is it?

[plex_patrol](https://github.com/l3uddz/plex_patrol) is a tool which can monitor a plex server to kick transcodes (audio or video or both), kick paused streams if not resumed within X minutes, kick specific players, e.g. Plex Web, etc.

| Details     |             |             |             |
|-------------|-------------|-------------|-------------|
| [:material-home: Project home](https://github.com/l3uddz/plex_patrol){: .header-icons } | [:octicons-link-16: Docs](https://github.com/l3uddz/plex_patrol){: .header-icons } | [:octicons-mark-github-16: Github](https://github.com/l3uddz/plex_patrol){: .header-icons } | [:material-docker: Docker](https://hub.docker.com/r/cloudb0x/plex_patrol){: .header-icons }|

### 1. Installation

``` shell
sb install sandbox-plex-patrol
```

### 2. URL

Plex Patrol has no UI; it's driven by a config file.

### 3. Usage

The role will fill in the Plex URL and token; aside from that the various settings are described in comments, with the defaults as below.

The settings file is found at:

```shell
/opt/plexpatrol/settings.ini
```

After editing the file, restart the container with `docker restart plex_patrol`.

default contents:

``` ini title="settings.ini"

[settings]
DEBUG = false # (1)!
SERVER_URL = http://plex:32400 # (2)!
SERVER_TOKEN = YOUR_TOKEN_WILL_BE_HERE # (3)!
SERVER_NAME = Saltbox # (4)!
CHECK_INTERVAL = 90 # (5)!
KICK_4K_TRANSCODE = true # (6)!
KICK_VIDEO_TRANSCODES = false # (7)!
KICK_AUDIO_TRANSCODES = false # (8)!
KICK_CLIENT_PLAYERS = # (9)!
KICK_MULTIPLE_IP = true # (10)!
KICK_MULTIPLE_IP_MAX = 1 # (11)!
KICK_PAUSED_TRANSCODES = true # (12)!
KICK_PAUSED_DIRECTPLAY = true # (13)!
KICK_PAUSED_GRACE_MINS = 15 # (14)!
# Messages to be displayed for different kick types.
KICK_4K_TRANSCODE_MESSAGE = You are not allowed to transcode 4K content, fix your settings!
KICK_PAUSED_MESSAGE = You are not allowed to pause a stream for that long... cya!
KICK_TRANSCODE_MESSAGE = You are not allowed to transcode streams, use a better client!
KICK_PLAYER_MESSAGE = You are not allowed to use this trash player. Use the official software from www.plex.tv/downloads -> Get An App!!!
KICK_MULTI_IP_MESSAGE = You are not allowed to stream from more than 1 IP address!
WHITELISTED_USERS = # (15)!
```

1. Show debug messages.
2. Plex server url (e.g. `http://plex:32400` or `https://plex.yourdomain.com`)
3. Plex token for server.
4. Name of server (does not matter, its used in the logs).
5. How often to check the active streams in seconds.
6. Instantly kick 4K transcodes? (true/false)
7. Instantly kick video transcodes? (true/false)
8. Instantly kick audio transcodes? (true/false)
9. Instantly kick any players from this , separated list?
10. Instantly kick streams from users with multiple IPs (true/false)
11. How many streams from unique IPs before kicking extra user streams if above is true.
12. Delay kick paused transcodes (direct streams count too)? (true/false)
13. Delay kick paused direct plays? (true/false)
14. When the options above are true, the user has this many minutes to resume, otherwise kick.
15. User list separated by a , who are immune from all checks.

PLEX_PATROL's log is found at `/opt/plex_patrol/status.log`:

```shell
2023-03-29 20:07:06,432 - INFO       - plex_patrol                              -  <module>                 -
       _                         _             _
 _ __ | | _____  __  _ __   __ _| |_ _ __ ___ | |
| '_ \| |/ _ \ \/ / | '_ \ / _` | __| '__/ _ \| |
| |_) | |  __/>  <  | |_) | (_| | |_| | | (_) | |
| .__/|_|\___/_/\_\ | .__/ \__,_|\__|_|  \___/|_|
|_|                 |_|

#########################################################################
# Author:   l3uddz                                                      #
# URL:      https://github.com/l3uddz/plex_patrol                       #
# --                                                                    #
# Part of the Cloudbox project: https://cloudbox.rocks                  #
#########################################################################
# GNU General Public License v3.0                                       #
#########################################################################

2023-03-29 20:07:06,433 - INFO       - plex_patrol                              -  <module>                 - Initializing
2023-03-29 20:07:06,433 - INFO       - plex_patrol                              -  <module>                 - Validating server 'http://plex:32400' with token 'YOUR_TOKEN_HERE'
2023-03-29 20:07:06,450 - INFO       - plex_patrol                              -  <module>                 - Server token was validated, proceeding to uphold the law!
...
```

- [:octicons-link-16: Documentation: Plex Patrol Docs](https://github.com/l3uddz/plex_patrol){: .header-icons }
