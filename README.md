
## 🇯🇵 Japanese Version / 日本語版

日本語版はこちら：**[NeverCrisisJP](https://github.com/ShadowMPo/NeverCrisisJP)**



# Never Crisis — Self-hosted game server for FF7 EVER CRISIS. Keep Midgar online after official EOS.

- **Why:** the service is shutting down; this keeps the single-player game — the stories above all — playable on your own machine.
- **How:** install the game first, unzip this package into the game's folder (it replaces two files and adds the rest), then run `FF7ECServer.exe`: it starts the game and cleans up when you close it.
- **Admin prompt:** once per launch, to add a few lines to the Windows hosts file that point the game at this server; removed on exit.
- **Needs:** Windows 10/11 x64, the complete game folder (`FF7EC_Data`, `octo` and the files included), port 443 free. No Steam client, no internet, nothing to install.
- **Not included, on purpose:** the game — it is Square Enix's and must come from your own installation — and the server's source for obvious reasons. 

## Disclaimer

- **Not affiliated:** this is a fan project. It is not made, endorsed, supported or approved by Square Enix, Applibot, Valve/Steam or anyone connected to them. FINAL FANTASY, FINAL FANTASY VII EVER CRISIS and all characters, art, music, text and data belong to Square Enix Co., Ltd.
- **No game data:** the package holds the server, its own recordings of network traffic, the game's tables and text (the same files the game downloaded to every player). Models, stages, music, movies — the game itself — stay in the copy you installed yourself.
- **No account, no money:** it does not touch Square Enix's servers, your Square Enix or Steam account, and nothing can be bought — the in-game shop for real money does not exist here.
- **Not for profit:** made to keep the single-player stories playable after the service ends. Never pay for this; it is free and must stay free.
- **As is:** no warranty of any kind. You use it at your own risk; the authors are not responsible for lost saves, a broken installation or anything else that follows from using it.
- **Single player only:** co-op, rankings and anything that needs other people are gone with the service and are not coming back.

## The folder

Three kinds of files end up side by side in the game folder.

**1. The game — from your own installation (about 47 GB):**

| | |
|---|---|
| `FF7EC.exe` (650 KB), `GameAssembly.dll` (140 MB), `baselib.dll` (400 KB), `UnityCrashHandler64.exe`, `Applibot.GraphicsUtility.dll`, `NativeVideoUtility.dll` | the game's own files |
| `FF7EC_Data\` (387 MB) | `il2cpp_data`, `Resources`, `StreamingAssets`, `Plugins`, `data.unity3d` … |
| `octo\` (46.5 GB, 235,000 files) | every model, stage, effect and movie, downloaded by the game while the service was up — without it fights cannot load |

**2. This package (48 MB), unzipped on top:**

| | |
|---|---|
| `FF7ECServer.exe` (4 MB) | the server — run this to play |
| `FF7ECServer.pak` (23 MB) | the server's data |
| `items.txt`, `README.md` | every item id (for `--give`), this file |
| `UnityPlayer.dll` (29 MB), `FF7EC_Data\Plugins\x86_64\steam_api64.dll` | the two game files it replaces |
| `save\MasterData\` (11 MB), `save\LocalizeText\` (1 MB) | the game's tables and text, as the service last published them |

**3. Created by the server on the first run:**

| | |
|---|---|
| `config.ini`, `events.ini` | settings (see below) |
| `ff7ec_account_id.txt` | the number of your offline account |
| `data\` | your account and gift box, the server's certificate |
| `save\GameSave\`, `save\MessagePack\` | the game's own save and cache |
| `backups\` | a copy of the account before a reset |

**To keep your progress, back up `data\`, `save\GameSave\` and `ff7ec_account_id.txt` together.** Everything else can be replaced.

## What works

Story chapters, side stories, character stories, dungeons, areas, tower, daily quests, events (solo, Clash and Crisis Battle included), draws, shops, crafting, chocobos, Highwind, missions, login bonuses, season pass, and a guild of your own: create it, its daily missions, bonuses, login bonus and achievements work, and the guild chat is yours alone.

Ended solo events can be brought back (`events.ini`). The draw banners open when this was made (dated until 7 October 2026) stay open for good; banners that had already ended cannot come back — the service deleted their odds.

## What does not work

- **Co-op** (private rooms, matchmaking): the fight runs on a server that no longer exists. Solo fights count for the co-op missions instead.
- **Guild battles, joining other guilds, friends, rankings, real-money purchases, account transfer:** they need other people or the real service.
- **Damage Challenge:** it needs the same battle server as co-op.
- **The Featured and Crossover draw tabs are empty:** their odds are gone from the game data.

## Known differences from the real service

- Draw odds are the game's own tables. Battle drop chances are estimates from recorded play: how often a non-guaranteed drop pays, and how often a clear adds a weapon or materia, were never in the game's data.
- A character who joins through the story arrives at the level of your weakest character (the real rule is unknown).
- Some mission chains and rare counters may advance slightly differently.
- Clash and Crisis Battle scores are kept, but their rankings were other players.
- The growth board tutorial can freeze the screen after the first board opens — a bug of the game itself, present online too. Restart the game.

## Settings

`config.ini`, next to the server; edit, save, restart.

| | |
|---|---|
| `reopen_events` / `events.ini` | bring ended solo events back, all or one by one |
| `keep_expired_items` | keep event currencies usable after their date |
| `infinite_crystals`, `infinite_paid_crystals`, `infinite_stamina`, `infinite_gil` | never spend them |
| `unlock_season_pass`, `season_pass` | open the paid pass track; pick the season (0 = newest) |
| `solo_counts_as_coop` | solo battles count for co-op missions (on by default) |

## Command-line options

Open a command prompt in the game folder (type `cmd` in the Explorer address bar) and start the server with the options; it then runs as usual and the game starts.

| | |
|---|---|
| `FF7ECServer.exe --give NAME=COUNT` | add currency or items to your account, once per thing, as many as you like |
| `FF7ECServer.exe --reopen-events` | bring back every ended solo event, ignoring `events.ini` |
| `FF7ECServer.exe --reset-account`, `--restore-account FOLDER` | see *Starting over* |

**`--give`** — the names: `crystals`, `red_crystals` (paid), `gil`, `stamina`, `chocobo_medals`, `weapon_medals`, `crisis_medals`, `dungeon_keys`, `gear_vouchers`, `memory_vouchers`, `parts`; anything else is `item=ID=COUNT` with the id from `items.txt` (next to the server: every item, its type and name — draw tickets are one id per banner).

```
FF7ECServer.exe --give crystals=3000 --give gil=200000
FF7ECServer.exe --give item=9003=100 --give item=10012=30
```

The amounts land in the account before the game starts and show at the next login. The `infinite_*` settings in `config.ini` are the alternative: nothing is ever spent.

## Starting over

- **"Reset Game Data"** in the title menu: a fresh account, the tutorial from the start; downloaded data is kept.
- `FF7ECServer.exe --reset-account`: the same from outside the game, when it will not start (a copy of the old account and save is kept in `backups\<stamp>-reset`).
- `FF7ECServer.exe --restore-account backups\<folder>`: put a backed-up account and save back (what they replace is backed up too).

