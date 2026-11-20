# Phobos Training Bay — Godot student project

An original first-person level study for Godot 4. It borrows broad design lessons from DOOM's 1993 opening level, E1M1: a safe moment to look around, visual clues about danger, gradually introduced combat, a readable switch/door goal, and a small height change. Its layout, names, geometry, and assets are original.

## Screenshot and gameplay

Click the screenshot to open the gameplay recording:

> This is the earlier gameplay capture. It does not yet show the lesson 3–4 changes below; make a fresh capture before submitting the updated project.

[![Phobos Training Bay gameplay screenshot — click to open the video](media/phobos-training-bay.png)](media/phobos-training-bay.mp4)

[Open the MP4 directly](media/phobos-training-bay.mp4)

## Run it

1. Install Godot 4.x.
2. In Project Manager, choose **Import** and open `D:\DoomGodot\project.godot`.
3. Open the project and press **F6** or the **Run Project** button.

## Controls

- **WASD / arrows** move; **mouse** looks
- **Left click**, **Ctrl**, or **Space** fires the pistol
- **E** activates the door control and exit console
- Running is the default; hold **Shift** to walk; **Esc** releases the mouse (click the game to capture it again)

## What to notice

- The entry bay is quiet so the player can learn movement and inspect the scene.
- A dropped equipment case and warning light tell a small story without a cutscene.
- Green status panels, steel supports, tiled floors, and contrasting light suggest an industrial science-fiction base.
- The route widens and changes height before the first enemy encounter.
- The control pedestal is beside a visible locked door, making the result of the interaction clear.
- The blast door spans the full two-cell-deep opening; its collision volume matches the visible panel, so the player cannot walk around it through the adjacent tile.
- Enemies are pixel sprites that face the camera from every angle. Imps launch visible fireballs whenever they can see the player within range. Shots use a camera-centered raycast; Imps take two hits. The HUD tracks health, armor, and ammo.
- The game renders at a 320×200 internal resolution scaled up to echo DOS-era display constraints.

## Crash course lessons 3 and 4

The Net Ninja crash course builds an Asteroids-style 2D game, so these ideas are adapted to this original first-person project instead of adding literal space meteors to an indoor Phobos base.

| Lesson concept | How this project applies it |
| --- | --- |
| [#3 — Physics & Signals](https://www.youtube.com/watch?v=nBCcnPAMvBg) | Player and Imp movement run in Godot's physics update. Enemy fireballs are `Area3D` objects that move with a velocity and detect collisions through the `body_entered` signal. A `hit_player` signal carries damage to the game, while `health_changed`, `door_unlocked`, and `level_completed` connect gameplay events to the HUD and level state. |
| [#4 — Adding Meteors](https://www.youtube.com/watch?v=MWE4d5Wtqbk) | The reusable fireball scene is instantiated when an Imp attacks, given a direction and speed, and cleaned up when it hits something or its lifetime ends. It applies the tutorial's spawned moving-hazard pattern to the setting's demon projectile. |

The fireball implementation lives in `fireball.tscn` and `fireball.gd`; the scene is spawned and its signals are connected in `main.gd`.

### Suggested screen-recording narration

1. “For lesson 3, the player and enemy use Godot physics updates. The Imp's fireball is an Area3D, and its body-entered signal detects a hit.”
2. “The projectile emits a hit-player signal with its damage. The main level updates health and refreshes the HUD when that event arrives.”
3. “For lesson 4, I used the meteor lesson's spawnable moving object idea for an Imp fireball. The level instantiates the reusable scene, aims it at the player, and lets physics collisions remove it on impact.”
4. “I also connected signals for unlocking the blast door and completing the level, so those interactions are separate events rather than direct UI changes.”

## DOOM development history

### From a new engine to an announcement (1992–January 1993)

id Software began planning DOOM after Wolfenstein 3D. John Carmack explored technology for a more expressive first-person world while the team debated what the game should become. Tom Hall, the early creative director, wrote the DOOM Bible, a design document with a more detailed story and characters. The finished game retained the broad science-fiction-versus-demons premise but left out many of those story plans. John Romero later described the team’s approach as experimental: they tried ideas, kept what worked, and removed things that did not.

On January 1, 1993, id announced DOOM publicly, describing ambitious graphics and network play before the game was finished. Romero later recalled that the engine was running in January. The team was building the game and its tools together rather than completing a long, separate preproduction phase. [Romero’s retrospective](https://rome-ro.squarespace.com/news/2018/12/10/reflections-on-dooms-development) and the [GDC postmortem summary](https://www.gamespot.com/articles/romero-and-hall-on-creating-doom/1100-6302251/) describe this early process.

### Building the engine, editor, and levels (1993)

Carmack led engine programming. Romero worked across programming, game design, and level design; Hall shaped the early creative direction; Adrian Carmack and Kevin Cloud made art. The team created DoomEd, a graphical level editor, alongside the engine. Romero and Carmack worked on different parts of the editor, using NeXT workstations and NeXTSTEP while the game itself targeted DOS PCs. This tight loop between engine, editor, and level design let them try ideas directly in playable maps.

DOOM is often called **2.5D**. The player sees a 3D-like first-person view, but the original engine did not build arbitrary stacked 3D rooms like a modern engine. Its sector-based world supported textured floors and ceilings, different heights, stairs, platforms, angled walls, doors, and changing light. Enemies and objects were drawn as sprites that turned toward the viewer. Those limits still gave designers a much wider palette than the straight, single-height corridors of Wolfenstein 3D. [Romero’s account](https://rome-ro.squarespace.com/news/2018/12/10/reflections-on-dooms-development) and this [history of DoomEd and E1M1](https://www.shacknews.com/article/99662/stairway-to-badass-the-making-and-remaking-of-doom?page=6) explain the tools and design changes.

### Changing the story and finishing the game (mid–late 1993)

During production, the team favored fast action, exploration, and atmosphere over the larger story outlined in the DOOM Bible. Hall left id in August 1993. Romero’s retrospective says Sandy Petersen and Dave Taylor joined to help finish the game. Romero also described adding co-op and deathmatch late in development; he chose the name “deathmatch” for the competitive mode. The [GDC postmortem summary](https://www.gamespot.com/articles/romero-and-hall-on-creating-doom/1100-6302251/) recounts the team changes and final push.

Romero designed E1M1, “Hangar,” near the end of development. He said that making the first level last let him use the team’s finished visual language, enemies, and environmental storytelling. The opening gives players time to look around before escalating. Room size and height change along the route, supplies help guide the player, and a distant Imp previews the fireballs that will become a familiar threat. Romero discussed this “make your first level last” approach in a [later interview](https://www.shacknews.com/article/136450/becoming-doomguy-john-romero-on-his-memoir-and-a-life-in-games).

DOOM’s first shareware release appeared on December 10, 1993, through the University of Wisconsin’s FTP server. The first episode, **Knee-Deep in the Dead**, was distributed as shareware; players could order the remaining episodes. The team’s use of shareware and mod-friendly data helped the game spread beyond conventional retail distribution. The release date and upload story are covered in the [GDC postmortem summary](https://www.gamespot.com/articles/romero-and-hall-on-creating-doom/1100-6302251/).

### The DOS game continued to change

The version people remember today was not frozen at the initial release. For example, a computer room was added to E1M1 in the 1.9 update in 1995; Romero said that earlier versions had a simpler hallway there. Comparing old releases is useful when researching “the first version” of DOOM, because later DOS versions changed levels and details. See the [E1M1 development history](https://www.shacknews.com/article/99662/stairway-to-badass-the-making-and-remaking-of-doom?page=6).

### How this project relates to DOOM

This is a Godot 3D exercise inspired by the original game’s design and technical constraints; it is not a recreation of the DOS engine, original map, or copyrighted art. The project uses simple 3D geometry for the environment, camera-facing pixel sprites for enemies, and a low-resolution viewport to study some of the choices that shaped the original experience.

## Research questions

1. How does E1M1 let the player explore before combat begins?
2. What visual details suggest that something dangerous has happened?
3. How do changing room sizes, heights, lights, and enemy placement shape the pace?
4. Why did a 2.5D engine need sprites for enemies, and how does that compare with this Godot project?
5. Which parts of the DOOM Bible remained, and which were changed or dropped before release?
6. Compare this original layout with E1M1. Which broad ideas did this project borrow, and which details are different?
7. Compare early and later DOS releases of E1M1. What changed, and how does that affect your definition of “the first version”?

## Sources

- [John Romero, “Reflections on DOOM’s Development”](https://rome-ro.squarespace.com/news/2018/12/10/reflections-on-dooms-development) — firsthand retrospective on the engine, DOOM Bible, tools, art pipeline, and team.
- [GameSpot, Romero and Hall on creating DOOM](https://www.gamespot.com/articles/romero-and-hall-on-creating-doom/1100-6302251/) — summary of their 2011 GDC postmortem, including the team timeline and release.
- [Shacknews, “The Making and Remaking of Doom”](https://www.shacknews.com/article/99662/stairway-to-badass-the-making-and-remaking-of-doom?page=6) — DoomEd, E1M1 design, and later map changes.
- [Shacknews, John Romero interview](https://www.shacknews.com/article/136450/becoming-doomguy-john-romero-on-his-memoir-and-a-life-in-games) — Romero’s explanation of making the first level last.
- [Game Engine Black Book: DOOM](https://fabiensanglard.net/b/gebbdoom.pdf) — technical history and a foreword by John Romero.
- [id Software’s released DOOM source code](https://github.com/id-Software/DOOM) — source for studying the released engine code.

For your write-up, distinguish firsthand comments from later historical interpretation, and cite the sources you use.
