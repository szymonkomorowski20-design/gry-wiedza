# Chiptune, trackery i generatory dźwięku

Dział katalogu: [08d — chiptune i trackery](../katalog/08d-chiptune-trackery.md), [08c — generatory i synteza](../katalog/08c-generatory-synteza.md). Liczby gwiazdek z GitHuba z 26 września 2026.

## Trackery — tworzenie muzyki retro

| Narzędzie | Licencja | Co robi |
|---|---|---|
| [Furnace](https://github.com/tildearrow/furnace) (★3,8 tys.) | GPL-2.0 lub nowsza (z ASIO: GPL-3.0; rdzenie emulacji — własne licencje) | tracker wielu układów naraz: NES, Game Boy, Mega Drive (YM2612), SNES, C64 (SID), OPL, AY i dziesiątki innych; otwiera moduły DefleMask |
| [BambooTracker](https://github.com/bambootracker/bambootracker) (★583) | GPL-2.0 | tracker układu YM2608 (FM, PC-98); odtwarzacz dla Godota: `maxotaku11niku/bambootrackerplayer` |
| [klystrack](https://github.com/kometbomb/klystrack) (★547) | MIT (tekst w pliku LICENSE; GitHub nie rozpoznaje) | tracker z własnym syntezatorem chip — prosty start |
| [0CC-FamiTracker](https://github.com/hertzdevil/0cc-famitracker) (★330) | GPL-2.0 | rozszerzony FamiTracker (NES 2A03 + rozszerzenia) |
| [chiptrack](https://github.com/jturcotte/chiptrack) (★188) | GPL-3.0 | programowalny sekwencer dla Game Boy Advance |
| OpenMPT, MilkyTracker, FamiTracker, DefleMask | — | w katalogach fal 01–04 |

**Licencja narzędzia ≠ licencja muzyki.** GPL trackera nie obejmuje utworów, które w nim skomponujesz — muzyka jest Twoja.

## Odtwarzanie formatów retro w grze

- **Pliki audio (najprościej):** wyeksportuj z trackera WAV/OGG i graj normalnie w Godocie.
- **Natywne moduły (małe pliki, pętle bez szwów):** libopenmpt (MOD/XM/IT/S3M), Game Music Emu (NSF/SPC/VGM/GBS), [vgmstream](https://github.com/vgmstream/vgmstream) (strumieniowe formaty z gier — tylko do analizy), [zxtune](https://github.com/vitamin-caig/zxtune) (ZX Spectrum), [nsfplay](https://github.com/bbbradsmith/nsfplay). Dla Godota 4 brak dojrzałej wtyczki GME — `godot-FLMusicLib` jest dla Godota 3.
- **Synteza na żywo:** [godot-blipkit](https://github.com/detomon/godot-blipkit) (MIT) — GDExtension z brzmieniem starych układów, sterowany z GDScript.

## Generatory efektów (SFX bez nagrań)

| Generator | Licencja | Uwagi |
|---|---|---|
| **8bit-sfx** — `cportka/8bit-sfx` | MIT | 8888 efektów w 44 kategoriach (skok, moneta, laser, eksplozja, UI, RPG, perkusja…), każdy z opisem w katalogu; deterministyczny — `render('kick_003')` zawsze daje te same próbki. Cała biblioteka wyrenderowana do WAV w `BAZA-AI/assety/fala-05/8bit-sfx-wav` (147 MB), komplet w paczce `8bit-sfx-komplet` (ZIP 14,8 MB) |
| [procedural-sounds](https://github.com/m1ckc3s/procedural-sounds) (★192) | MIT | dźwięki interfejsu generowane w przeglądarce |
| [audio (raphaelsalaja)](https://github.com/raphaelsalaja/audio) (★581) | MIT | deklaratywna synteza dla weba |
| [engine-sound-generator](https://github.com/antonio-r1/engine-sound-generator) | MIT | dźwięk silnika spalinowego (Web Audio) — gry wyścigowe |
| [engine-sim](https://github.com/ange-yaghi/engine-sim) | — | symulator silnika spalinowego z realistycznym dźwiękiem |
| [Pink Trombone](https://github.com/zakaton/pink-trombone) (★222) | GPL-3.0 | synteza głosu z modelu traktu głosowego — „bełkot” postaci |
| [noise-canvas](https://github.com/robclouth/noise-canvas) (★297) | AGPL-3.0 | malowanie dźwięków na spektrogramie |
| sfxr, bfxr, jsfxr, jfxr, ChipTone | różne | w katalogach fal 01–04 |

## Muzyka proceduralna i adaptacyjna

- `gvastethecreator/game-music-composer` (CC0) — skill dla agentów AI + studio w przeglądarce: 32 style, 240 gotowych „cue”, eksport MIDI i audio; oryginalne banki Mega Drive/SNES. Paczki: `gmc-muzyka-ogg`, `gmc-midi-i-banki`.
- [divisi](https://github.com/hyprtuna/divisi) (MIT) — muzyka adaptacyjna w Godocie 4: zegar muzyczny i sygnały na beat/takt.
- W Godocie bez wtyczek: `AudioStreamInteractive` i `AudioStreamSynchronized` ([opracowanie 03](03-audio-w-godot.md)).

## Jak wybrać

1. Gra retro 8-bit, mało czasu → 8bit-sfx (SFX) + gotowe utwory z `gmc-muzyka-ogg`.
2. Własna muzyka chip → Furnace, eksport OGG z pętlą.
3. Dźwięk reagujący na rozgrywkę (silnik, głos, szum) → generator lub `AudioStreamGenerator` (uwaga: w webie tylko tryb Stream).
