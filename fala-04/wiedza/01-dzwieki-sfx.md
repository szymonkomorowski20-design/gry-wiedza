# Efekty dźwiękowe w grze — od paczki do miksu

Opracowanie na podstawie repozytoriów SFX z fali 04 i ich zawartości. Opisuje praktykę; nie jest recenzją każdego nagrania.

## Co realnie dostałeś w tej fali

| Paczka / źródło | Zawartość | Licencja | Gdzie |
|---|---|---|---|
| Zulubo Sounds | 290 WAV: zniszczenia (butelka, puszka, szkło, okno), otoczenie (windy, kolejka linowa, drzwi sci-fi, dźwignie), kroki (metal), interakcje (klamka, karton, plastik), fizyka uderzeń | MIT | [paczka](../paczki/zulubo-sounds.zip) |
| mrbid Sound-Effects | 63 WAV z syntezatora: alarmy, blipy, „collect”, teleport, statek kosmiczny, obcy, silnik | Unlicense | [paczka](../paczki/mrbid-sound-effects.zip) |
| JimLynchCodes, Cuboos SS13, Kavex, moutend, buckn (bfxr) | razem ~150 plików | brak licencji lub GPL | tylko lokalnie w `BAZA-AI/fala-04` |
| sourcesounds (21 repo, ok. 18 GB) | dźwięki gier Valve | własność Valve | tylko opisane linki — nie do użycia |

Zulubo nagrywał pliki sam, a kilka przerobił z domeny publicznej; to dobre źródło „fizycznych” dźwięków 3D. mrbid pasuje do arcade i sci-fi.

## Formaty i ustawienia importu

- **Źródło trzymaj w WAV** (bezstratnie). Do gry eksportuj krótkie efekty jako WAV lub OGG, a muzykę i długie pętle jako OGG (strumieniowanie).
- **Mono dla dźwięków w przestrzeni 3D.** Silnik sam je rozmieszcza. Stereo zostaw dla UI, muzyki i ambientu „w głowie” gracza.
- Pliki z końcówką `_lp` (np. `CableCar_lp.wav` w Zulubo) to pętle — włącz zapętlenie w imporcie i sprawdź, czy nie ma trzasku na styku.
- `moutend/SoundEffect` pokazuje prosty pipeline SoX: 22 050 Hz, mono, 16 bit. Taki format wystarcza dla krótkich efektów UI.

## Jak sprawić, by dźwięki nie męczyły

1. **Warianty zamiast jednego pliku.** Dla kroku lub uderzenia losuj 3–5 próbek.
2. **Losowa wysokość i głośność** (np. ±5% pitch, ±2 dB) na każde odtworzenie.
3. **Warstwowanie**: uderzenie = transjent (klik) + ciało (materiał) + ogon (pogłos otoczenia).
4. **Priorytety i limity głosów**: nie odtwarzaj 30 identycznych trafień w jednej klatce.
5. **Magistrale miksu**: osobno SFX, UI, muzyka, dialogi — gracz musi mieć suwaki.
6. **Wyrównaj głośność** paczek z różnych źródeł, zanim ustawisz miks — paczki mają różne poziomy.

## Generatory zamiast nagrań

`buckn/game_sounds` zawiera 33 pliki `.bfxrsound` — to ustawienia generatora bfxr, a nie gotowy dźwięk. Otwórz je w bfxr, zmodyfikuj i wyeksportuj WAV. Tak szybko powstają retro efekty w jednym stylu. W katalogu fali 04 znajdziesz więcej generatorów i edytorów w dziale [Dźwięk i muzyka](../katalog/08-audio.md).

## Licencje — pułapki

- **GPL na dźwiękach** (Kavex/GameSounds) — licencja programowa na assetach utrudnia zamknięte wydanie. Omijaj ją w projekcie komercyjnym.
- **„Według mojej wiedzy royalty-free”** (JimLynchCodes) to nie licencja. Użyj tylko do prototypu.
- **Przerobione nagrania Freesound** (moutend) dziedziczą licencje oryginałów: sprawdź każdy oryginał.
- **Dźwięki z gier komercyjnych** (sourcesounds) służą tylko do odsłuchu i analizy stylu.
- Paczka arnofaure/free-sfx deklaruje CC BY 4.0, ale jej ZIP jest dziś niedostępny.

Zapisuj źródło, autora i licencję każdego dźwięku w rejestrze zasobów projektu ([szablon z fali 02](../../fala-02/szablony/REJESTR-ZASOBOW.md)).

[Katalog: Dźwięk i muzyka](../katalog/08-audio.md) · [Paczki fali 04](../paczki/README.md)
