# Attribution

## Steam Achievement Caretaker is based on Steam Achievement Manager

Steam Achievement Caretaker derives, directly and substantially, from **Steam Achievement
Manager (SAM)** by **Rick — [gibbed](https://github.com/gibbed)**:

- Upstream project: <https://github.com/gibbed/SteamAchievementManager>
- Original copyright: © 2008–2024 Rick (rick 'at' gibbed 'dot' us)
- Original licence: [zlib](https://opensource.org/licenses/Zlib)

SAM was released as closed source in 2008, had its last major release in 2011 and a hotfix
in 2013, and was later opened so that others could build on it. This project is one of
those derivatives.

Caretaker is an **altered source version** of SAM, and says so:

- in the header of every source file, together with the full zlib notice;
- in [`README.md`](../README.md);
- in [`docs/RELEASE-NOTES.md`](RELEASE-NOTES.md);
- in [`CLAUDE.md`](../CLAUDE.md), so that coding agents keep it that way;
- in the `Copyright` and `Description` properties of both assemblies, so it survives into
  the compiled binaries.

Removing any of those would break the licence, not just the courtesy.

## What Caretaker inherited

Essentially all of the native interop is SAM's work, carried over with renames only:

- the vtable marshalling layer (`NativeWrapper`, `NativeClass`, `NativeStrings`);
- the `ISteam*` interface layouts and their wrappers;
- the callback pump;
- the Valve KeyValues parsers, binary and text;
- the achievement and statistics model.

## What Caretaker changed

- Merged `SAM.Picker.exe` and `SAM.Game.exe` into one executable that dispatches on its
  command line, and renamed `SAM.API` to `SteamAchievementCaretaker.SteamApi`.
- Replaced the Windows Forms UI with Avalonia.
- Migrated from .NET Framework 4.8 to .NET 10, including 64-bit and non-Windows targets.
- Added the SQLite library and achievement caches and the icon cache.
- Rebuilt the game list around achievement completion, with collections, sorting and two
  view modes.
- Fixed the `GetISteamApps` interop signature and the `GetSteamID` struct-return ABI.

The per-version detail is in [`RELEASE-NOTES.md`](RELEASE-NOTES.md).

## Licence position — needs a decision

The repository currently carries **two** licence files, and they do not agree:

| File | Says |
|---|---|
| `LICENSE` | MIT, © 2026 Yaroslav V Tatarenko |
| `LICENSE.txt` | zlib, © 2008–2024 Rick (gibbed) — the upstream notice |

The derived code is bound by zlib regardless: clause 3 says the notice may not be removed,
and clause 2 requires altered versions to be plainly marked. Every source file therefore
carries the zlib notice, and `LICENSE.txt` must stay.

What is unresolved is whether the *new* work in this repository is offered under MIT
alongside that, or whether the whole project should simply be zlib like its parent. Both
are defensible — zlib and MIT are both permissive, and zlib does not forbid distributing a
derivative under additional terms as long as the notice survives — but shipping two licence
files without saying which governs is the one option that helps nobody.

**Recommended:** keep the project zlib-licensed, matching upstream, and drop `LICENSE` — or
keep `LICENSE` and add a sentence to it saying it covers only the changes made in this
repository, with the code as a whole remaining under zlib. Until that is decided, treat
`LICENSE.txt` as governing.

## Trademarks

Steam is a trademark of Valve Corporation. This project is not affiliated with, endorsed
by, or sponsored by Valve Corporation, nor by the author of Steam Achievement Manager.

## Third-party components

| Component | Licence |
|---|---|
| [Avalonia](https://avaloniaui.net/) | MIT |
| [CommunityToolkit.Mvvm](https://github.com/CommunityToolkit/dotnet) | MIT |
| [Microsoft.Data.Sqlite](https://learn.microsoft.com/dotnet/standard/data/sqlite/) | MIT |
| [SQLitePCLRaw](https://github.com/ericsink/SQLitePCL.raw) | Apache-2.0 |

Earlier SAM releases used the [Fugue Icons](https://p.yusukekamiyamane.com/) set by Yusuke
Kamiyamane (CC BY 3.0). Caretaker ships no icon bitmaps; every icon is a vector geometry
drawn for this project.
