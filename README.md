# An Anime Game Launcher components index

Index repository for components used in the launcher. Lists wine and dxvk versions. Changes here are automatically distributed to all the launchers

## How to create your own index

### Clone repository

```sh
git clone https://github.com/an-anime-team/components
```

### Modify index

#### Components index (`components.json`):

```ts
{
    wine: Wine[],
    dxvk: Dxvk[]
}
```

```ts
type Wine = {
    name: string,
    title: string,
    ?features: {
        ?need_dxvk: boolean,
        ?command: string,
        ?env: {
            [id: string]: string
        }
    }
}
```

```ts
type Dxvk = {
    name: string,
    title: string,
    ?features: {
        ?env: {
            [id: string]: string
        }
    }
}
```

All string fields here (`command` and `env` values) accept these keywords:

| Keyword | Description |
| - | - |
| `%build%` | path to wine build |
| `%prefix%` | path to wine prefix |
| `%temp%` | path to temp folder specified in config file |
| `%launcher%` | path to launcher folder |
| `%game%` | path to the game |

#### Components index (example):

```json
{
    "wine": [
        {
            "name": "wine-ge-proton",
            "title": "Wine-GE-Proton",
            "features": {
                "env": {
                    "WINEDEBUG": "+all"
                }
            }
        },
        {
            "name": "wine-ge-proton",
            "title": "Wine-GE-Proton",
            "features": {
                "command": "'%build%/custom_script'",
                "no_dxvk": true
            }
        }
    ],
    "dxvk": [
        {
            "name": "vanilla",
            "title": "Vanilla"
        },
        {
            "name": "async",
            "title": "Async",
            "features": {
                "env": {
                    "DXVK_ASYNC": 1
                }
            }
        }
    ]
}
```

#### Wine (`wine/[name].json`):

```ts
[
    {
        name: string,
        title: string,
        uri: string,
        files: {
            wine: string,
            ?wine64: string,
            ?wineserver: string,
            ?wineboot: string,
            ?winecfg: string
        },
        ?features: {
            ?need_dxvk: boolean,
            ?command: string,
            ?env: {
                [id: string]: string
            }
        }
    }
]
```

#### Wine (example):

```ts
[
    {
        "name": "lutris-GE-Proton7-37-x86_64",
        "title": "Wine-GE-Proton 7-37",
        "uri": "https://github.com/GloriousEggroll/wine-ge-custom/releases/download/GE-Proton7-37/wine-lutris-GE-Proton7-37-x86_64.tar.xz",
        "files": {
            "wine": "bin/wine",
            "wine64": "bin/wine64",
            "wineserver": "bin/wineserver",
            "wineboot": "bin/wineboot",
            "winecfg": "lib64/wine/x86_64-windows/winecfg.exe"
        }
    },
    {
        "name": "GE-Proton7-49",
        "title": "GE-Proton 7-49",
        "uri": "https://github.com/GloriousEggroll/proton-ge-custom/releases/download/GE-Proton7-49/GE-Proton7-49.tar.gz",
        "files": {
            "wine": "files/bin/wine",
            "wine64": "files/bin/wine64",
            "wineserver": "files/bin/wineserver",
            "winecfg": "files/lib64/wine/x86_64-windows/winecfg.exe"
        },
        "features": {
            "need_dxvk": false
        }
    
]
```

#### Dxvk (`dxvk/[name].json`):

```ts
[
    {
        name: string,
        title: string,
        uri: string,
        ?features: {
            ?env: {
                [id: string]: string
            }
        }
    }
]
```

#### Dxvk (example):

```ts
[
    {
        "name": "dxvk-2.1",
        "version": "2.1",
        "uri": "https://github.com/doitsujin/dxvk/releases/download/v2.1/dxvk-2.1.tar.gz"
    },
    {
        "name": "dxvk-async-2.0",
        "version": "2.0-async",
        "uri": "https://github.com/Sporif/dxvk-async/releases/download/2.0/dxvk-async-2.0.tar.gz",
        "features": {
            "env": {
                "DXVK_ASYNC": 1
            }
        }
    }
]
```

### Update launcher index servers

Change `components.servers` property in the launcher's `config.json` file. You can put local folder path here as well, e.g.: `file:///home/username/.local/share/anime-game-launcher/my-own-components-index`
