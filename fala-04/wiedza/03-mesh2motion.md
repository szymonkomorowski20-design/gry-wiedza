# Mesh2Motion — darmowy rigging i animacje (alternatywa dla Mixamo)

Mesh2Motion to otwarta aplikacja webowa (kod MIT, modele/rigi/animacje CC0). Importujesz model, dopasowujesz szablon szkieletu i eksportujesz postać z animacjami. W przeciwieństwie do Mixamo obsługuje nie tylko ludzi.

## Przepływ pracy (wg README aplikacji)

1. Zaimportuj model 3D — obecnie tylko **GLB/glTF**. Z FBX/OBJ najpierw wyeksportuj GLB, np. w Blenderze.
2. Wybierz typ szkieletu.
3. Dopasuj szkielet do wnętrza modelu i opcjonalnie przetestuj deformację.
4. Przetestuj animacje.
5. Zaznacz wybrane animacje i wyeksportuj (GLB/glTF).

Aplikacja działa online (app.mesh2motion.org) albo lokalnie: Node.js, `npm install`, `npm run dev`; jest też Docker (`docker-compose up -d`, port 3000). Wersja desktopowa (Tauri) jest w budowie.

## Szkielety i animacje w paczkach fali 04

[mesh2motion-animacje-glb](../paczki/mesh2motion-animacje-glb.zip) zawiera szkielety (`rig-*.glb`), modele bazowe (`model-*.glb`) i zestawy animacji. Klipy odczytano bezpośrednio z plików GLB:

| Szkielet | Liczba klipów | Przykłady |
|---|---:|---|
| Człowiek — bazowe | 87 | Idle_A, Jog, Crouch_Walk, Roll/Roll_RM, Punch_Jab, Pistol_Shoot, Pistol_Reload, Chop_Tree, Farm_Harvest, Chest_Open, PickUp_Table, Hit_Knockback |
| Człowiek — dodatkowe | 75 | Backflip, Bow Pull/Release, Climb Ladder, Ledge Hang, Dodge (+RM), Death_A–C, Fighting Idle, Meditate, Levitate |
| Człowiek — motion capture | 16 | Cheer, Fishing Cast/Reel, Golf Drive, Salute, Turn Left/Right 90/180 |
| Lis | 14 | Bark, Bite, Howl, Sneak, Sit, Fetch, Run |
| Koń | 14 | Trot, Rear, Kick, Eating, Sleep, Turn_Left/Right |
| Kaiju | 10 | Roar, Tail Attack, Swim, Walk RM |
| Pająk | 10 | Attack, Bite, Jump, Eating |
| Wąż | 8 | Coiled, Side winding, Bite |
| Rekin | 7 | Swim Horizontal/Vertical, Dead Floating |
| Ptak / smok | 5 / 5 | Flap, Glide, Fly Flap, Fly Glide |

Sufiks `RM` oznacza root motion — [wyjaśnienie](02-rigging-i-animacja.md#4-root-motion). Klip „Rest Pose” pomaga sprawdzić dopasowanie.

- [mesh2motion-postacie-warianty](../paczki/mesh2motion-postacie-warianty.zip): 40 zrigowanych wariantów, m.in. policjanci, SWAT, kombinezony hazmat, zombie, potwory, lekarz, oraz warianty lisa, ptaka, ryby i kaiju. Służą do testów i prototypowania NPC.
- [mesh2motion-rigi-blender](../paczki/mesh2motion-rigi-blender.zip): źródłowe rigi Blendera dla 9 szkieletów i szablony kości — do tworzenia własnych animacji zgodnych z aplikacją.

Pełne źródła (rigi z animacjami, surowe nagrania BVH, skrypty Python, paczki CC0) są w lokalnej `BAZA-AI/fala-04/zrodla/Mesh2Motion--mesh2motion-assets`.

## Własny mocap → Mesh2Motion (wg README folderu motion-capture)

1. Zduplikuj plik konfiguracji Blendera z rigiem IK człowieka.
2. Zaimportuj BVH ze skalą **0,01**.
3. Uruchom `retarget-master.py`: wyrównuje kości i tworzy kości pole IK.
4. W dodatku Rokoko Retargeter wczytaj mapowanie kości (jest plik JSON) i wykonaj retarget.

## Zastosowanie w silniku

- **Godot 4**: przeciągnij GLB do projektu. Animacje trafią do `AnimationPlayer`; stan ruchu zbuduj w `AnimationTree`.
- **Unity**: zaimportuj GLB przez pakiet glTFast albo przekonwertuj do FBX. Dla humanoida ustaw Avatar i sprawdź mapowanie kości.
- **three.js**: `GLTFLoader` + `AnimationMixer`, klip wybierasz po nazwie.

Szkielety Mesh2Motion mają własne nazewnictwo kości. Retargeting do Mixamo lub Unity Humanoid wymaga mapowania.

[Rigging i animacja — podstawy](02-rigging-i-animacja.md) · [Pobrane paczki](../paczki/README.md)
