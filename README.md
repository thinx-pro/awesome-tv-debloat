# awesome-tv-debloat

**Open-source ways to get the ads, telemetry and junk off your smart TV, compared.**

Since CleanYourTV went viral on 17 October 2026, dozens of TV debloat projects have appeared on GitHub in ten days: originals, forks, phone apps, launchers, blocklists. This list sorts out which one fits your TV and how you want to do it.

Every entry below was opened and its README read on **2026-10-27**. Star counts are from that day. The facts in the tables are what each project documents about itself; this list has **not** tested them on a TV. Corrections are welcome (see [Contributing](#contributing)).

## Pick in 30 seconds

| Your TV | You have | Use |
|---|---|---|
| Android TV / Google TV (TCL, Sony, Philips, Xiaomi, Hisense, NVIDIA Shield, Chromecast…) | a computer + Claude Code, Codex or another coding agent | [CleanYourTV](https://github.com/Gathin23/cleanyourtv) |
| Android TV / Google TV | only an Android phone | [Clean Your TV app](https://github.com/udhaykumarbala/cleanyourtv-app) or [TV Slim](https://github.com/jolabs40/TVSlim) (phone app) |
| Android TV / Google TV | a Windows PC, no agent | [TV Slim](https://github.com/jolabs40/TVSlim) |
| Android TV / Google TV | Python + adb, want a dry run first | [tvdebloat](https://github.com/colefoster/android-tv-debloat) |
| Android TV / Google TV | want a nicer home screen more than a debloat | [Free My TV](https://github.com/simbasjungles/free-my-tv) |
| LG webOS | no root | [Free My TV](https://github.com/simbasjungles/free-my-tv#lg-tvs-webos) or [FreeMyTvWebOS](https://github.com/danielthejoker18/FreeMyTvWebOS) as a Developer Mode app, plus a [DNS blocklist](#network-level-blocking-any-tv) |
| LG webOS | a rooted TV (webOS 5+) | [CleanYourTV for webOS](https://github.com/lasharor/cleanyourtv-WebOS) |
| Samsung Tizen | — | [Free My TV](https://github.com/simbasjungles/free-my-tv#samsung-tvs-tizen) as a Developer Mode app, [the Tizen storage guide](https://github.com/ardazeytin/samsung-tizen-tv-debloat), and the [tracking settings walkthrough](https://cleanyour.tv/not-android) |
| Amazon Fire TV | — | CleanYourTV's debloat half only (Fire OS won't hand Home to another launcher), or a [DNS blocklist](#network-level-blocking-any-tv) |
| Anything, including Roku and Vizio | a Pi-hole or AdGuard Home | [Network-level blocking](#network-level-blocking-any-tv) |

## Android TV and Google TV

All of these work over ADB on your home network: you turn on developer options and network/USB debugging on the TV, and nothing needs root. Most of them **disable** packages for the main user instead of uninstalling them, so changes can be undone; the Undo column says which.

| Project | How you run it | Also replaces Home | Undo | Stars | License | Notes |
|---|---|---|---|---|---|---|
| [CleanYourTV](https://github.com/Gathin23/cleanyourtv) | Hand the repo to a coding agent (Claude Code, Codex…) on a computer on the same Wi-Fi | Yes, a small native launcher | Restore script; backup made first | 39,960 | Custom (see repo) | The original. Per-model debloat lists from 170+ TV models. Fire TV: debloat only. A few China-market TCL sets refuse any launcher. |
| [Clean Your TV app](https://github.com/udhaykumarbala/cleanyourtv-app) | Android phone app (Android 9+) | Yes, CleanYourTV's launcher | Per-app or full restore; exportable restore scripts | 774 | MIT | No computer or agent needed. A watchdog on the TV restores the stock Home if the phone drops mid-switch. |
| [TV Slim](https://github.com/jolabs40/TVSlim) | Windows app (10/11) or Android phone app | No; switches to a launcher you install | One line or one click | 19 | Apache-2.0 | Package catalogue with side effects per package; re-applies after system updates; also a general ADB toolbox. Tested on TCL and NVIDIA Shield. |
| [tvdebloat](https://github.com/colefoster/android-tv-debloat) | Python 3.8+ CLI + adb (macOS, Linux, Windows) | No (on purpose) | Restore file written before the first change | 0 | MIT | Read-only scan by default, dry run unless `--apply`, sources cited per package; disables by default, `--method uninstall` optional. Never touches Home, setup wizard, Play Store or ADB. |
| [tv-home](https://github.com/mihirgupta0900/tv-home) | Coding agent with one prompt, or scripts by hand (macOS) | Yes | `tools/restore.sh` | 559 | Custom (see repo) | Measured on a 2 GB TCL: home screen memory 192 MB → 83 MB. Documents the Google TV Home-button hijack fix. |
| [Free My TV](https://github.com/simbasjungles/free-my-tv) | Coding agent, or install the release APK with adb | Yes | One button back to the factory Home | 4,898 | MIT | Focus is the home screen: trending picks from your apps (TMDB key needed), weather, your photos. Also runs on LG and Samsung as an app (below). |
| [Android TV Toolkit](https://github.com/seun-novodev/android-tv-debloat-toolkit) | Windows GUI (Python + PySimpleGUI) | Installs FLauncher | Not documented | 786 | MIT | Predates the October wave. Author says it is not actively maintained. |
| [TCL Google TV Optimizer](https://github.com/livvaa/TCL-Google-TV-Debloat-Optimizer) | One PowerShell command | No | Not documented; README says it removes the apps | 7 | MIT | TCL only; README in Turkish. Runs a remote script with `irm … \| iex`, so read it before running. |

Variants of CleanYourTV with a different look or audience: [tvhome-zh](https://github.com/mclhm8182/tvhome-zh) (Chinese, prebuilt 373 KB APK, settings on the remote), [CleanYourTV UI](https://github.com/matheus-caldeira/cleanyourtv-ui) (Free My TV's look with TMDB browsing), [UrTV](https://github.com/tshi-dev/UrTV) (Arabic launcher with prayer times and Hijri date).

## LG webOS

LG TVs have no ADB. Two routes:

| Project | Root needed | What it does | Stars | License |
|---|---|---|---|---|
| [Free My TV](https://github.com/simbasjungles/free-my-tv#lg-tvs-webos) | No (LG Developer Mode; needs a free LG developer account) | Its home screen as an LG app; LG's Home stays, one key press away | 4,898 | MIT |
| [FreeMyTvWebOS](https://github.com/danielthejoker18/FreeMyTvWebOS) | No (Developer Mode) | A webOS port of Free My TV's home screen; Python installer or webOS Dev Manager | 254 | MIT |
| [CleanYourTV for webOS](https://github.com/lasharor/cleanyourtv-WebOS) | Yes ([webOS Homebrew](https://webosbrew.org)) | Replaces LG's Home (RAM-only mount, LG files untouched), optional removal of LG's ad and telemetry services, uninstaller; webOS 5+ | 254 | Custom (see repo) |

Rooting is done with the [webOS Homebrew Channel](https://github.com/webosbrew/webos-homebrew-channel) community's tools and depends on your firmware; read their docs first.

## Samsung Tizen

Samsung TVs have no ADB and very little an owner can change.

- [Free My TV](https://github.com/simbasjungles/free-my-tv#samsung-tvs-tizen) installs its home screen as an app through Samsung's Developer Mode (Tizen, 2015 or newer); Samsung's Home stays.
- [samsung-tizen-tv-debloat](https://github.com/ardazeytin/samsung-tizen-tv-debloat) is an honest guide to what Samsung's `sdb` tool can and cannot do on retail TVs: it can uninstall some store and regional apps when storage is full, and it lists the system packages you must never touch. Verified on one 2018 model.
- [cleanyour.tv/not-android](https://cleanyour.tv/not-android) walks through turning off tracking and ads in the settings with the remote (also for LG, Roku, Vizio and Hisense VIDAA).

## Network-level blocking (any TV)

A DNS blocker on your network (Pi-hole, AdGuard Home) blocks ad and telemetry hosts for every TV, without touching the TV. It can't remove apps or rows from the home screen, and hard-coded IP addresses get around it.

| List | Covers | Stars |
|---|---|---|
| [Perflyst/PiHoleBlocklist](https://github.com/Perflyst/PiHoleBlocklist) | Smart TV (general and AdGuard Home format), Amazon Fire TV, Android tracking | 1,033 |
| [lg-smart-tv-pihole-blocklist](https://github.com/nesdeq/lg-smart-tv-pihole-blocklist) | LG webOS: ads, tracking, ACR, telemetry; an aggressive list and one that keeps the LG Content Store working | 7 |

## Launchers

A launcher replaces the home screen; it doesn't disable anything by itself. Install it **before** disabling the stock home screen, or you can end up with a black screen.

- [FLauncher](https://gitlab.com/flauncher/flauncher) (GitLab): open-source, ad-free Android TV launcher; several debloat tools above install it.
- The launchers bundled with [CleanYourTV](https://github.com/Gathin23/cleanyourtv), [tv-home](https://github.com/mihirgupta0900/tv-home) and [Free My TV](https://github.com/simbasjungles/free-my-tv) can be installed on their own.

## Before you start

- **Turn network debugging off when you're done.** With ADB over the network enabled, anyone on your Wi-Fi can connect to the TV and install apps (tvdebloat's README says this plainly).
- **Disable, don't uninstall**, and keep the restore file each tool writes. Firmware updates can turn things back on; most tools above can re-apply.
- **Don't disable what you can't see the purpose of**: Home, the setup wizard, Settings, the package installer, Play Services. Each tool's list explains its choices; when in doubt, leave it on.
- **Read scripts before piping them into a shell** (`curl … | sh`, `irm … | iex`), especially from forks you haven't seen before.
- **Official links only**: CleanYourTV's README warns that other domains using its name are not run by the project.

## What's not listed

- Plain copies and re-uploads of another project with no documented changes. Many exist; use the original.
- Tools that rely on kernel exploits or DRM bypasses.
- Projects with no README.

## Contributing

Open an issue or a pull request with: the link, the TV platforms it supports, how you run it, whether it needs root, how to undo it, and the license. A project is added once its README documents those things. If you've tested a tool on your own TV, say which model and firmware; that's the most useful thing this list doesn't have yet.

## License

The list itself is [MIT](LICENSE). Each linked project has its own license.
