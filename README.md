# VATSIM EuroScope and Audio for VATSIM on non-Windows

This is a script that's meant to facilitate installing an ATC-environment for Linux/Mac users.

If everything goes well, it does not require any additional interaction.

As both the essential VATSIM ATC programs [EuroScope](https://www.euroscope.hu/) and
[Audio for VATSIM](https://audio.vatsim.net/) are Windows-only (why?!), this uses `wine` as emulation layer.

## Current recommendation

2022-02: Audio for VATSIM does currently not run with `wine`. Installing EuroScope in `wine` works though and runs fine.
But we don't need Audio for VATSIM any more because there is now a project that aims to provide a native client for all platforms. 

Recommendation: 

Use this script only to install EuroScope and its newest beta (`./euroscope-afv-wine_install.sh --euroscope`) (see "Usage" below).

For audio use the Mac/Linux AfV client project [pierr3/VectorAudio](https://github.com/pierr3/VectorAudio). You can find downloads under "[Releases](https://github.com/pierr3/VectorAudio/releases)".
This is in beta state but mostly usable. It needs people testing it. Please report problems with it on [pierr3/VectorAudio issues](https://github.com/pierr3/VectorAudio/issues).


## Requirements:

* `bash`, `unzip`, `grep`, `wget`
* `wine` and `winetricks`. Suggested (unsure if needed): Packaged `wine-gecko` and `wine-mono`
* You will see a warning if something is missing.

## Usage:

```
# ./euroscope-afv-wine_install.sh --help
Usage: euroscope-afv-wine_install.sh [<options>]
  <options>:
        -h|--help       this help
        -a|--afv        install only afv
        -e|--euroscope  install only EuroScope
        -B|--no-euroscope-beta do not install EuroScope beta
        -y|--yes        no confirmations
        -v|--verbose    echo all script commands
```

```bash
# create a new directory for your wine environment and change into it
wineDir=$USER/VATSIM-ATC/wine
mkdir -p "$wineDir"
cd "$wineDir"

# download the installer script
wget https://raw.githubusercontent.com/jonaseberle/euroscope-afv-wine/main/euroscope-afv-wine_install.sh

# make executable
chmod +x euroscope-afv-wine_install.sh

# check its options
./euroscope-afv-wine_install.sh --help

# .. and execute it
./euroscope-afv-wine_install.sh --euroscope
```
You'll find your configured "Documents" directory (`xdg-user-dir DOCUMENTS`) labelled "Documents" in the Windows file
browsers, too. This can be adjusted with `winecfg`. EuroScope expects its settings files at `"Documents"/EuroScope`.

## Tested with:

* wine 7.5
* wine 7.0-rc5
* wine 6
* Manjaro, Ubuntu 20.4
* please report your successes/failures with other environments

## Known issues:

* 2022-03: Arch/Manjaro's wine 7.3 is not able to start EuroScope. The problem is [this Arch/wine bug](https://bugs.winehq.org/show_bug.cgi?id=52614).
  Workaround: use the package `wine-staging`. 
* Audio for VATSIM sometimes starts fine, then on another day it might not start any more. It probably has something to
  do with its internal updater. Recommendation: Do not install AfV.
* EuroScope hangs on quitting, after saving changed settings.
  ([WineHQ AppDB entry](https://appdb.winehq.org/objectManager.php?sClass=version&iId=32239))
* [AFV_BRIDGE](https://github.com/AndyTWF/afv-euroscope-bridge) does not work. EuroScope
  message: `AFV_BRIDGE: Unable to open communication for AfV Bridge`.
* [VCH Plugin](https://github.com/DrFreas/VCH) outputs a message but seems to work fine. EuroScope
  message: `ERROR DATA: ERROR: Request didn't work`.

If you have any updates on these, please report. I would like to keep this list up-to-date.

## Suggestions:

Try updating `winetricks` if you experience problems with the "Installing libs…" step:

```bash
[sudo] winetricks --self-update
```

## Contact:

Contributions of any form are very welcome. You can approach me via the "discussions" or "issues" functions here
(prefered) or via my [VATSIM forums profile](https://forums.vatsim.net/profile/191848-jonas-eberle/).

## Thank you

This is built on top of the work of Samir Gebran https://forums.vatsim.net/topic/31019-euroscope-on-linux-howto/.

Thank you to the creators of the EuroScope and Audio for VATSIM programs. 
It is a pity that they are not available cross-platform natively.
