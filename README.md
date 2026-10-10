# ProceduralEmitterSystem

A lightweight, Blueprint-based procedural audio emitter system for Unreal Engine 5. Spawns a configurable number of spatialized audio emitters at randomised positions within a defined zone, with per-emitter volume variation for natural, non-repetitive ambient sound.

Designed as a drop-in system for ambient audio, swap in any sound and it works. Originally built for wind and forest ambience in the Envirosonics demo, rebuilt as a sound-agnostic tool.

---

## Features

- Procedural spawning of "X" audio emitters within a user-defined bounding box
- Per-emitter randomised volume (0.3 to 1.0) for natural variation
- Logarithmic volume attenuation with configurable inner radius and falloff distance
- Panning spatialization for believable 3D positioning
- Debug sphere visualization in editor so you can see exactly where emitters land
- Timer-based respawning: emitters re-randomise their positions on a loop
- Three layered emitter groups with delay, randomizer, and modulator nodes for additional texture
- Sound agnostic: no audio assets included, plug in your own

---

## Setup

1. Clone or download the project
2. Open `AmbientEmitters.uproject` in Unreal Engine 5.6.1 or later
3. Navigate to `Content/` and open the map
4. In `EmitterSoundCue`, assign your own audio asset in the Sound Wave
5. In `EmitterSpawner_Blueprint`, set the Last Index on the For Loop to control emitter count
6. Resize the Spawn Area box component to cover your desired zone
7. Press Play: debug spheres show emitter positions

---

## Blueprints

**Emitter_Blueprint**: Individual emitter. On BeginPlay, sets a randomised volume multiplier and plays the assigned audio. Debug sphere visualises the emitter position in editor.

**EmitterSpawner_Blueprint**: Spawner controller. On BeginPlay, sets a looping timer that calls SpawnEmitter every 10 seconds. SpawnEmitter gets the bounding box world location and extents, generates a random point within it, and spawns X instances of Emitter_Blueprint at that position via a For Loop.

**EmitterSoundCue**: Three emitter groups, each with five wave players going through delays into a randomiser and modulator before mixing down. Swap the NONE wave players for your own assets, add emitter groups or more effects as needed.

---

## Initial Attenuation Settings

```
Attenuation Function:  Logarithmic
Attenuation Shape:     Sphere
Inner Radius:          2000.0
Falloff Distance:      10000.0
Spatialization:        Panning
```

Adjust inner radius and falloff distance to match your level scale.

---

## Customisation

- Emitter count: change Last Index on the For Loop in EmitterSpawner_Blueprint
- Respawn interval: change Time on the Set Timer node (default 10 seconds)
- Volume range: change Min/Max on the Random Float in Range node in Emitter_Blueprint
- Spawn zone: resize the Box Component on EmitterSpawner_Blueprint in the level

---

## Requirements

- Unreal Engine 5.6.1 or later
- No C++ required: fully functional with Blueprints
- No audio assets included

---

## Context

Part of a broader portfolio of technical audio systems. Related projects:

- [Envirosonics](https://www.youtube.com/@ParthRaneAudio): procedural reactive ambience system in UE5 with Wwise, featuring wildlife that responds dynamically to player interaction
- [Audio Signal Chain Simulator](https://github.com/ParthRaneAudio/AudioSignalChainSimulator-cpp): C++ WAV file processor implementing a five-stage signal chain

---

## Author

**Parth Rane** — Technical Sound Designer  
[Portfolio](https://parthraneaudio.github.io/) · [LinkedIn](https://uk.linkedin.com/in/parthraneprofile) · [YouTube](https://www.youtube.com/@ParthRaneAudio) · [GitHub](https://github.com/ParthRaneAudio)
