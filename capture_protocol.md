# Capture protocol (Route 2: stock apps) — follow literally

**You need:** an iPhone 15 or newer (a Pro / Pro Max for the LiDAR tier), the printed scale
marker `docs/scale_marker_A4.pdf` (video and photo tiers only), and a Mac or PC with this repo
installed (README, step 1). All lights on, curtains open, interior doors fully open.

**Before any tier:** print the marker at **100 % / "Actual size"**. Check with a ruler that the
black square is **180 mm**; if it is not, reprint. Place it flat on the floor near the middle of
each room you capture, not under furniture. Move it to the next room as you go.
(LiDAR tier: the marker is not needed but does no harm.)

## LiDAR tier (iPhone Pro / Pro Max only) — app: **Stray Scanner** (free, App Store)

1. Open Stray Scanner, tap the record button. Hold the phone upright at chest height.
2. Start in the hallway/connector. Walk **slowly** (one small step per second).
3. In every room, walk along the walls about 1 m away from them. **At each wall, tilt the
   phone from the floor up to the ceiling and back down**, so the screen shows the line where
   wall meets ceiling. Then point at the ceiling for 2 seconds.
4. At every doorway, stop **in the doorway for 2 seconds** and aim at the door frame, then look
   into the next room before walking through.
5. Visit every room once, then **return to where you started** and point at the first wall
   you recorded for 3 seconds. Stop recording. Keep one walk under 6 minutes; split a large
   home into two walks that share one room.
6. Do not: point at a mirror for more than 1 second, let people walk in front of the phone,
   run, or cover the top-back of the phone (LiDAR sensor) with your fingers.

## Video tier (any iPhone 15+) — app: built-in **Camera**, mode **Video**

1. Settings → Camera → Record Video → **1080p at 30 fps**. Turn off Cinematic and Action mode.
   Use the normal **1×** lens. Do not zoom.
2. Put the marker on the floor of the first room. Press record. Walk the same route as the
   LiDAR tier (steps 2–5 above), panning slowly — about 3 seconds to turn 90°.
3. In each room, **point at the marker from about 1.5 m for 3 seconds** (move it to the next
   room before entering it, or use several printed markers with the same pattern).
4. One continuous clip. Stop recording when back at the start.

## Photo tier (any iPhone 15+) — app: built-in **Camera**, mode **Photo**

Per room, take **5 to 8 photos**, all at chest height, phone held **sideways (landscape)**, 1× lens:

1. **4 corner photos:** stand in each corner and photograph the opposite corner, so each photo
   shows floor, two walls and the ceiling line. The marker must be visible in at least two.
2. **One doorway photo per doorway:** stand in the doorway and photograph **into the next room**.
   This photo goes into the folder of the room you are standing in. Do the same from the other
   side when you capture the next room.
3. Do not stand where a mirror shows you. Do not use flash or Live Photo effects.

Make one folder per room on the computer, named after the room (e.g. `bedroom_1`,
`hallway`), and put that room's photos in it. All room folders go inside one parent folder.

## Hand-off (all tiers)

Copy the files to the computer with AirDrop or the Files app:
* LiDAR: Stray Scanner → Library → the recording → Share → Save to Files (a folder).
* Video: the `.MOV` file. Photo: the parent folder of room folders. HEIC or JPEG both work.

Then run **one command** (the tier is detected automatically):

```
python -m roomscan run <the folder or .MOV file> --out out/<any name>
```

Open `out/<name>/plan.png` for the floor plan; `plan.json` has every number with its interval.
