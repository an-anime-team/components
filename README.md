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
        ?no_dxvk: boolean,
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
        "name": "lutris-GE-Proton7-36-x86_64",
        "title": "Wine-GE-Proton 7-36",
        "uri": "https://github.com/GloriousEggroll/wine-ge-custom/releases/download/GE-Proton7-36/wine-lutris-GE-Proton7-36-x86_64.tar.xz",
        "files": {
            "wine": "bin/wine",
            "wine64": "bin/wine64",
            "wineserver": "bin/wineserver",
            "wineboot": "bin/wineboot",
            "winecfg": "lib64/wine/x86_64-windows/winecfg.exe"
        }
    }
]
```

#### Dxvk (`dxvk/[name].json`):

```ts
[
    {
        name: string,
        title: string,
        uri: string
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
        "name": "dxvk-2.0",
        "version": "2.0",
        "uri": "https://github.com/doitsujin/dxvk/releases/download/v2.0/dxvk-2.0.tar.gz"
    }
]
```

### Update launcher index servers

Change `components.servers` property in the launcher's `config.json` file. You can put local folder path here as well, e.g.: `file:///home/username/.local/share/anime-game-launcher/my-own-components-index`
