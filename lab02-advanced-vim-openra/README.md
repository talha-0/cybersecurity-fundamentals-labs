# Lab 2: Advanced VIM and OpenRA

## Goal

Three parts: a short answer on the law around selling a software vulnerability, the rest of `vimtutor`, and fixing a deliberately broken copy of the OpenRA source tree using VIM so the game builds again.

## Tools and concepts

- VIM: line jumps (`:N`, `Ngg`), word motions (`w`, `e`, `$`), `cw`, `x`, `d3w`, range delete, substitution with regular expressions, split windows with yank and paste
- `sed -i`, `chmod 755`, `make`
- OpenRA (open source Red Alert engine, C#) and its YAML rule files
- Computer Fraud and Abuse Act, responsible disclosure

## What I did

- Wrote a 50-word answer arguing that selling a browser exploit online is not allowed, citing the Computer Fraud and Abuse Act, and that responsible disclosure is the safer route.
- Finished `vimtutor` lessons 3 to 7 (about 75 minutes in total by my work log) and the vimgenius level 7 quiz.
- Ran `make all` on the OpenRA tree, read the compiler errors, and fixed the seeded errors across `WAngle.cs`, `Player.cs`, `FieldLoader.cs`, `Actor.cs` and `Download.cs`. There were 13. The first came with a worked example and I recorded the VIM keystrokes I used for the other 12.
- Changed the unit cost in `mods/ra/rules/infantry.yaml` so every infantry unit costs 1.

Examples of the commands I used:

| Task | VIM command |
| --- | --- |
| Comment out a three-line block in C# | `:53,55s/^/\/\//` |
| Delete a block of duplicate lines | `:50,59d` |
| Rename an identifier across a file | `:%s/Actorid/ActorID/g` |
| Remove three repeated words | `2w` then `d3w` |
| Paste a missing function body from another file | `:split file.txt`, visual select, yank, switch window, `p` |
| Set every cost line to 1 | `:%s/Cost: .*/Cost: 1/g` |

## Result

The game built and ran. My screenshot of a single-player mission shows the build menu with Rocket Soldier priced at $1. The screenshot is not in this repository.

## Not included

The broken source tree and the two-line `sed` helper script came from the instructor, so they are not here.
