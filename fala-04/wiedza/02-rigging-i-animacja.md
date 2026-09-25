# Rigging i animacja postaci do gier

Opracowanie na podstawie dokumentacji repozytoriów fali 04: GameRig, Game-Human-Rig, Unity Animation Rigging, AutoTPose, 3DCharacter, tutorial Miny Pêcheux, Proscenio i Spine Animation AI.

## 1. Rig do gry to nie rig do filmu

Rig ma dwie warstwy: **kości deformujące** (poruszają siatkę) i **kontrolery** (wygodne uchwyty dla animatora). Do silnika eksportujesz tylko kości deformujące.

Autor GameRig wskazuje trzy problemy standardowego Rigify w grach:

1. kości deformujące nie tworzą jednej hierarchii, więc eksport ciągnie zbędne kości;
2. kości deformujące mają skalę, którą silniki interpretują inaczej niż Blender;
3. „bendy bones” deformują w Blenderze inaczej niż zwykłe kości w silniku.

GameRig (dodatek do Rigify, GPL-2.0) generuje jedną czystą hierarchię, bez skali na kościach deformujących i bez bendy bones. Game-Human-Rig (MIT, [paczka](../paczki/game-human-rig.zip)) omija Rigify: to gotowy plik .blend z dwiema zrigowanymi siatkami (męską i żeńską, na bazie demo Blendera) oraz kilkoma przykładowymi animacjami, m.in. sprintem; ma się importować do Unity i Unreal. Jego autor wskazuje dodatek Expy-Kit do konwersji rigów Rigify.

## 2. Poza spoczynkowa i retargeting

Retargeting przenosi animację z jednego szkieletu na inny. Działa pewniej, gdy obie postacie mają tę samą pozę spoczynkową (zwykle T-pose lub A-pose) i podobne nazwy kości.

**AutoTPose** (MIT, [kod](../paczki/kod-autotpose-blender.zip)) w Blenderze:
- rozpoznaje nazewnictwo Mixamo, Rigify i Unreal, a przy nietypowych nazwach używa hierarchii i geometrii;
- wyrównuje ramiona względem osi barków, a nie sztywnej osi świata;
- domyślnie zmienia tylko pozę; `APPLY_AS_REST_POSE = True` zapisuje ją jako nową pozę spoczynkową. Ta zmiana może zepsuć istniejące animacje.

## 3. Animacje Mixamo — na co uważać

Przykład `aaronsnoswell/3DCharacter` pokazuje typowe poprawki animacji Mixamo pod Godot: skala, timing i przesunięcie w pętli chodu/biegu. Plik zawiera m.in. idle, chód, bieg, kucanie, skradanie, skok, przewrót i krok w tył. Repozytorium nie ma licencji, a treści Mixamo podlegają warunkom Adobe — zostało tylko w lokalnej bazie.

## 4. Root motion

Sufiks `_RM` w animacjach Mesh2Motion (np. `Roll_RM`, `Dodge_left_RM`) oznacza **root motion**: przesunięcie postaci zapisane w animacji. Wersja bez `_RM` animuje w miejscu, a ruch nadaje kod. Wybierz jeden model na postać. Mieszanie obu powoduje „ślizganie” lub podwójny ruch.

## 5. IK i animacja proceduralna w Unity

Pakiet **Unity Animation Rigging** (kopia needle-mirror, Unity Companion License) daje gotowe więzy, oparte na C# Animation Jobs: Two Bone IK (ręka/noga), Chain IK (łańcuchy, np. ogon), Multi-Aim (patrzenie głową), Multi-Parent (broń przechodząca z ręki do ręki), Damped Transform (opóźnione, „miękkie” elementy), Twist Correction, Override Transform, Blend oraz Multi-Position/Rotation/Referential.

Tutorial Miny Pêcheux łączy Two Bone IK z prostym skryptem C#: cel stopy trzyma się ziemi, a gdy ciało odejdzie za daleko, skrypt przestawia stopę z wygładzeniem. Tak powstaje proceduralny chód pająka lub robota. `TeckUnity/AnimationRiggingPlayground` dokłada własne więzy (remapowanie transformacji, ramię 6DOF). Warsztat Unity z SIGGRAPH 2019 zawiera sceny do nauki pakietu. Oba repozytoria i warsztat są tylko lokalnie (brak licencji).

## 6. Animacja 2D: cutout i szkielety

**Proscenio** (GPL-3.0) to pipeline Photoshop → Blender → Godot 4: warstwy PSD z tagami trafiają do Blendera, gdzie powstaje siatka, rig, wagi i animacja. Do Godot trafia scena z natywnych węzłów `Skeleton2D`, `Bone2D`, `Polygon2D`, `AnimationPlayer`, więc gra nie wymaga wtyczki w czasie działania. Kroki są idempotentne: ponowny eksport nie niszczy Twojej sceny-opakowania.

**Spine Animation AI** (PolyForm Noncommercial — tylko do celów niekomercyjnych) to skill dla agenta AI generujący animacje Spine 4.2. To dobry przykład struktury skilla dla własnego bota; licencja nie pozwala na komercyjne użycie.

## 7. Minimalny test postaci

1. Import modelu w skali silnika (1 jednostka = 1 m).
2. Poza spoczynkowa widoczna w edytorze silnika, bez przekręconych kości.
3. Idle, chód, bieg — płynne przejścia bez przeskoku w miejscu pętli.
4. Stopy nie ślizgają się względem prędkości postaci.
5. Kolizja postaci jest kapsułą, nie siatką.

[Automatyczny rigging Mesh2Motion](03-mesh2motion.md) · [Katalog: Animacja i rigging](../katalog/18-animacja-rigging.md)
