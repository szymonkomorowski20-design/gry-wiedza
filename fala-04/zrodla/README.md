# Źródła i zakres fali 04

Stan opracowania: 25 września 2026. Wszystkie repozytoria pobrano tego dnia (klon płytki, gałąź domyślna) i przypięto do commitu w [manifeście](manifest.json). Lokalna kopia (5,1 GB) jest w `BAZA-AI/fala-04/zrodla` na pulpicie — nie ma jej w repozytorium GitHuba.

Zlecenie zawierało 71 adresów. Po usunięciu duplikatów zostało 48 repozytoriów, 1 Gist, 2 organizacje (sourcesounds, Mesh2Motion) i 13 unikalnych tematów GitHuba. Dwa repozytoria już nie istnieją. Z organizacji Mesh2Motion pobrano dodatkowo 4 repozytoria. Adres `topics/game-assethttps://github.com/topics/game-asset` był sklejeniem dwóch linków — potraktowano go jako temat `game-asset`.

## Dźwięki / SFX

| Źródło | Co zawiera i jak je wykorzystano | Licencja | Nowe wpisy |
|---|---|---|---:|
| [JimLynchCodes/Game-Sound-Effects](https://github.com/JimLynchCodes/Game-Sound-Effects) | 45 plików WAV (wybuchy, strzały, interfejs, power-upy) zebranych przez autora. Autor pisze, że „według jego wiedzy” są royalty-free — brak pliku licencji i źródeł poszczególnych dźwięków. | Brak licencji; pochodzenie dźwięków nieudokumentowane — tylko lokalnie, do prototypów | 1 |
| [zulubo/Zulubo-Sounds](https://github.com/zulubo/Zulubo-Sounds) | 290 WAV autorstwa Zach Tsiakalis-Brown w działach: zniszczenia, otoczenie, kroki, interakcje, fizyka. Dobre do gier 3D z fizyką (upadki, uderzenia, drewno, metal). | MIT + deklaracja „free to use for any purpose” w README | 1 |
| [buckn/game_sounds](https://github.com/buckn/game_sounds) | 33 pliki .bfxrsound — ustawienia generatora bfxr (wybuchy, trafienia, kroki, podnoszenie). Otwiera się je w bfxr, by wygenerować i zmodyfikować dźwięk. | Brak licencji — tylko lokalnie | 1 |
| [Kavex/GameSounds](https://github.com/Kavex/GameSounds) | 22 WAV na licencji GPL-3.0. Licencja programowa dla dźwięków bywa kłopotliwa w zamkniętej grze — sprawdź zgodność z projektem. | GPL-3.0 — nie spełnia reguły CC0/MIT/CC-BY dla paczek GitHuba; lokalnie | 0 |
| [moutend/SoundEffect](https://github.com/moutend/SoundEffect) | 5 krótkich WAV przetworzonych SoX z nagrań Freesound; README pokazuje, jak samodzielnie przyciąć i znormalizować dźwięki (22 kHz, mono, 16 bit). | Brak licencji; oryginały z Freesound mają własne licencje — lokalnie | 8 |
| [freesoundeffects/100-free-soundeffects](https://github.com/freesoundeffects/100-free-soundeffects) | Repozytorium zawiera wyłącznie jednozdaniowe README — brak plików dźwiękowych. | Nie dotyczy | 1 |
| [Cuboos/SS13-Sound-Library](https://github.com/Cuboos/SS13-Sound-Library) | 43 OGG stworzone dla Space Station 13 (TG station): maszyny, broń, otoczenie sci-fi. Brak pliku licencji. | Brak licencji — tylko lokalnie | 1 |
| [mrbid/Sound-Effects](https://github.com/mrbid/Sound-Effects) | 63 WAV wygenerowane syntezatorami Borg: alarmy, sci-fi, obcy, blipy, wobble. Domena publiczna (Unlicense). | Unlicense (domena publiczna) | 1 |
| [arnofaure/free-sfx](https://github.com/arnofaure/free-sfx) | Strona podglądu paczki SFX (alert, input, sci-fi, woosh, głos) na CC BY 4.0. Link do ZIP na studionora.ca zwraca obecnie stronę HTML — paczki nie da się pobrać. | CC BY 4.0 wg README; plik ZIP niedostępny | 3 |

## Animacje / Rigging

| Źródło | Co zawiera i jak je wykorzystano | Licencja | Nowe wpisy |
|---|---|---|---:|
| [readyplayerme/animation-library](https://github.com/readyplayerme/animation-library) | 240 animacji mocap (GLB + FBX) w wersjach męskiej i żeńskiej: idle, chód, bieg, taniec, gesty, emocje. Retargetowane na szkielet Ready Player Me. | Licencja RPM: tylko z awatarami Ready Player Me, zakaz redystrybucji — wyłącznie lokalnie do nauki | 2 |
| [ostef/Game-Human-Rig](https://github.com/ostef/Game-Human-Rig) | Plik .blend z ludzkim rigiem przeznaczonym do gier (lekka hierarchia kości deformujących + kontrolery). Punkt wyjścia do własnych animacji eksportowanych do silnika. | MIT | 2 |
| [aaronsnoswell/3DCharacter](https://github.com/aaronsnoswell/3DCharacter) | Postać Mixamo przygotowana do Godot: idle, chód, bieg, skradanie, skok, przewrót. Pokazuje, jak poprawić skalę i timing animacji Mixamo. | Brak licencji; treści Mixamo mają warunki Adobe — tylko lokalnie | 1 |
| [Arminando/GameRig](https://github.com/Arminando/GameRig) | Dodatek do Blendera generujący rigi zgodne z silnikami gier (osobna hierarchia deformacji, bez ograniczeń nieobsługiwanych przez eksport). | GPL-2.0 (kod dodatku) | 1 |
| [Roboticela/Animator](https://github.com/Roboticela/Animator) | Wieloplatformowy edytor animacji w przeglądarce i na desktopie (Tauri, React, TypeScript). | AGPL-3.0 | 19 |
| [GenielabsOpenSource/spine-animation-ai](https://github.com/GenielabsOpenSource/spine-animation-ai) | Skill dla agenta AI i skrypty do tworzenia animacji szkieletowych Spine 4.2 z grafik 2D; zawiera dokumentację, przykłady i aplikację do reskinu. | PolyForm Noncommercial — zakaz użycia komercyjnego; lokalnie | 14 |
| [firebound/proscenio](https://github.com/firebound/proscenio) | Narzędzia przenoszące postacie 2D (cutout) z Photoshopa i Blendera do Godot 4 z kośćmi i animacjami; obszerna dokumentacja. | GPL-3.0-or-later | 62 |
| [needle-mirror/com.unity.animation.rigging](https://github.com/needle-mirror/com.unity.animation.rigging) | Lustrzana kopia oficjalnego pakietu Unity Animation Rigging: więzy IK (Two Bone IK, Multi-Aim, Chain IK), dokumentacja i przykłady. | Unity Companion License — tylko w projektach Unity | 4 |
| [MinaPecheux/UnityTutorials-ProceduralAnimations](https://github.com/MinaPecheux/UnityTutorials-ProceduralAnimations) | Projekt do tutorialu: IK nóg sterowane skryptem C# (stopy podążają za ciałem), z wygładzaniem. | Brak licencji — lokalnie do nauki | 3 |
| [TeckUnity/AnimationRiggingPlayground](https://github.com/TeckUnity/AnimationRiggingPlayground) | Sandbox z przykładowymi rigami Unity Animation Rigging, własny constraint remapujący transformacje i ramię robota 6DOF. | Brak licencji — lokalnie do nauki | 3 |
| [Isabella98Liu/RigAnything](https://github.com/Isabella98Liu/RigAnything) | Kod badawczy Adobe: model autoregresyjny przewidujący szkielet i wagi skinningu dla dowolnego modelu 3D. | Adobe Research License — tylko niekomercyjne badania | 3 |
| [adamscript/Auto-Rigger](https://github.com/adamscript/Auto-Rigger) | Skrypty Python dla Autodesk Maya tworzące rig postaci z lokatorów. | MIT | 5 |
| [4onstudios/AutoTPose](https://github.com/4onstudios/AutoTPose) | Skrypt Python/Blender ustawiający zrigowaną postać w T-pose przed retargetingiem. | MIT | 4 |
| [loyal-studio/Honami-Animation-System](https://github.com/loyal-studio/Honami-Animation-System) | Pakiet Unity: system animacji oparty na kodzie (268 plików C#) z edytorem i zrzutami ekranu. | MIT | 3 |
| [Mesh2Motion/mesh2motion-app](https://github.com/Mesh2Motion/mesh2motion-app) | Aplikacja webowa: importujesz model 3D, dopasowujesz szablon szkieletu (człowiek, czworonóg, ptak, smok…) i eksportujesz z gotowymi animacjami. Zawiera finalne GLB rigów i animacji. | LICENSE-MIT + LICENSE-CC0 w repozytorium | 7 |
| [Mesh2Motion/mesh2motion-assets](https://github.com/Mesh2Motion/mesh2motion-assets) | Pliki Blendera rigów dla każdego typu szkieletu, animacje, modele, pliki BVH mocap i skrypty Python — źródła assetów Mesh2Motion. | CC0-1.0 | 9 |
| [Mesh2Motion/mesh2motion-desktop](https://github.com/Mesh2Motion/mesh2motion-desktop) | Offline’owa wersja aplikacji na Tauri; README opisuje budowanie na Windows. | Brak licencji w repozytorium | 1 |
| [Mesh2Motion/mesh2motion-godot](https://github.com/Mesh2Motion/mesh2motion-godot) | Na dzień pobrania zawiera tylko plik licencji MIT. | MIT | 1 |
| [Unity-Technologies/animation-rigging-workshop-siggraph2019](https://github.com/Unity-Technologies/animation-rigging-workshop-siggraph2019) | Projekt Unity z warsztatu SIGGRAPH 2019: przykładowe rigi, więzy i sceny do nauki pakietu Animation Rigging. | Brak licencji w repozytorium — lokalnie do nauki | 1 |

## Modele 3D / Tekstury / CC0

| Źródło | Co zawiera i jak je wykorzystano | Licencja | Nowe wpisy |
|---|---|---|---:|
| [ToxSam/open-source-3D-assets](https://github.com/ToxSam/open-source-3D-assets) | Rejestr JSON 18 kolekcji / 991 modeli Polygonal Mind z kategoriami i atrybutami. Bez zmian od fali 03 — teraz połączony z fizycznie pobranymi modelami. | CC0 (metadane) | 0 |
| [ToxSam/cc0-models-Polygonal-Mind](https://github.com/ToxSam/cc0-models-Polygonal-Mind) | 991 modeli GLB z projektów Polygonal Mind (2018–2023) z miniaturami: jarmark średniowieczny, pagody neonowe, piramidy, park, muzeum, transport i inne. Gotowe do Godot, Unity, three.js. | CC0-1.0 (fork PolygonalMind/initiative-opensource-release) | 3 |
| [ToxSam/os3a-gallery](https://github.com/ToxSam/os3a-gallery) | Kod strony opensource3dassets.com (Next.js) — przeglądarka rejestru modeli z podglądem 3D. | Brak licencji w repozytorium | 2 |
| [3dassets-dev/3dassets](https://github.com/3dassets-dev/3dassets) | Pliki dla agentów AI: skill i most MCP do serwisu 3dassets.dev z modelami GLB CC0 — przydatne przy budowie własnego bota. | CC0-1.0 | 31 |
| [devanshutak25/3d-resources](https://github.com/devanshutak25/3d-resources) | Uporządkowana baza 3533 wpisów w YAML: biblioteki modeli, tekstury, HDRI, audio, wtyczki Blendera/Houdini, kursy, mocap AI, oświetlenie, VFX. Każdy wpis ma typ, licencję i datę weryfikacji. | CC0-1.0 | 2935 |
| [kaydee001/3d-resources](https://github.com/kaydee001/3d-resources) | Krótka numerowana lista serwisów z modelami, teksturami i narzędziami 3D (darmowe i płatne). | CC0-1.0 | 9 |
| [madjin/awesome-cc0](https://github.com/madjin/awesome-cc0) | Awesome-lista wyłącznie zasobów CC0: modele, awatary VRM, tekstury, HDRI, audio, muzyka, fonty. | CC0-1.0 | 19 |
| [RayMarch/ferris3d](https://github.com/RayMarch/ferris3d) | Model 3D krabika Ferris (maskotka Rusta) w .blend. | CC0-1.0 | 4 |
| [GuilhermeGraca/blender-warrior-character](https://github.com/GuilhermeGraca/blender-warrior-character) | Postać wojownika w Blenderze pokazująca pipeline od base mesh do tekstur; pliki .blend w dwóch wariantach. | Brak licencji — tylko lokalnie do nauki | 4 |
| [fernandotonon/QtMeshEditor](https://github.com/fernandotonon/QtMeshEditor) | Program (C++/Qt) do otwierania, walidacji, konwersji i naprawy FBX/GLB/OBJ/DAE z GUI i CLI — przydatny w pipeline assetów. | MIT | 15 |

## Sceny / Środowiska / Mapy

| Źródło | Co zawiera i jak je wykorzystano | Licencja | Nowe wpisy |
|---|---|---|---:|
| [djrm/open-game-assets](https://github.com/djrm/open-game-assets) | Tylko jednolinijkowe README — brak zasobów. | Nie dotyczy | 1 |
| [GDQuest/game-sprites](https://github.com/GDQuest/game-sprites) | Bez zmian od fali 03 (wybrane SVG już w paczce gdquest-prototype-sprites). | CC0-1.0 | 0 |
| [czyzby/gdx-skins](https://github.com/czyzby/gdx-skins) | ~40 skórek interfejsu (atlas PNG, JSON, fonty .fnt) m.in. Arcade, Commodore64, Neon, Pixthulhu. PNG da się wykorzystać także w innych silnikach jako grafikę przycisków i okien. | Licencja w README każdej skórki; większość CC BY 4.0 (Raymond „Raeleus” Buckley) | 69 |
| [ahnerd/creative-commons-game-assets-collection](https://github.com/ahnerd/creative-commons-game-assets-collection) | Bez zmian od fali 03. | Brak licencji | 0 |

## Kompletne paczki / Mega-listy

| Źródło | Co zawiera i jak je wykorzystano | Licencja | Nowe wpisy |
|---|---|---|---:|
| [praveencrypty/Game-Development-Resource-Collection-2025](https://github.com/praveencrypty/Game-Development-Resource-Collection-2025) | Bez zmian od fali 03. | Brak licencji | 0 |
| [getvmio/free-game-development-resources](https://github.com/getvmio/free-game-development-resources) | Tabela darmowych zasobów nauki gamedevu (kursy, playgroundy) z kategoriami. | Brak licencji | 74 |
| [notpresident35/The-Gamedev-Resource-Mega-List](https://github.com/notpresident35/The-Gamedev-Resource-Mega-List) | Fork listy „Awesome Learn Gamedev”: programowanie, tech art (shadery, rigging, VFX), grafika, animacja, audio, design, produkcja; z archiwami PDF. | CC0-1.0 | 13 |
| [JackLuguibin/GameAssets](https://github.com/JackLuguibin/GameAssets) | Indeks stron z assetami (postacie, sceny, tekstury, UI, audio, efekty) z uwagami o zgodności licencyjnej; w języku chińskim. | MIT | 31 |
| [teamgravitydev/gamedev-free-resources](https://github.com/teamgravitydev/gamedev-free-resources) | Źródło fali 01; teraz porównano nowszą wersję i dodano tylko nowe adresy. | Brak licencji | 14 |
| [TMHSDigital/Free-Game-Dev-Assets](https://github.com/TMHSDigital/Free-Game-Dev-Assets) | Nowsza wersja niż w fali 03 — przetworzono wszystkie karty, dodano tylko nowe adresy. | CC0-1.0 | 8 |
| [HotpotDesign/Game-Assets-And-Resources](https://github.com/HotpotDesign/Game-Assets-And-Resources) | Bez zmian od fali 03. | Brak licencji | 0 |
| [HotpotDesign/Unity-Game-Assets](https://github.com/HotpotDesign/Unity-Game-Assets) | Poradnik-lista darmowych assetów do gier Unity, 2D i 3D. | Brak licencji | 13 |
| [benfrankel/5332a90d681506292e973eab4efa91e8](https://gist.github.com/benfrankel/5332a90d681506292e973eab4efa91e8) | Tabela serwisów z assetami, fontami, audio i narzędziami z typem i licencją. | Brak licencji Gista | 1 |

## Organizacje i niedostępne adresy

| Źródło | Stan |
|---|---|
| [sourcesounds](https://github.com/sourcesounds) | 21 repozytoriów z dźwiękami gier Valve i modów Source (ok. 18 GB). Brak licencji; to cudza własność. Każde repozytorium opisano w katalogu audio jako referencję. Nie pobrano. |
| [Mesh2Motion](https://github.com/mesh2motion) | 7 repozytoriów; pobrano app, assets, desktop, godot. Pominięto stronę marketingową, stronę zbiórki i `.github`. |
| soundeffectapp/Free-Sound-Effects-Library | 404 — repozytorium nie istnieje (sprawdzono 25.09.2026). |
| abisoftstudios/Open-Source-Assets | 404 — repozytorium nie istnieje. |

## Tematy GitHuba

| Temat | Na GitHubie | Pobrano | W katalogu (≥3★, nowe) |
|---|---:|---:|---:|
| [sound-effects](https://github.com/topics/sound-effects) | 523 | 523 | 147 |
| [sfx](https://github.com/topics/sfx) | 179 | 179 | 70 |
| [animation-rigging](https://github.com/topics/animation-rigging) | 4 | 4 | 1 |
| [3d-animation](https://github.com/topics/3d-animation) | 410 | 410 | 117 |
| [auto-rigging](https://github.com/topics/auto-rigging) | 20 | 20 | 12 |
| [3d-assets](https://github.com/topics/3d-assets) | 78 | 78 | 24 |
| [free-3d-models](https://github.com/topics/free-3d-models) | 4 | 4 | 1 |
| [3d-model](https://github.com/topics/3d-model) | 348 | 348 | 96 |
| [game-assets](https://github.com/topics/game-assets) | 349 | 349 | 105 |
| [game-asset](https://github.com/topics/game-asset) | 14 | 14 | 5 |
| [free-assets](https://github.com/topics/free-assets) | 29 | 29 | 13 |
| [rigging](https://github.com/topics/rigging) | 250 | 250 | 118 |
| [2d-animation](https://github.com/topics/2d-animation) | 125 | 125 | 37 |

Kolumna „W katalogu” liczy repozytoria z co najmniej 3 gwiazdkami przed usunięciem powtórek. Część z nich była już w starszych falach albo w innym temacie. Wszystkie wyniki, także poniżej progu, są w [tematy-github.json](tematy-github.json). Wykluczono 11 repozytoriów z oznakami piractwa, malware lub spamu: [lista z powodami](pominiete-podejrzane.json).

## Zawartość i granice analizy

Zinwentaryzowano 15258 plików (ścieżka, rozmiar, SHA-256 i git-blob dokumentów): [inwentarz](inwentarz-plikow.json). Linki wyciągnięto z README repozytoriów z assetami i kodem, ze wszystkich dokumentów repozytoriów-list i dokumentacji (Proscenio, Mesh2Motion, Spine AI, Unity Animation Rigging, TMHSDigital, gdx-skins) oraz z 201 plików YAML bazy devanshutak25. Pominięto plakietki, obrazki, linki do samych siebie i odnośniki pomocnicze (licencje, media społecznościowe, issues): [lista pomocnicza](odnosniki-pomocnicze.json).

Nie uruchamiano pobranego kodu ani aplikacji (Mesh2Motion, QtMeshEditor, Animator), nie importowano paczek do silników i nie pobierano stron spoza GitHuba. Nazwy klipów animacji i kategorie modeli odczytano bezpośrednio z plików GLB i JSON.

## Autorstwo i licencje

Licencja listy nie jest licencją zasobów, do których odsyła. Na GitHub trafiły tylko paczki CC0, MIT, Unlicense i CC BY 4.0 — szczegóły w [pobrane.json](../pobrane.json). Materiały bez licencji lub z licencją ograniczającą (Ready Player Me, Adobe Research, PolyForm Noncommercial, Unity Companion, GPL/AGPL dla assetów) są tylko w lokalnej BAZA-AI lub jako linki, z opisem ograniczeń. Własne opracowania i opisy udostępniono na CC BY-SA 4.0, jak w poprzednich falach.

[Reguły pomijania powtórek](DEDUPLIKACJA.md) · [Raport kontroli](../kontrola.json)
