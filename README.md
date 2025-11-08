<div align="center">

![retro_music](https://github.com/Malwarize/retro/assets/130087473/c9824547-9b09-48fc-a113-e1a847793cca)

<h2> play music with command line </h2>

[![GitHub release](https://img.shields.io/github/v/release/Malwarize/retro?color=blue&label=release)]()
[![GitHub license](https://img.shields.io/github/license/Malwarize/retro?color=green)]()
[![GitHub issues](https://img.shields.io/github/issues/Malwarize/retro?color=red)]()
[![GitHub stars](https://img.shields.io/github/stars/Malwarize/retro?color=yellow)]()
[![GitHub forks](https://img.shields.io/github/forks/Malwarize/retro?color=orange)]()
[![GitHub watchers](https://img.shields.io/github/watchers/Malwarize/retro?color=blue)]()

play music then continue your work on the terminal.

<img src="https://github.com/Malwarize/retro/assets/130087473/aa91f82c-7faa-4804-b8e6-42b31ce7e6d9" alt="hi" style="width: 500px;" >
</div>

## 🗺️ map 
- [<code>📦 Installation</code>](#-installation)
- [<code>📁 Directory Structure</code>](#-directory-structure)
- [<code>🎮 Music management</code>](#-music-management)
- [<code>🎧 Playlist management</code>](#-playlist-management)
- [<code>🚦️ Controls</code>](#-controls)
- [<code>⚙️ Configuration</code>](#-configuration)
- [<code>💾 Cache</code>](#-cache)
- [<code>🌐 Update</code>](#-update)
- [<code>📝 License</code>](#-license)
- [<code>📢 Acknowledgments</code>](#-acknowledgments)
 
## 📦 Installation
$${\color{#AC3097}Install \space \color{#56565E}Retro}$$ 
```sh
wget https://github.com/Malwarize/retro/releases/download/v0.0.44/installer.tar.gz
tar -xvf installer.tar.gz
chmod +x installer.sh
./installer.sh
```
this installer is for linux of `systemd` based systems, if you are using other systems you can install it manually by compiling the source code then run the server as you like.

$${\color{#AC3097}Uninstall \space \color{#56565E}Retro}$$
```sh
~/.local/bin/uninstall_retro.sh
```

## 📁 Directory Structure

```
retro/
├── client/                 # Client-side CLI application
│   ├── cmd/               # Command-line interface commands
│   │   └── views/         # Terminal UI views (status, playlists, etc.)
│   ├── controller/        # Client controllers for commands and services
│   └── main.go            # Client entry point
├── server/                # Server-side music player
│   ├── player/            # Core music player logic
│   │   ├── db/            # Database models and operations
│   │   ├── discord/       # Discord Rich Presence integration
│   │   ├── engines/       # Music source engines (YouTube, SoundCloud)
│   │   └── *.go           # Player, queue, and server logic
│   └── main.go            # Server entry point
├── config/                # Configuration management
├── logger/                # Logging utilities
├── shared/                # Shared utilities and constants
├── scripts/               # Build and deployment scripts
├── etc/                   # System service files (systemd)
├── go.mod                 # Go module dependencies
├── go.sum                 # Go module checksums
├── Makefile               # Build automation
└── README.md              # This file
```

#### $${\color{#AC3097}Key \space \color{#56565E}Components}$$

- **client**: The command-line interface that users interact with. It communicates with the server to control music playback.
- **server**: The background service that handles music playback, queue management, and downloading/streaming from various sources.
- **engines**: Modular music source implementations for YouTube and SoundCloud.
- **db**: SQLite database operations for storing playlists and music metadata.
- **config**: Configuration file handling and default settings.
- **shared**: Common utilities used across both client and server.

## 🎮 Music Management
$${\color{#AC3097}Play \space \color{#56565E} Music}$$
```sh
retro play "Despacito - Luis Fonsi"                      # you can search and play music by name
```
*play command is smart enough to play music from different sources, you can play music by name, url, file path, directory path, queue, and playlist.*
```sh
retro play "https://www.youtube.com/watch?v=kJQP7kiw5Fk" # you can play music by url
retro play queue_music                                   # you can play music from queue, you can do this with music index in the queue
retro play ~/Music/Despacito.mp3                         # you can play music by file path 
retro play ~/Music/                                      # you can play music by directory path, it will play all music in the directory
retro play queue_music                                   # it prioritize music in queue and play it first you can do this with music index in the queue
retro play playlist_name                                 # you can play music from playlist
```

$${\color{#AC3097}Status \space \color{#56565E} Music}$$
```sh
retro status # 🎵 check the queue status tasks downloading|searching, playing|paused, songs in queue
```

#### $${\color{#AC3097}Pause/Resume \space \color{#56565E}Music}$$
```sh
retro pause  # ⏸️
retro resume # ▶ ️
```

#### $${\color{#AC3097}Next/Previous \space \color{#56565E}Music Queue}$$
```sh
retro next # ⏭️️
retro prev # ⏮️️
```
#### $${\color{#AC3097} Remove \space \color{#56565E}Music from Queue}$$
```sh
retro remove music_name #🗑️
```
*you can remove music from queue by name or index `retro remove 1`*

#### $${\color{#AC3097}Adjust \space \color{#56565E}Volume}$$
```sh
retro vol 50 # 🎚️ set volume to 50% 
retro vol 0  # 🔇 mute volume Adjust
```

#### $${\color{#AC3097}Stop \color{#56565E}Music Queue}$$
```sh
retro stop # 🛑
```
## 🎧 Playlist Management
#### $${\color{#AC3097}Create \space \color{#56565E}Playlist}$$
```sh
retro list create my_playlist # 📂
```

#### $${\color{#AC3097}Add \space \color{#56565E}Music to Playlist}$$
```sh
retro list add my_playlist "Despacito - Luis Fonsi"                      # ➕ search and add song to playlist
retro list add my_playlist "https://www.youtube.com/watch?v=kJQP7kiw5Fk" # ➕ add song to playlist by url
retro list add my_playlist queue_music                                   # ➕ add music from queue
```
*you can add music to playlist by name, url, queue (index|name`retro list add my_playlist music_index`) and file path* 

#### $${\color{#AC3097}Remove \space \color{#56565E}Music from Playlist}$$
```sh
retro list remove my_playlist "Despacito - Luis Fonsi" # ➖ remove song from playlist
retro list remove my_playlist 1                        # ➖ remove song from playlist by index
```

#### $${\color{#AC3097}Show \space \color{#56565E}Playlist}$$
```sh
retro list my_playlist # 📂 show all songs in playlist
```

#### $${\color{#AC3097}Play \space \color{#56565E}Playlist}$$
```sh
retro list play my_playlist # 📂 add all songs in playlist to queue
```
#### $${\color{#AC3097}Delete \space \color{#56565E}Playlist}$$
```sh
retro list remove my_playlist # 📂 delete playlist
```

## 🚦 Controls
#### $${\color{#AC3097}Logs \space \color{#56565E}Control}$$
```sh
retro logs        # 📜 show all logs #last 200 lines 
retro logs info   # 📢 show all info logs 
retro logs error  # 🚫 show all error logs
retro logs warn   # ⚠️ show all warning logs
```

#### $${\color{#AC3097}Changing \space \color{#56565E}Theme}$$
```sh
retro theme pink    #🧼 
retro theme purple  #🔮  
retro theme blue    #🌊
# TODO: retro theme custom 
```

#### $${\color{#AC3097}Command \space \color{#56565E}Help}$$
```sh   
retro help      #❓ show all commands
retro help play #❗ show play command help
```
## 💾 Cache

#### $${\color{#AC3097}Cache \space \color{#56565E}Control}$$
```
retro cache       # 💾 show all cached data
retro cache clear # 🧹 clear all cache
```

## 🔧 Configuration 
#### $${\color{#AC3097}Config \space \color{#56565E}File}$$
the config file is located by default in `~/.retro/config.json`
if not found, you can create it manually by 
```sh
mkdir -p ~/.retro
touch ~/.retro/config.json
```
$${\color{#AC3097}Default \space \color{#56565E}Config}$$
```json

{
  "retro_path": "~/.retro/",       
  "path_ytldpl": "yt-dlp",        
  "path_ffmpeg": "ffmpeg",         
  "path_ffprobe": "ffprobe",      
  "search_timeout": 60000000000,   
  "theme": "pink",        
  "db_path": "~/.retro/retro.db",
  "discord_rpc": false, 
  "log_file": "~/.retro/retro.log",
  "server_port": "3131"
}
```
you can change the config manually, easy to understand and modify.

$${\color{#AC3097}Note \space \color{#56565E}that}$$

* ☝ ️ if you change the config file, its recommended to restart the retro service.
with `systemctl --user restart retro`
* ⚠️  the config file will override the default values.
* 🤖  please make sure to setup the autocompletion script to have a better experience with retro. see `retro completion`
## 🌐 Update
$$\color{#AC3097}Retro \space \color{#56565E}Update$$

to update retro to the latest version on github you can use the following command
```sh
retro update
```

## 📝 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

## 📢 Acknowledgments

#### $${\color{#AC3097}Thanks \space to \space our \space sponsor \space \color{#FF99EE}@HelloHabiba \space ☕}$$ 
#### $${\color{#AC3097}retro \space \color{#56565E}is \space  made  \space  by  \space  \color{#FF99EE} @Malwarize \color{#56565E} \space with \space \color{red} ❤️}$$


