Nightvision Reveal — Setup Guide (L_Overview)

1) Open the Level Blueprint
- Open the map:
  Content/NightvisionReveal/Maps/L_Overview
- With the map open, go to:
  Blueprints → Open Level Blueprint

------------------------------------------------------------
PART A — Create the “NightvisionRef” actors array

2) Copy the BeginPlay block
In the Level Blueprint, copy the first block:
- Event BeginPlay
- Get All Actors With Tag (Tag: Nightvision)

3) Create the variable “NightvisionRef”
- From Get All Actors With Tag, right-click the blue pin “Out Actors”
- Choose “Promote to Variable”
- Rename the new variable to: NightvisionRef

4) Use NightvisionRef where needed
- If your graph uses a ForEachLoop, plug NightvisionRef into the loop’s Array input.
- Use the loop’s Array Element as the Target for:
  - Set Actor Enable Collision
  - Set Actor Hidden In Game
(as needed in your setup)

------------------------------------------------------------
PART B — Copy the input/toggle block (Key N)

5) Copy the toggle block
Copy the second section:
- N (Pressed)
- FlipFlop
- Play Sound 2D (ON / OFF sounds)
- Set Actor Hidden In Game
- Set Actor Enable Collision
(and any related nodes in that toggle section)

------------------------------------------------------------
PART C — Create and configure the Post Process Volume (green nightvision)

6) Add a PostProcessVolume to the level
- Place a Post Process Volume in the level
- In Details:
  - Enable “Infinite Extent (Unbound)”  (IMPORTANT: Unbound, not Bound)

7) Set the green tint
- In Misc:
  - Enable “Scene Color Tint”
  - Set the color to green
(Optional) Set the volume’s Blend Weight to 0 so the level starts normally.

------------------------------------------------------------
PART D — Create a reference to the PostProcessVolume in the Level Blueprint

8) Create the reference node
- Select the PostProcessVolume in the level
- Go back to the Level Blueprint
- Right-click → “Create a Reference to PostProcessVolume”

9) Connect the volume reference to the Blend Weight nodes
- Delete any old/incorrect “Post Process Volume” nodes in the graph (wrong references).
- In BOTH “Set Blend Weight” nodes:
  - Connect the PostProcessVolume reference to the BLUE Target pin

Blend Weight values:
- Nightvision ON  → Blend Weight = 1.0
- Nightvision OFF → Blend Weight = 0.0

------------------------------------------------------------
PART E — Replace old references with NightvisionRef

10) Replace old Nightvision arrays/references
- Delete the old Nightvision references wired into:
  - Set Actor Hidden In Game
  - Set Actor Enable Collision
- Drag the variable NightvisionRef into the graph (GET)
- Use it as the array for your ForEachLoop, and apply:

Nightvision ON:
- Set Actor Hidden In Game = false
- Set Actor Enable Collision = true

Nightvision OFF:
- Set Actor Hidden In Game = true
- Set Actor Enable Collision = false

------------------------------------------------------------
EXTRA

11) Change activation/deactivation sounds
- Replace the Sound assets in the “Play Sound 2D” nodes (ON/OFF) with your preferred SFX.