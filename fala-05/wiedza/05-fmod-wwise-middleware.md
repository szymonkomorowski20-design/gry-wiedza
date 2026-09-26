# FMOD, Wwise i middleware audio

Dział katalogu: [08e — middleware](../katalog/08e-middleware.md) (tematy GitHuba `fmod`, `wwise`, `audio-middleware`: 333 repozytoria + linki z ich README).

## Po co middleware

Middleware (FMOD Studio, Audiokinetic Wwise) przenosi logikę dźwięku z kodu do narzędzia dla sound designera: zdarzenia (`event:/Player/Footstep`), parametry (prędkość, powierzchnia, zdrowie), warstwy muzyki, miks, przestrzeń 3D. Programista wywołuje tylko zdarzenie i ustawia parametry.

**Kiedy warto:** duża gra z dedykowanym sound designerem, muzyka mocno adaptacyjna, wiele platform. **Kiedy nie:** mała gra jednoosobowa, gra webowa, prototyp — wbudowane klasy Godota 4 (`AudioStreamInteractive`, `AudioStreamRandomizer`, szyny) wystarczają i nie dokładają licencji ani zależności binarnych.

## Licencje — sprawdź przed wydaniem

FMOD i Wwise są **komercyjne** z darmowymi progami dla małych projektów; warunki (progi budżetu/przychodu, wymóg rejestracji projektu, logo w napisach) zmieniają się. Integracje z GitHuba mają własne licencje (często MIT), ale nie zastępują licencji samego silnika audio. Aktualne warunki: strony licencyjne FMOD i Audiokinetic (w katalogu: `fmod.com/legal`, strony `audiokinetic.com`).

## Integracje z silnikami (z katalogu)

| Projekt | Silnik | Licencja integracji |
|---|---|---|
| [utopia-rise/fmod-gdextension](https://github.com/utopia-rise/fmod-gdextension) (★938) | Godot 4 | MIT |
| [alessandrofama/wwise-godot-integration](https://github.com/alessandrofama/wwise-godot-integration) (★446) | Godot | brak SPDX |
| [heraldofgargos/godot-fmod-integration](https://github.com/heraldofgargos/godot-fmod-integration) (★178) | Godot 3 | MIT |
| `gamecraftguild/fmod-gdextension-csharp-binding` | Godot 4 C# | MIT |
| [salzian/bevy_fmod](https://github.com/salzian/bevy_fmod) (★92) | Bevy | Apache-2.0 |
| [martenfur/fmodforfoxes](https://github.com/martenfur/fmodforfoxes) (★140) | C# (MonoGame) | MIT |
| [huailiang/lipsync](https://github.com/huailiang/lipsync) (★497) | Unity — ruch ust z głosu, obsługa FMOD | MIT |
| `VilleOjala/FMOD-Unity-Tools`, `VilleOjala/UE5-Wwise_SpatialBlendAreas` | Unity / UE5 | MIT / Apache-2.0 |
| [microsoft/ProjectAcoustics](https://github.com/microsoft/ProjectAcoustics) (★170) | akustyka falowa dla Unity/Unreal, z Wwise | CC-BY-4.0 (repozytorium) |
| `msub2/fmod-webxr-test`, `msub2/wwise-webxr-test` | WebXR | MIT |

## Narzędzia do banków (.bank, .bnk, .fsb, .wem)

W katalogu jest wiele narzędzi do otwierania i przebudowy banków (`bnnm/wwiser`, `vswarte/rewwise`, `JSleim/bnk-tools`, `lhx077/FSBProcessor`, `9382/FMODBankDecryptor`, edytory soundbanków). **Do czego legalnie:** debugowanie własnych banków, modyfikacje gier, które na to pozwalają, badania formatów. **Nie:** wyciąganie muzyki i efektów z cudzych gier do własnego projektu — pliki pozostają chronione prawem autorskim niezależnie od narzędzia.

## Alternatywy open source

- **Pure Data → kod:** [hvcc (Heavy compiler)](https://github.com/wasted-audio/hvcc) (★417, GPL-3.0) kompiluje łatki Pure Data do C/C++ i wtyczek — proceduralny dźwięk bez middleware.
- **Silniki audio C/C++:** miniaudio, SoLoud, OpenAL Soft (fale 01–04) oraz nowe w tej fali, m.in. `rope-50/rope-audio` (C++20, bez blokad).

## Rekomendacja dla game-buildera

Domyślnie **bez middleware**. Decyzję „FMOD/Wwise” dopuszczać tylko w karcie decyzji na etapie bootstrapu, z jawnym wpisem o licencji i o braku wsparcia eksportu webowego przez większość integracji.
